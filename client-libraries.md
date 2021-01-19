# AnimatedLEDStrip Client Libraries

Clients can be written in any language, provided they send the correct JSON communications to the server.
Client libraries are designed to simplify that.

Currently, client libraries are written for the following languages:
- [C++](https://github.com/AnimatedLEDStrip/client-cpp)
- [Dart](https://github.com/AnimatedLEDStrip/client-dart)
- [Go](https://github.com/AnimatedLEDStrip/client-go)
- [Kotlin/JVM](https://github.com/AnimatedLEDStrip/client-kotlin-jvm)
- [Python 3](https://github.com/AnimatedLEDStrip/client-python)
- [Ruby](https://github.com/AnimatedLEDStrip/client-ruby)
- Rust

## Library Features

### Receiving Capability

<table>
  <tr>
    <th>Language</th>
    <th align="center">AnimationData</th>
    <th align="center">AnimationInfo</th>
    <th align="center">EndAnimation</th>
    <th align="center">Message</th>
    <th align="center">Section</th>
    <th align="center">StripInfo</th>
  </tr>
  <tr>
    <td>C++</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">❌</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Dart</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Go</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Kotlin/JVM</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Python 3</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Rust</td>
    <td />
    <td />
    <td />
    <td />
    <td />
    <td />
  </tr>
</table>

### Sending Capability

<table>
  <tr>
    <th>Language</th>
    <th align="center">AnimationData</th>
    <th align="center">AnimationInfo</th>
    <th align="center">Command</th>
    <th align="center">EndAnimation</th>
    <th align="center">Section</th>
  </tr>
  <tr>
    <td>C++</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">❌</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Dart</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Go</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Kotlin/JVM</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Python 3</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Rust</td>
    <td />
    <td />
    <td />
    <td />
    <td />
  </tr>
</table>

### Other Capabilities

<table>
  <tr>
    <th>Language</th>
    <th align="center">Partial Data*</th>
    <th align="center">Callbacks**</th>
  </tr>
  <tr>
    <td>C++</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Dart</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Go</td>
    <td align="center">❌</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Kotlin/JVM</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Python 3</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Rust</td>
    <td />
    <td />
  </tr>
</table>

\* Ability to handle an incomplete communication from the server that is completed later

** Program can specify actions to execute when certain events occur

## Creating a New Client Library

This is an overview of how the communication part of a client should work, with things such as:

- Variables that should exist and their type
- Methods that should exist and pseudocode for their operation

All client libraries should follow this format, though small variations are expected because not every language works the same.

### Variables

```
address: String
port: Int
connection: Socket

started: Boolean
connected: Boolean

runningAnimations: Map<String, AnimationData>
sections: Map<String, Section>
supportedAnimations: Map<String, AnimationInfo>
stripInfo: StripInfo

onConnectCallback: (ip: String, port: Int) -> Any
onDisconnectCallback: (ip: String, port: Int) -> Any
onUnableToConnectCallback: (ip: String, port: Int) -> Any

onReceiveCallback: (data: String) -> Any
onNewAnimationInfoCallback: (AnimationInfo) -> Any
onNewCurrentStripColorCallback: (CurrentStripColor) -> Any
onNewEndAnimationCallback: (EndAnimation) -> Any
onNewMessageCallback: (Message) -> Any
onNewRunningAnimationParamsCallback: (RunningAnimationParams) -> Any
onNewSectionCallback: (Section) -> Any
onNewStripInfoCallback: (StripInfo) -> Any
```

### Methods

#### Start

```
if started
  return

clear runningAnimations
clear sections
clear supportedAnimations
stripInfo = null

started = true

try
  connect socket	// timeout 2s
except
  call onUnableToConnectCallback
  started = false
  connected = false
  return

connected = true
call onConnectCallback

start receive loop
```

#### End

```
if not connected
  return
started = false
connected = false
close socket
stop receive loop
```

### Receive Loop

```
while connected
  try
    read input from socket
  except io error
    started = false
    connected = false
    call onDisconnectCallback
    return

  append partialData to beginning of input
  clear partialData
  split input into inputList by ';;;'
  if last input in inputList is incomplete
    save last input to partialData
    remove last input from inputList

  for splitData in inputList
    if splitData is an empty string
      continue

    call onReceiveCallback
    
    data = decodeJson(splitData)

    if data is AnimationInfo
      add instance to supported animations
      call onNewAnimationInfoCallback
    else if data is AnimationToRunParams
      print warning "Receiving AnimationToRunParams is not supported by client"
    else if data is ClientParams
      print warning "Receiving ClientParams is not supported by client"
    else if data is Command
      print warning "Receiving Command is not supported by client"
    else if data is EndAnimation
      call onNewEndAnimationCallback
      remove animation from running animations
    else if data is Message
      call onNewMessageCallback
    else if data is RunningAnimationParams
      call onNewRunningAnimationParamsCallback
      add instance to running animations
    else if data is Section
      call onNewSectionCallback
      add instance to sections
    else if data is StripInfo
      set stripInfo to instance
      call onNewStripInfoCallback
    else
      print warning "Unrecognized data type: $data"
```
