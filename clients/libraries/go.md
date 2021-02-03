---
title: Go
parent: Client Libraries
grand_parent: Clients
---

# AnimatedLEDStrip Client Library for Go

This library allows a Go client to communicate with an AnimatedLEDStrip server.

## Using the Library in a Project

The library can be downloaded with:

```bash
go get github.com/AnimatedLEDStrip/client-go
```

## Creating an `ALSHttpClient`

A new client is created with `ALSHttpClient(ipAddress)`.

```go
import als "github.com/AnimatedLEDStrip/client-go"

client := als.ALSHttpClient("10.0.0.254")
```

## Communicating with the Server

This library follows the conventions laid out for [AnimatedLEDStrip client libraries](/clients/client-libraries), with the following modifications:

- Function names and struct variables are capitalized because of how Go denotes exported identifiers
- `DegreesRotation` and `RadiansRotation` are constructors for the `rotation` struct, which uses the `RotationType` variable to track which type it is
- `AbsoluteDistance` and `PercentDistance` are constructors for the `distance` struct, which uses the `DistanceType` variable to track which type it is
- `ColorContainer` and `PreparedColorContainer` have a `ContainerType` variable that works similarly to above, though the structs are different
- The `colors` parameter for an `AnimationToRunParams` struct only accepts `ColorContainer`s
- The `default` parameter for an `AnimationParameter` hasn't been figured out yet
