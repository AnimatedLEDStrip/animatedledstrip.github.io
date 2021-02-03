---
title: Home
nav_order: 1
permalink: /
---

# Control LEDs with ease and run stunning animations
{: .fs-9 }

AnimatedLEDStrip is designed to make running fancy animations on LEDs easy, with over 20 animations already provided.
{: .fs-6 .fw-300 }

---

## Getting Started

AnimatedLEDStrip gives you many options for how you integrate it into your project.
If you want a solution that works right out of the box, then.....

## Features

The AnimatedLEDStrip project comes with many features, including:

- Controlling a LED strip and changing the pixel's colors
- Controlling multi-dimensional LED matrices and fields by specifying a location for each pixel
- Running animations on the LEDs, including running multiple animations simultaneously
- Customizing how those animations are run
- Identifying sections of the strip that can be controlled as if they were an independent strip
- An HTTP server that clients can communicate with to control the strip

# AnimatedLEDStrip
The AnimatedLEDStrip set of libraries are meant to simplify the process of running animations on an LED strip to a point that anyone can do it.
The core of the libraries supports concurrency, allowing multiple animations to be run simultaneously, even over the same part of the strip.

## Structure
AnimatedLEDStrip is designed to give you multiple options for how you integrate AnimatedLEDStrip into your project.
You can get a solution that works out of the box, convert your program into a client, or even include the core library directly.

### [Core Library](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip)
Contains all the animations and generic structure for controlling LED strips.
Written in Kotlin/JVM.

### [Server Library](https://github.com/AnimatedLEDStrip/server)
A library for running a server that runs animations on a LED strip.
The server communicates with clients to start and end animations, among other things.
Written in Kotlin/JVM

### [Client Libraries](client-libraries)
Clients can be written in any language, provided they send the correct JSON communications to the server.
Client libraries are designed to simplify that.

### [Device Libraries](device-libraries)
Each device that can run LEDs has its own device library.
Currently the only device supported is the [Raspberry Pi](https://github.com/AnimatedLEDStrip/device-pi), but this can be expanded to more devices in the future.

### Programs
#### [Browser Client](http://alsclient.website)
A website for connecting to an AnimatedLEDStrip server and controlling your LEDs.
Can be found at [alsclient.website](http://alsclient.website).
Written in [Kotlin/JS for React](https://kotlinlang.org/docs/tutorials/javascript/setting-up.html).

#### [ledclient](https://github.com/AnimatedLEDStrip/ledclient)
A command line program for communicating with a server.
Written in C++.
Can be installed by running:
```
curl -s https://animatedledstrip.github.io/install/install-ledclient.sh | sudo bash
```

#### [Raspberry Pi Server](https://github.com/AnimatedLEDStrip/server-pi)
Runs a server for a Raspberry Pi.
Written in Kotlin/JVM.
Can be installed by running:
```
curl -s https://animatedledstrip.github.io/install/install-pi-server.sh | sudo bash
```

#### [Android App](https://github.com/AnimatedLEDStrip/AnimatedLEDStripAndroidControl)
An app for communicating with an AnimatedLEDStrip server.

### Other
#### [Arduino Library](https://github.com/AnimatedLEDStrip/AnimatedLEDStripCppArduino)
Also included in the set of libraries is one written in C++ for Arduinos.
This is the library that started AnimatedLEDStrip.
See our [history](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/wiki#history) for more details.
