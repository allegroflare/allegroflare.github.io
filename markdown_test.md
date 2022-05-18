## Placement2D

Placement2D is typically used for positioning objects on a screen (sprites), but it can also work as a camera. It has the properties position, size, align, scale, and anchor. All of these are vec2d(x, y). It also has rotation (float) and flip, also vec2d(x, y).

You would typically position objects (sprites, text) by:

```c++
Placement2D place;
place.start_transform();
  // do your drawing here, as if the orientation is 0, 0
place.restore_transform();
For a Camera, rather than using start_transform(), you would use start_reverse_transform(), and have these calls wrap around the objects when they are being drawn in the scene.
```

So,

```cpp
Placement2D camera;
camera.start_reverse_transform();
  // draw all your entities here using their usual world coordinates
camera.restore_transform();
```

By default, Placement2D has an alignment of (0.5, 0.5), so your camera will zoom in and out, and be pointed such that the position of the camera (position.x, position.y) is at the center of the screen.

So, if your character sprite is at (300, 200), and your camera is at position (300, 200), then the character will be at the center of the screen. And, when you zoom in/out, the character will still be at the center.

Note that you can nest multiple Placement2Ds inside each other and they will retain the transform from the previous element.

```c++
Placement2D camera;
camera.start_reverse_transform();
  Placement2D sprite_placement;
  sprite_placement.start_transform();
     al_draw_bitmap(bmp, 0, 0, 0);
  sprite_placement.restore_transform();

  Placement2D sprite_placement2;
  sprite_placement2.start_transform();
     al_draw_bitmap(bmp2, 0, 0, 0);
  sprite_placement2.restore_transform();
camera.restore_transform();
```
