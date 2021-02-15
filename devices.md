---
title: Devices
nav_order: 6
---

# AnimatedLEDStrip Device Libraries

AnimatedLEDStrip uses device libraries to bridge the gap between the abstract code in the core library and the physical LEDs.

## Available Device Libraries

Currently only one device library is available, for the Raspberry Pi:

- [Raspberry Pi](https://github.com/AnimatedLEDStrip/device-pi)

## Using a Device Library

See [Creating a New Server Executable](/server#creating-a-new-server-executable).

## Creating a Device Library

New device libraries are fairly simple to create.
They must include one class that implements `NativeLEDStrip`.

The class implementing `NativeLEDStrip` must have one argument in its primary constructor:

- A `StripInfo` instance that should be used to set appropriate parameters.

See the [Raspberry Pi Device Library](https://github.com/AnimatedLEDStrip/device-pi) for an example of a device library.

