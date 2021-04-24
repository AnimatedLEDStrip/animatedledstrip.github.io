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
{: .fs-5 }

|Parameter|Type    |Default|
|:-------:|:------:|:-----:|
|`x`      |`Double`|`0.0`  |
|`y`      |`Double`|`0.0`  |
|`z`      |`Double`|`0.0`  |

#### `AnimationInfo`
{: .fs-5 }

|Parameter        |Type                                                        |Default   |
|:---------------:|:----------------------------------------------------------:|:--------:|
|`name`           |`String`                                                    |`""`      |
|`abbr`           |`String`                                                    |`""`      |
|`description`    |`String`                                                    |`""`      |
|`runCountDefault`|`Int`                                                       |`0`       |
|`minimumColors`  |`Int`                                                       |`0`       |
|`unlimitedColors`|`Boolean`                                                   |`false`   |
|`dimensionality` |`Set<String>`                                               |`setOf()` |
|`intParams`      |`List<AnimationParameter<Int>>`                             |`listOf()`|
|`doubleParams`   |`List<AnimationParameter<Double>>`                          |`listOf()`|
|`stringParams`   |`List<AnimationParameter<String>>`                          |`listOf()`|
|`locationParams` |`List<AnimationParameter<Location>>`                        |`listOf()`|
|`distanceParams` |`List<AnimationParameter<AbsoluteDistance/PercentDistance>>`|`listOf()`|
|`rotationParams` |`List<AnimationParameter<DegreesRotation/RadiansRotation>>` |`listOf()`|
|`equationParams` |`List<AnimationParameter<Equation>>`                        |`listOf()`|

#### `AnimationParameter<T>`
{: .fs-5 }

|Parameter    |Type    |Default|
|:-----------:|:------:|:-----:|
|`name`       |`String`|`""`   |
|`description`|`String`|`""`   |
|`default`    |`T?`    |`null` |

#### `AnimationToRunParams`
{: .fs-5 }

|Parameter       |Type                                           |Default   |
|:--------------:|:---------------------------------------------:|:--------:|
|`animation`     |`String`                                       |`""`      |
|`colors`        |`List<ColorContainer/PreparedColorContainer>`  |`listOf()`|
|`id`            |`String`                                       |`""`      |
|`section`       |`String`                                       |`""`      |
|`runCount`      |`Int`                                          |`0`       |
|`intParams`     |`Map<String, Int>`                             |`mapOf()` |
|`doubleParams`  |`Map<String, Double>`                          |`mapOf()` |
|`stringParams`  |`Map<String, String>`                          |`mapOf()` |
|`locationParams`|`Map<String, Location>`                        |`mapOf()` |
|`distanceParams`|`Map<String, AbsoluteDistance/PercentDistance>`|`mapOf()` |
|`rotationParams`|`Map<String, DegreesRotation/RadiansRotation>` |`mapOf()` |
|`equationParams`|`Map<String, Equation>`                        |`mapOf()` |

#### `ColorContainer`
{: .fs-5 }

|Parameter|Type       |Default   |
|:-------:|:---------:|:--------:|
|`colors` |`List<Int>`|`listOf()`|

#### `DegreesRotation`
{: .fs-5 }

|Parameter      |Type          |Default                        |
|:-------------:|:------------:|:-----------------------------:|
|`xRotation`    |`Double`      |`0.0`                          |
|`yRotation`    |`Double`      |`0.0`                          |
|`zRotation`    |`Double`      |`0.0`                          |
|`rotationOrder`|`List<String>`|`listOf("ROTATE_Z", "ROTATE_X"`|

#### `Equation`
{: .fs-5 }

|Parameter     |Type       |Default   |
|:------------:|:---------:|:--------:|
|`coefficients`|`List<Int>`|`listOf()`|

#### `Location`
{: .fs-5 }

|Parameter|Type    |Default|
|:-------:|:------:|:-----:|
|`x`      |`Double`|`0.0`  |
|`y`      |`Double`|`0.0`  |
|`z`      |`Double`|`0.0`  |

#### `PreparedColorContainer`
{: .fs-5 }

|Parameter       |Type       |
|:--------------:|:---------:|
|`colors`        |`List<int>`|
|`originalColors`|`List<int>`|

#### `RadiansRotation`
{: .fs-5 }

|Parameter      |Type          |Default                         |
|:-------------:|:------------:|:------------------------------:|
|`xRotation`    |`Double`      |`0.0`                           |
|`yRotation`    |`Double`      |`0.0`                           |
|`zRotation`    |`Double`      |`0.0`                           |
|`rotationOrder`|`List<String>`|`listOf("ROTATE_Z", "ROTATE_X")`|

