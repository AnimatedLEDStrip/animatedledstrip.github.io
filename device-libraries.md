# Device Libraries

- [Raspberry Pi (device-pi)](https://github.com/AnimatedLEDStrip/device-pi)

A device library is how AnimatedLEDStrip bridges the gap between the abstract code in the core library and the physical LEDs.

## Using a Device Library

See [Creating an Executable Server](https://animatedledstrip.github.io/creating-an-executable-server).

## Creating a Device Library

New device libraries are fairly simple to create.
They must include one class that implements `NativeLEDStrip`.

The class implementing `NativeLEDStrip` must have one argument in its primary constructor:
A `StripInfo` instance (see below) that should be used to set appropriate parameters.

See the [Raspberry Pi Device Library](https://github.com/AnimatedLEDStrip/device-pi) for an example of a device library.

### StripInfo

The `StripInfo` class defines parameters for creating the LED strip such as:
- The number of LEDs
- The pin number
- Time between strip renders
- Whether to enable render logging
- What dimensionality of animations are supported (1d, 2d, 3d)
- etc.

See the `StripInfo` class in the [core library](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/blob/master/src/commonMain/kotlin/animatedledstrip/leds/stripmanagement/StripInfo.kt) for latest parameters available.
