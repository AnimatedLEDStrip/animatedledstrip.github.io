---
title: Colors
nav_order: 2
parent: Core
---

# Colors in the AnimatedLEDStrip Library

The AnimatedLEDStrip library includes the [`ColorContainer`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.colors/-color-container/index.html) class, which is used to send colors to an animation.
A `ColorContainer` can hold a variable number of colors and will prepare the colors when it is sent to the animation so the colors fade from one to the next along the whole strip.
A `PreparedColorContainer` is the prepared form of the `ColorContainer` and is used by the animation.

Colors can be set and retrieved using a variety of methods. Examples include:
```kotlin
val a = ColorContainer(0xFF, 0xFF00FF)        // Construction with a variable number of arguments
val b = ColorContainer(0xFFFF)

a[0]                                          // Returns 0xFF as a Long
a[0..1]                                       // Returns List<Long>(0xFF, 0xFF00FF)
a[1, 0]                                       // Returns List<Long>(0xFF00FF, 0xFF)
b[3]                                          // Returns 0xFFFF (because there is only one color in the ColorContainer)
a[3]                                          // Returns 0 (because there are multiple colors in the ColorContainer 
                                              // and 3 is not a valid index)

a[1] = 0xFF00                                 // a.colors = [0xFF, 0xFF00]
a[4] = 0xFFFFFF                               // a.colors = [0xFF, 0xFF00, 0xFFFFFF]
a += 0xFF0000                                 // a.colors = [0xFF, 0xFF00, 0xFFFFFF, 0xFF0000]
a[2..4] = 0xFFFF00                            // a.colors = [0xFF, 0xFF00, 0xFFFF00, 0xFFFF00, 0xFFFF00]
a[0, 3] = 0x0                                 // a.colors = [0x0,  0xFF00, 0xFFFF00, 0x0,      0xFFFF00]
```

## [`grayscale()`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.colors/grayscale.html) vs [`grayscaled()`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.colors/grayscaled.html) and [`invert()`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.colors/invert.html) vs [`inverse()`](https://animatedledstrip.github.io/AnimatedLEDStrip/animatedledstrip-core/animatedledstrip.colors/inverse.html)
The `ColorContainer` class contains methods for grayscaling and inverting the colors inside it.
There are slight differences between `grayscale()` and `grayscaled()`, and between `invert()` and `inverse()`.
For example:
```kotlin
val c = ColorContainer(0xFF00FF, 0xFFFF00)
c.invert()                                            // c.colors = [0x00FF00, 0x0000FF]
val d = c.inverse()                                   // c.colors = [0x00FF00, 0x0000FF]
                                                      // d.colors = [0xFF00FF, 0xFFFF00]
```
Notice how `invert()` changed the colors in `c` while `inverse()` did not.

`grayscale()` and `invert()` change the `ColorContainer` they are invoked upon and return a reference to that `ColorContainer`.

`grayscaled()` and `inverse()` create a new `ColorContainer` with the grayscale/inverse and return the new `ColorContainer` while leaving the original alone.
