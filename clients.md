# How Clients Should Work

This is an overview of how the communication part of a client should work, with things such as:
- Variables that should exist and their type
- Methods that should exist and the order of the operations they perform

## Variables

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

## Methods

### Start

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

### End

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
