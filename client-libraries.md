# AnimatedLEDStrip Client Libraries

Clients can be written in any language, provided they send the correct JSON communications to the server.
Client libraries are designed to simplify that.

Currently, client libraries are written for the following languages:
- [C++](https://github.com/AnimatedLEDStrip/client-cpp)
- Dart
- [Go](https://github.com/AnimatedLEDStrip/client-go)
- [Kotlin/JVM](https://github.com/AnimatedLEDStrip/client-kotlin-jvm)
- [Python 3](https://github.com/AnimatedLEDStrip/client-python)
- [Ruby](https://github.com/AnimatedLEDStrip/client-ruby)
- Rust

## Library Feature Chart
<table>
  <tr>
    <th>Language</th>
    <th align="center">AnimationData*</th>
    <th align="center">AnimationInfo*</th>
    <th align="center">EndAnimation*</th>
    <th align="center">Section*</th>
    <th align="center">StripInfo*</th>
    <th align="center">Partial Data**</th>
    <th align="center">Callbacks***</th>
  </tr>
  <tr>
    <td>C++</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Dart</td>
    <td />
    <td />
    <td />
    <td />
    <td />
    <td />
    <td />
  </tr>
  <tr>
    <td>Go</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">❌</td>
    <td align="center">❌</td>
  </tr>
  <tr>
    <td>Kotlin/JVM</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Python 3</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">❌</td>
    <td align="center">✅</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅/✅</td>
    <td align="center">✅</td>
    <td align="center">❌</td>
  </tr>
  <tr>
    <td>Rust</td>
    <td />
    <td />
    <td />
    <td />
    <td />
    <td />
    <td />
  </tr>
</table>
* Send/Receive capability

** Ability to handle an incomplete communication from the server that is completed later

*** Program can specify actions to execute when certain events occur

## Creating a New Client Library

This is an overview of how the communication part of a client should work, with things such as:

- Variables that should exist and their type
- Methods that should exist and the order of the operations they perform

All client libraries should follow this format.

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
onNewAnimationDataCallback: (AnimationData) -> Any
onNewAnimationInfoCallback: (AnimationInfo) -> Any
onNewEndAnimationCallback: (EndAnimation) -> Any
onNewMessageCallback: (Message) -> Any
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
    break
  except io error
    started = false
    connected = false
    call onDisconnectCallback
    return

  append partialData to beginning of input
  clear partialData
  split input into inputList by ';;;'
  if last input in inputList is incomplete, save to partialData and remove from inputList

  for data in inputList
    if data is an empty string
      continue

    call onReceiveCallback

    if type is AnimationData (DATA:)
      create instance
      call onNewAnimationDataCallback
      add instance to running animations
    else if type is AnimationInfo (AINF:)
      create instance
      add instance to supported animations
      call onNewAnimationInfoCallback
    else if type is Command (CMD :)
      print warning "Receiving Command is not supported by client"
    else if type is EndAnimation (END :)
      create instance
      call onNewEndAnimationCallback
      remove animation from running animations
    else if type is Message (MSG :)
      create instance
      call onNewMessageCallback
    else if type is Section (SECT:)
      create instance
      call onNewSectionCallback
      add instance to sections
    else if type is StripInfo (SINF:)
      create instance
      set stripInfo to instance
      call onNewStripInfoCallback
    else
      print warning "Unrecognized data type: $type"
```
