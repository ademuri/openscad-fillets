# openscad-fillets
Git-ified version of https://www.thingiverse.com/thing:2461392

## Summary

This is a library to apply fillets to both your 2d and 3d objects in OpenSCAD.

If you have ever tried to add a fillet to a complex shape in OpenSCAD, you quickly realize that it's no easy task. In fact, it can be nearly impossible. There is nothing built in that allows you to accomplish fillets in an easy way.

This library was built out of the need for something more performant than the existing solutions. It's not perfect for all purposes, but with some planning it can be used to make your 3d prints much better.

There are two files included here. fillets2d.scad and fillets3d.scad. They can be used together or independently.

For 3d fillets, I change steps to match whatever my printing layer height will be. For example, for a 0.3mm layer height print, and a fillet of 3mm, I would set steps to 10 (3 / 0.3), so the steps match my print layer height. If you are making a generic object, 1 step per 0.1mm would be considered good quality.

The 3d fillet library also has an "enable" flag. For complex shapes, the fillet can add many objects to the screen, causing previews to be slow. I have spent a lot of time and many iterations of this library to attempt to gain as much performance as possible. If you are encountering slow down, set e=0 until you are ready to render.

## fillets2d.scad

This library is used to add rounding or fillets to your 2d objects. It has two modules:
- ```
  rounding2d(r)
  r = radius of rounding
  ```
  `rounding2d` removes material to round the outside corners of a shape.

- ```
  fillet2d(r)
  r = radius of rounding
  ```
  `fillet2d` adds material to round the inside corners of a shape.

## fillets3d.scad

This library is used to add top and/or bottom fillets to your 3d objects. It has 3 modules:

- ```
  topBottomFillet(b, t, r, s, e)
  b = z of bottom of 3d object
  t = z of top of 3d object
  r = radius of fillet
  s = steps of filler (smaller is smoother)
  e = enabled (pass e = 0 to disable fillet for faster preview)
  ```

- ```
  topFillet(t, r, s, e)
  t = z of top of 3d object
  r = radius of fillet
  s = steps of filler (smaller is smoother)
  e = enabled (pass e = 0 to disable fillet for faster preview)
  ```

- ```
  bottomFillet(b, r, s, e)
  b = z of bottom of 3d object
  r = radius of fillet
  s = steps of filler (smaller is smoother)
  e = enabled (pass e = 0 to disable fillet for faster preview)
  ```
  
## Examples
### 2D Example

```c++
use <fillets2d.scad>;
linear_extrude(1)
rounding2d(1)
fillet2d(1)
difference() {
    union() {
        square([10, 10], center = true);
        translate([5, 5])
        square([10, 10], center = true);
    }

    translate([-5, -5])
    square([10, 10], center = true);

    translate([8, 8])
    circle(3);
}
```

### 3D Example

```c++
use <fillets3d.scad>;
topBottomFillet(b = 0, t = 10, r = 2, s = 20)
linear_extrude(10, scale = 1.2)
difference() {
    union() {
        square([10, 10], true);
        translate([-15, 0]) circle(15);
    }
    translate([-15, 0]) circle(8);
    translate([-15, 0]) square([13, 13], center = true);
}
```

### Both example

```c++
use <fillets2d.scad>;
use <fillets3d.scad>;
topBottomFillet(b = 0, t = 10, r = 1, s = 10)
linear_extrude(10)
rounding2d(1)
fillet2d(1)
difference() {
    union() {
        square([10, 10], true);
        translate([-15, 0]) circle(15);
    }
    translate([-15, 0]) circle(8);
    translate([-15, 0]) square([13, 13], center = true);
}
```
