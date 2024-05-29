---
title: Server
nav_order: 4
has_children: true
---

[GitHub Repo](https://github.com/AnimatedLEDStrip/server){: .btn }

# AnimatedLEDStrip Server

The server library adds two features to the core library:

- Command line and config file parsing
- An HTTP server for clients to communicate with

## Usage

### Raspberry Pi Server

[GitHub Repo](https://github.com/AnimatedLEDStrip/server-pi){: .btn }

A 32 bit server implementation for the Raspberry Pi can be installed by running:

```bash
curl -s https://animatedledstrip.github.io/install/install-pi-server-32bit.bash | sudo bash
```

A 64 bit server implementation for the Raspberry Pi can be installed by running:

```bash
curl -s https://animatedledstrip.github.io/install/install-pi-server-64bit.bash | sudo bash
```

### Creating a New Server Executable

The AnimatedLEDStrip server library, a compatibility class and a short main method are needed to create an executable server.

Example class, connecting AnimatedLEDStrip to the [rpi-ws281x-java](https://github.com/rpi-ws281x/rpi-ws281x-java) library:

```kotlin
class WS281xCompat(stripInfo: StripInfo) : Ws281xLedStrip(
    stripInfo.numLEDs,
    stripInfo.pin ?: 12,
    800000,
    10,
    255,
    0,
    false,
    LedStripType.WS2811_STRIP_GRB,
    false,
), NativeLEDStrip {

    override val numLEDs: Int = stripInfo.numLEDs

    override fun close() {}

    override fun setPixelColor(pixel: Int, color: Int) =
        setPixel(
            pixel,
            color shr 16 and 0xFF,
            color shr 8 and 0xFF,
            color and 0xFF,
        )
}
```

Example main method:

```kotlin
fun main(args: Array<String>) {
    startServer(args, WS281xCompat::class)
}
```

Replace `WS281xCompat::class` with the class you create.

See the [Raspberry Pi Server](#raspberry-pi-server) for an example server executable.
