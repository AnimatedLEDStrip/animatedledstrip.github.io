---
title: Pixel Colors
nav_order: 3
parent: Core
---

# Pixel Colors in the AnimatedLEDStrip Library

The AnimatedLEDStrip library uses the concept of a LED pixel having four colors "assigned" to it:
- Actual Color - The color you see on the strip
- Fade Color - The color the strip is currently at as it fades to the prolonged color
- Prolonged Color - The color the pixel will fade or revert to
- Temporary Color - A color that overrides the fade and prolonged colors until the pixel is reverted

When the `LEDStripRenderer` is ready to send a color to a pixel in the strip, it asks the `PixelColor` associated with the pixel to figure out what color should be sent.

- First, the `PixelColor` checks if the temporary color is set to anything other than `-1`. If it isn't `-1`, then it uses the temporary color
- Next, if the temporary color is not set, it then uses the fade color if the fade color is not `-1`
- Last, if both the temporary and fade colors are not set, then it uses the prolonged color
- It then sets the color using the `NativeLEDStrip` sent to it
- The actual color is updated to reflect what was just sent to the `NativeLEDStrip`
- It then fades the fade color towards the prolonged color, if the fade color is set and if the renderer told it to perform the fade
- Once all pixels have been updated, the renderer tells the `NativeLEDStrip` to render the colors
