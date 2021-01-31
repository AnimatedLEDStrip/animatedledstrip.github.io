# AnimatedLEDStrip Client Libraries

Clients can be written in any language, provided they send the correct JSON communications to the server.
Client libraries are designed to simplify that.

Currently, client libraries are written for the following languages:
- [C++](https://github.com/AnimatedLEDStrip/client-cpp) (needs update to be compatible with 1.0.0)
- [Dart](https://github.com/AnimatedLEDStrip/client-dart) (needs update to be compatible with 1.0.0)
- [Go](https://github.com/AnimatedLEDStrip/client-go) (needs update to be compatible with 1.0.0)
- [Kotlin/MPP, supporting Kotlin/JVM and Kotlin/JS](https://github.com/AnimatedLEDStrip/client-kotlin-mpp)
- [Python 3](https://github.com/AnimatedLEDStrip/client-python) (needs release to be compatible with 1.0.0)
- [Ruby](https://github.com/AnimatedLEDStrip/client-ruby) (needs update to be compatible with 1.0.0)
- Rust (incomplete)

## Creating a New Client Library

This is an overview of what should be included in the client library, such as:

- Classes that should be created
- HTTP Endpoints to communicate with

All client libraries should follow this format, though small variations are expected because not every language works the same.

### Classes

Because some classes use other classes, the optimal creation order would be:
- `AbsoluteDistance`, `ColorContainer`, `DegreesRotation`, `Equation`, `Location`, `PercentDistance`, `PreparedColorContainer`, `RadiansRotation`
- `AnimationToRunParams`, `RunningAnimationParams`
- `AnimationParameter`
- `AnimationInfo`
- `StripInfo`
- `Section`
- `CurrentStripColor`

#### `AbsoluteDistance`

- `x` (double) (`0.0`)
- `y` (double) (`0.0`)
- `z` (double) (`0.0`)

#### `AnimationInfo`

- `name` (string) (`""`)
- `abbr` (string) (`""`)
- `description` (string) (`""`)
- `runCountDefault` (int) (`0`)
- `minimumColors` (int) (`0`)
- `unlimitedColors` (boolean) (`false`)
- `dimensionality` (set(string)) (`setOf()`)
- `intParams` (list(`AnimationParameter<Int>`)) (`mapOf()`)
- `doubleParams` (list(`AnimationParameter<Double>`)) (`mapOf()`)
- `stringParams` (list(`AnimationParameter<String>`)) (`mapOf()`)
- `locationParams` (list(`AnimationParameter<Location>`)) (`mapOf()`)
- `distanceParams` (list(`AnimationParameter<AbsoluteDistance/PercentDistance>`)) (`mapOf()`)
- `rotationParams` (list(`AnimationParameter<DegreesRotation/RadiansRotation>`)) (`mapOf()`)
- `equationParams` (list(`AnimationParameter<Equation>`)) (`mapOf()`)

#### `AnimationParameter<T>`

- `name` (string) (`""`)
- `description` (string) (`""`)
- `default` (nullable of type `T`) (`null`)

#### `AnimationToRunParams`

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

- `colors` (list(int)) (`listOf()`)

#### `DegreesRotation`

- `xRotation` (double) (`0.0`)
- `yRotation` (double) (`0.0`)
- `zRotation` (double) (`0.0`)
- `rotationOrder` (list(string)) (`listOf("ROTATE_Z", "ROTATE_X"`)

#### `Equation`

- `coefficients` (list(int)) (`listOf()`)

#### `Location`

- `x` (double) (`0.0`)
- `y` (double) (`0.0`)
- `z` (double) (`0.0`)

#### `PreparedColorContainer`

- `colors` (list(int))
- `originalColors` (list(int))

#### `RadiansRotation`

- `xRotation` (double) (`0.0`)
- `yRotation` (double) (`0.0`)
- `zRotation` (double) (`0.0`)
- `rotationOrder` (list(string)) (`listOf("ROTATE_Z", "ROTATE_X"`)

#### `RunningAnimationParams`

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

- `name` (string) (`""`)
- `pixels` (list(int)) (`listOf()`)
- `parentSectionName` (string) (`""`)

### HTTP Endpoints

#### GET Endpoints

- `/animation/{name}` (`getAnimationInfo`, requires one string parameter) (returns `AnimationInfo`)
- `/animations/names` (`getSupportedAnimationNames`) (returns list(string))
- `/animations` (`getSupportedAnimations`) (returns list(`AnimationInfo`))
- `/animations/map` (`getSupportedAnimationsMap`) (returns map(string to `AnimationInfo`))
- `/running` (`getRunningAnimations`) (returns map(string to `RunningAnimationParams`))
- `/running/ids` (`getRunningAnimationsIds`) (returns list(string))
- `/running/{id}` (`getRunningAnimationParams`, requires one string parameter) (returns `RunningAnimationParams`)
- `/sections` (`getSections`) (returns list(`Section`))
- `/sections/map` (`getSectionsMap`) (returns map(string to `Section`))
- `/section/{name}` (`getSection`, requires one string parameter) (returns `Section`)
- `/strip/info` (`getStripInfo`) (returns `StripInfo`)
- `/strip/color` (`getCurrentStripColor`) (returns list(int))

##### Additional Functions

- `getFullStripSection` (calls `getSection` with `"fullStrip"`)

#### POST Endpoints

- `/sections` (`createNewSection`, requires one `Section` parameter) (returns `Section`)
- `/start` (`startAnimation`, requires one `AnimationToRunParams` parameter) (returns `RunningAnimationParams`)
- `/strip/clear` (`clearStrip`) (no return)

#### DELETE Endpoints

- `/running/{id}` (`endAnimation`, requires one string parameter) (returns `RunningAnimationParams`)

##### Additional Functions

- `endAnimation` or `endAnimationFromParams`, requiring one `RunningAnimationParams` parameter (calls `endAnimation` with `param.id`)
