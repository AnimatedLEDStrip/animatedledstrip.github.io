---
title: Color Set/Get Functions
nav_order: 1
parent: Defining a New Animation
grand_parent: Core
---

# Color Functions

## Setting Colors

There are four colors associated with each pixel, three of which can be set directly (see [Pixel Colors](/core/pixel-colors)).
Each color type (`Fade`, `Prolonged`, `Temporary`) can be set for one or multiple pixels.
Each function is an extension for `AnimationManager`, `SectionManager`, and `LEDStrip` instances.

`setPixel<type>Color` takes a pixel index and a color. - [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-fade-color.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-prolonged-color.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-temporary-color.html)

`setPixel<type>Colors` takes a list of pixel indices or an `IntRange` of pixel indices and a color - [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-fade-colors.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-prolonged-colors.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-pixel-temporary-colors.html)

There are also functions for reverting pixel(s) (removing any temporary color set).
[One pixel](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/revert-pixel.html) or [multiple pixels](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/revert-pixels.html) can be reverted at once.

The color of the full strip (or section that the animation is running in) can be set with `setStrip<type>Color` - [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-strip-fade-color.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-strip-prolonged-color.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/set-strip-temporary-color.html)

[`clear()`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/clear.html) will remove all colors set to all pixels in the strip (or section).

## Getting Colors

There are four colors associated with each pixel (see [Pixel Colors](/core/pixel-colors)).
Each color type (`Actual`, `Fade`, `Prolonged`, `Temporary`) can be retrieved for one or all pixels.
Each function is an extension for `AnimationManager`, `SectionManager`, and `LEDStrip` instances.
Each property is an extension for `LEDStripColorManager`, `LEDStrip`, and `SectionManager` instances.

`getPixel<type>Color` returns the color set for the specified pixel - [Actual](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-actual-color.html), [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-fade-color.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-prolonged-color.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-temporary-color.html)

Each function has a nullable counterpart named `getPixel<type>ColorOrNull` - [Actual](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-actual-color-or-null.html), [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-fade-color-or-null.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-prolonged-color-or-null.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/get-pixel-temporary-color-or-null.html)

The colors of all pixels in the strip (or section) can be retrieved with the `pixel<type>ColorList` properties - [Actual](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/pixel-actual-color-list.html), [Fade](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/pixel-fade-color-list.html), [Prolonged](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/pixel-prolonged-color-list.html), [Temporary](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.leds.colormanagement/pixel-temporary-color-list.html)
