---
title: Server
nav_order: 3
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

A server implementation for the Raspberry Pi can be installed by running:

```bash
curl -s https://animatedledstrip.github.io/install/install-pi-server.sh | sudo bash
```

### Creating a New Server Executable

The AnimatedLEDStrip server library is combined with a device library to run a server on that device.
Both are added as dependencies and a short main method is added.

Example main method:

```kotlin
fun main(args: Array<String>) {
    startServer(args, WS281xCompat::class)
}
```

Replace `WS281xCompat::class` with the class from the device library being used.

See the [Raspberry Pi Server](#raspberry-pi-server) for an example server executable.
