---
title: Client Libraries
nav_order: 1
has_children: true
parent: Clients
---

Currently, client libraries are written for the following languages:
- [C++](https://github.com/AnimatedLEDStrip/client-cpp) (needs update to be compatible with 1.0.0)
- [Dart](https://github.com/AnimatedLEDStrip/client-dart) (needs update to be compatible with 1.0.0)
- [Go](https://github.com/AnimatedLEDStrip/client-go)
- [Kotlin/MPP, supporting Kotlin/JVM and Kotlin/JS](libraries/kotlin-mpp)
- [Python 3](https://github.com/AnimatedLEDStrip/client-python) (needs release to be compatible with 1.0.0)
- [Ruby](https://github.com/AnimatedLEDStrip/client-ruby) (needs release to be compatible with 1.0.0)
- Rust (incomplete)

## Creating a New Client Library

This is an overview of what should be included in the client library, such as:

- Classes that should be created
- HTTP Endpoints to communicate with

All client libraries should follow this format, though small variations are expected because not every language works the same.

### Classes

Because some classes use other classes, the optimal creation order would be:
- `AbsoluteDistance`, `PercentDistance`
- `DegreesRotation`, `RadiansRotation`
- `Equation`, `Location`
- `ColorContainer`, `PreparedColorContainer`
- `AnimationToRunParams`, `RunningAnimationParams`
- `AnimationParameter`
- `AnimationInfo`
- `StripInfo`
- `Section`

#### `AbsoluteDistance`
{: .fs-4 }

- `x` (double) (`0.0`)
- `y` (double) (`0.0`)
- `z` (double) (`0.0`)

#### `AnimationInfo`
{: .fs-4 }

|Parameter|Type|Default|
|:-------:|:--:|:-----:|
|`name`|`String`|`""`|
|`abbr`|`String`|`""`|
|`description`|`String`|`""`|
|`runCountDefault`|`Int`|`0`|
|`minimumColors`|`Int`|`0`|
|`unlimitedColors`|`Boolean`|`false`|
|`dimensionality`|`Set<String>`|`setOf()`|
|`intParams`|`List<AnimationParameter<Int>>`|`listOf()`|
|`doubleParams`|`List<AnimationParameter<Double>>`|`listOf()`|
|`stringParams`|`List<AnimationParameter<String>>`|`listOf()`|
|`locationParams`|`List<AnimationParameter<Location>>`|`listOf()`|
|`distanceParams`|`List<AnimationParameter<AbsoluteDistance/PercentDistance>>`|`mapOf()`|
|`rotationParams`|`List<AnimationParameter<DegreesRotation/RadiansRotation>>`|`mapOf()`|
|`equationParams`|`List<AnimationParameter<Equation>`>|`mapOf()`|

#### `AnimationParameter<T>`
{: .fs-4 }

- `name` (string) (`""`)
- `description` (string) (`""`)
- `default` (nullable of type `T`) (`null`)

#### `AnimationToRunParams`
{: .fs-4 }

- `animation` (string) (`""`)
- `colors` (list(`ColorContainer`/`PreparedColorContainer`)) (`listOf()`)
- `id` (string) (`""`)
- `section` (string) (`""`)
- `runCount` (int) (`0`)
- `intParams` (map(string to int)) (`mapOf()`)
- `doubleParams` (map(string to double)) (`mapOf()`)
- `stringParams` (map(string to string)) (`mapOf()`)
- `locationParams` (map(string to `Location`)) (`mapOf()`)
- `distanceParams` (map(string to `AbsoluteDistance`/`PercentDistance`)) (`mapOf()`)
- `rotationParams` (map(string to `DegreesRotation`/`RadiansRotation`)) (`mapOf()`)
- `equationParams` (map(string to `Equation`)) (`mapOf()`)

#### `ColorContainer`
{: .fs-4 }

- `colors` (list(int)) (`listOf()`)

#### `DegreesRotation`
{: .fs-4 }

- `xRotation` (double) (`0.0`)
- `yRotation` (double) (`0.0`)
- `zRotation` (double) (`0.0`)
- `rotationOrder` (list(string)) (`listOf("ROTATE_Z", "ROTATE_X"`)

#### `Equation`
{: .fs-4 }

- `coefficients` (list(int)) (`listOf()`)

#### `Location`
{: .fs-4 }

- `x` (double) (`0.0`)
- `y` (double) (`0.0`)
- `z` (double) (`0.0`)

#### `PreparedColorContainer`
{: .fs-4 }

- `colors` (list(int))
- `originalColors` (list(int))

#### `RadiansRotation`
{: .fs-4 }

- `xRotation` (double) (`0.0`)
- `yRotation` (double) (`0.0`)
- `zRotation` (double) (`0.0`)
- `rotationOrder` (list(string)) (`listOf("ROTATE_Z", "ROTATE_X"`)

#### `RunningAnimationParams`
{: .fs-4 }

- `animationName` (string) (`""`)
- `colors` (list(`PreparedColorContainer`))
- `id` (string) (`""`)
- `section` (string) (`""`)
- `runCount` (int) (`0`)
- `intParams` (map(string to int)) (`mapOf()`)
- `doubleParams` (map(string to double)) (`mapOf()`)
- `stringParams` (map(string to string)) (`mapOf()`)
- `locationParams` (map(string to `Location`)) (`mapOf()`)
- `distanceParams` (map(string to `AbsoluteDistance`)) (`mapOf()`)
- `rotationParams` (map(string to `RadiansRotation`)) (`mapOf()`)
- `equationParams` (map(string to `Equation`)) (`mapOf()`)
- `sourceParams` (`AnimationToRunParams`)

#### `StripInfo`
{: .fs-4 }

- `numLEDs` (int) (`0`)
- `pin` (nullable int) (`null`)
- `renderDelay` (int) (`10`)
- `isRenderLoggingEnabled` (boolean) (`false`)
- `renderLogFile` (string) (`""`)
- `rendersBetweenLogSaves` (int) (`1000`)
- `is1DSupported` (boolean) (`true`)
- `is2DSupported` (boolean) (`false`)
- `is3DSupported` (boolean) (`false`)
- `ledLocations` (list(`Location`)) (`listOf()`)

#### `Section`
{: .fs-4 }

- `name` (string) (`""`)
- `pixels` (list(int)) (`listOf()`)
- `parentSectionName` (string) (`""`)

### HTTP Endpoints

#### GET Endpoints

- `/animation/{name}` (`getAnimationInfo`, requires one string parameter) (returns `AnimationInfo`)
- `/animations` (`getSupportedAnimations`) (returns list(`AnimationInfo`))
- `/animations/map` (`getSupportedAnimationsMap`) (returns map(string to `AnimationInfo`))
- `/animations/names` (`getSupportedAnimationsNames`) (returns list(string))
- `/running` (`getRunningAnimations`) (returns map(string to `RunningAnimationParams`))
- `/running/ids` (`getRunningAnimationsIds`) (returns list(string))
- `/running/{id}` (`getRunningAnimationParams`, requires one string parameter) (returns `RunningAnimationParams`)
- `/section/{name}` (`getSection`, requires one string parameter) (returns `Section`)
- `/sections` (`getSections`) (returns list(`Section`))
- `/sections/map` (`getSectionsMap`) (returns map(string to `Section`))
- `/strip/color` (`getCurrentStripColor`) (returns list(int))
- `/strip/info` (`getStripInfo`) (returns `StripInfo`)

##### Additional Functions
{: .text-grey-lt-100 }

- `getFullStripSection` (calls `getSection` with `"fullStrip"`)

#### POST Endpoints

- `/animations/newGroup` (`createNewGroup`, requires one `NewAnimationGroupInfo` parameter) (returns `AnimationInfo`)
- `/sections` (`createNewSection`, requires one `Section` parameter) (returns `Section`)
- `/start` (`startAnimation`, requires one `AnimationToRunParams` parameter) (returns `RunningAnimationParams`)
- `/strip/clear` (`clearStrip`) (no return)

#### DELETE Endpoints

- `/running/{id}` (`endAnimation`, requires one string parameter) (returns `RunningAnimationParams`)

##### Additional Functions
{: .text-grey-lt-100 }

- `endAnimation` or `endAnimationFromParams`, requiring one `RunningAnimationParams` parameter (calls `endAnimation` with `param.id`)