#### `RunningAnimationParams`
{: .fs-5 }

|Parameter       |Type                           |Default  |
|:--------------:|:-----------------------------:|:-------:|
|`animationName` |`String`                       |`""`     |
|`colors`        |`List<PreparedColorContainer>` |         |
|`id`            |`String`                       |`""`     |
|`section`       |`String`                       |`""`     |
|`runCount`      |`Int`                          |`0`      |
|`intParams`     |`Map<String, Int>`             |`mapOf()`|
|`doubleParams`  |`Map<String, Double>`          |`mapOf()`|
|`stringParams`  |`Map<String, String>`          |`mapOf()`|
|`locationParams`|`Map<String, Location>`        |`mapOf()`|
|`distanceParams`|`Map<String, AbsoluteDistance>`|`mapOf()`|
|`rotationParams`|`Map<String, RadiansRotation>` |`mapOf()`|
|`equationParams`|`Map<String, Equation>`        |`mapOf()`|
|`sourceParams`  |`AnimationToRunParams`         |         |

#### `StripInfo`
{: .fs-5 }

|Parameter               |Type            |Default   |
|:----------------------:|:--------------:|:--------:|
|`numLEDs`               |`Int`           |`0`       |
|`pin`                   |`Int?`          |`null`    |
|`renderDelay`           |`Int`           |`10`      |
|`isRenderLoggingEnabled`|`Boolean`       |`false`   |
|`renderLogFile`         |`String`        |`""`      |
|`rendersBetweenLogSaves`|`Int`           |`1000`    |
|`is1DSupported`         |`Boolean`       |`true`    |
|`is2DSupported`         |`Boolean`       |`false`   |
|`is3DSupported`         |`Boolean`       |`false`   |
|`ledLocations`          |`List<Location>`|`listOf()`|

#### `Section`
{: .fs-5 }

|Parameter          |Type       |Default   |
|:-----------------:|:---------:|:--------:|
|`name`             |`String`   |`""`      |
|`pixels`           |`List<Int>`|`listOf()`|
|`parentSectionName`|`String`   |`""`      |

### HTTP Endpoints

|Method|Endpoint              |Function                     |Parameter              |Return                               |
|:-----|:--------------------:|:---------------------------:|:---------------------:|:-----------------------------------:|
|GET   |`/animation/{name}`   |`getAnimationInfo`           |`String`               |`AnimationInfo`                      |
|GET   |`/animations`         |`getSupportedAnimations`     |                       |`list<AnimationInfo>`                |
|GET   |`/animations/map`     |`getSupportedAnimationsMap`  |                       |`Map<String, AnimationInfo>`         |
|GET   |`/animations/names`   |`getSupportedAnimationsNames`|                       |`List<String>`                       |
|POST  |`/animations/newGroup`|`createNewGroup`             |`NewAnimationGroupInfo`|`AnimationInfo`                      |
|GET   |`/running`            |`getRunningAnimations`       |                       |`Map<String, RunningAnimationParams>`|
|GET   |`/running/ids`        |`getRunningAnimationsIds`    |                       |`List<String>`                       |
|GET   |`/running/{id}`       |`getRunningAnimationParams`  |`String`               |`RunningAnimationParams`             |
|DELETE|`/running/{id}`       |`endAnimation`               |`String`               |`RunningAnimationParams`             |
|GET   |`/section/{name}`     |`getSection`                 |`String`               |`Section`                            |
|GET   |`/sections`           |`getSections`                |                       |`List<Section>`                      |
|POST  |`/sections`           |`createNewSection`           |`Section`              |`Section`                            |
|GET   |`/sections/map`       |`getSectionsMap`             |                       |`Map<String, Section>`               |
|POST  |`/start`              |`startAnimation`             |`AnimationToRunParams` |`RunningAnimationParams`             |
|POST  |`/strip/clear`        |`clearStrip`                 |                       |`void`                               |
|GET   |`/strip/color`        |`getCurrentStripColor`       |                       |`List<int>`                          |
|GET   |`/strip/info`         |`getStripInfo`               |                       |`StripInfo`                          |

##### Additional Functions
{: .text-grey-lt-100 }

|Function                                  |Parameter               |Operation                            |
|:----------------------------------------:|:----------------------:|:-----------------------------------:|
|`endAnimation` or `endAnimationFromParams`|`RunningAnimationParams`|calls `endAnimation` with `param.id` |
|`getFullStripSection`                     |                        |calls `getSection` with `"fullStrip"`|
