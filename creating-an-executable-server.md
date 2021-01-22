# Creating an Executable Server

The [AnimatedLEDStrip server](https://github.com/AnimatedLEDStrip/server) library is combined with a device library to run a server on that device.
Both are added as dependencies and a short main method is added.

Example main method:
```
fun main(args: Array<String>) {
    startServer(args, WS281xCompat::class)
}
```

Replace `WS281xCompat::class` with the class from the device library being used.

See the [Raspberry Pi Server](https://github.com/AnimatedLEDStrip/server-pi)
for an example of how to create a server executable.
