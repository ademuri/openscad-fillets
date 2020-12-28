# openscad-fillets
Git-ified version of https://www.thingiverse.com/thing:2461392

## Summary

This is a library to apply fillets to both your 2d and 3d objects in OpenSCAD.

If you have ever tried to add a fillet to a complex shape in OpenSCAD, you quickly realize that it's no easy task. In fact, it can be nearly impossible. There is nothing built in that allows you to accomplish fillets in an easy way.

This library was built out of the need for something more performant than the existing solutions. It's not perfect for all purposes, but with some planning it can be used to make your 3d prints much better.

There are two files included here. fillets2d.scad and fillets3d.scad. They can be used together or independently.

For 3d fillets, I change steps to match whatever my printing layer height will be. For example, for a 0.3mm layer height print, and a fillet of 3mm, I would set steps to 10 (3 / 0.3), so the steps match my print layer height. If you are making a generic object, 1 step per 0.1mm would be considered good quality.

The 3d fillet library also has an "enable" flag. For complex shapes, the fillet can add many objects to the screen, causing previews to be slow. I have spent a lot of time and many iterations of this library to attempt to gain as much performance as possible. If you are encountering slow down, set e=0 until you are ready to render.
