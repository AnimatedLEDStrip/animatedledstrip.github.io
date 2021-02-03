---
title: Kotlin/MPP
parent: Client Libraries
grand_parent: Clients
---

# AnimatedLEDStrip Client Libary for Kotlin/MPP

This library allows a Kotlin/JVM or Kotlin/JS client to communicate with an AnimatedLEDStrip server.

## Creating an `ALSHttpClient`

A new client is created with `ALSHttpClient(clientEngine, ip)`.
`clientEngine` is a [Ktor `HttpClientEngineFactory`](https://ktor.io/docs/http-client-engines.html)

```kotlin
val client = ALSHttpClient(CIO, ip = "10.0.0.254")
```

An optional configuration for the Ktor engine can be passed as a third argument.
Any configuration should include a JSON feature that uses the AnimatedLEDStrip serializer:

```kotlin
import animatedledstrip.communication.serializer as alsSerializer

install(JsonFeature) {
    serializer = KotlinxSerializer(alsSerializer)
}
```

## Communicating with the Server

This library follows the conventions laid out for [AnimatedLEDStrip client libraries](/clients/client-libraries).