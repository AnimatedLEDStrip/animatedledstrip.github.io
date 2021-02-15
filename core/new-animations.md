---
title: Defining a New Animation
nav_order: 1
parent: Core
has_children: true
---

# Creating a New Animation

Animations come in two forms: Defined Animations and Animation Groups.
[Defined Animations](#defined-animations) are single animations that modify the LED strip or run specific sub-animations.
[Animation Groups](#animation-groups) are a list of animations that will be run together, either in a specific order or randomized.
Defined Animations and Animation Groups built-in to the library are located in the `animations.predefined` and `animations.predefinedgroups` packages, respectively.

## `AnimationInfo`

All animations have a corresponding `AnimationInfo` instance with details about that animation.
These details include:
- `name` - The name used to identify the animation. Capitalization, spaces, underscores, hyphens, and parenthesis are removed before trying to identify the animation
- `abbr` - An abbreviated version of the name that also identifies the animation. This can technically be anything but the precedent is for it to be three capital letters
- `description` - A description of the animation, which is used to when creating the wiki page about this animation
- `runCountDefault` - The number of times this animation should be run if not otherwise specified. A negative number will make the animation run until it is manually stopped
- `minimumColors` - How many [colors](/core/colors) your animation requires, at a minimum
- `unlimitedColors` - Whether your animation can handle more than the minimum number of colors you require. Animations like this include [Alternate](Alternate) and [Fireworks](Fireworks)
- `dimensionality` - This specifies what dimensions your animation works in. This is a set of `Dimensionality`s, which you can create using `Dimensionality.oneDimensional` or `Dimensionality.anyDimensional`, among others. Examples of one-dimensional animations include [Bounce](Bounce) or [Cat Toy](Cat-Toy). Examples of animations that work in all dimensions include [Alternate](Alternate), [Ripple](Ripple) and [Sparkle](Sparkle).
- `intParams` - A list of [integer parameters](#animation-specific-parameters) that your animation will use
- `doubleParams` - A list of [double parameters](#animation-specific-parameters) that your animation will use
- `stringParams` - A list of [string parameters](#animation-specific-parameters) that your animation will use
- `locationParams` - A list of [`Location` parameters](#animation-specific-parameters) that your animation will use
- `distanceParams` - A list of [`Distance` parameters](#animation-specific-parameters) that your animation will use
- `rotationParams` - A list of [`Rotation` parameters](#animation-specific-parameters) that your animation will use
- `equationParams` - A list of [`Equation` parameters](#animation-specific-parameters) that your animation will use

### Animation-Specific Parameters

Animation-specific parameters come in seven types: `Int`, `Double`, `String`, `Location`, `Distance`, `Rotation`, and `Equation`.
To specify a parameter that can be modified, such as the delay between movements or the rotation of a plane, you add an `AnimationParameter` to the appropriate parameter list.
An `AnimationParameter` requires a name, which will be used to identify the parameter, a description, which will be used to when creating the wiki page about this animation, and can take an optional default value to use if the parameter is not set.

```kotlin
AnimationParameter("paramName", "Param description", default)
```

### Example `AnimationInfo`

```kotlin
Animation.AnimationInfo(
    name = "Fireworks",
    abbr = "FWK",
    description = "Runs [Ripple](Ripple) animations from random center points within the defined " +
                  "locations of all pixels, travelling a predefined distance.\n" +
                  "Color is chosen randomly from `colors`.",
    runCountDefault = -1,
    minimumColors = 1,
    unlimitedColors = true,
    dimensionality = Dimensionality.anyDimensional,
    intParams = listOf(AnimationParameter("interMovementDelay",
                                          "Delay between movements in the ripple animation",
                                          30),
                       AnimationParameter("interAnimationDelay",
                                          "Time between start of one animation and start of the next",
                                          500)),
    doubleParams = listOf(AnimationParameter("movementPerIteration",
                                             "How far to move during each iteration of the animation",
                                             1.0)),
    distanceParams = listOf(AnimationParameter("distance",
                                               "Distance each firework should travel",
                                               PercentDistance(0.1, 0.1, 0.1))),
)
```

## Animation Parameter Types

There are seven different types for animation parameters, but only three are types that are part of the language (`Int`, `Double`, `String`).
The other four are specially created for animations.
These include:
- `Location`
- `Distance`
- `Rotation`
- `Equation`

### `Location`

A location is a point in three-dimensional space, taking three `Double` arguments for the x, y, and z coordinates.
The distance between two `Location`s can be calculated using the `Location.distanceFrom(other: Location)` function.

### `Distance`

A distance is a set of three values, specifying how far an animation should travel in the x, y, and z directions.
There are two types of distances, `AbsoluteDistance`s and `PercentDistance`s
An `AbsoluteDistance` is a distance with the exact distance in each direction.
A `PercentDistance` is a distance that specifies a percentage of the full distance covered by LEDs in that direction that should be traveled (`100.0` represents the full distance).
All `PercentDistance`s are converted to `AbsoluteDistance`s when the parameters for an animation are being prepared.

### `Rotation`

A rotation is a set of three values, specifying how far to rotate points around the x, y, and z axes, plus a list of `RotationAxis`es that specify what order to perform the rotations.
There are two types of rotations, `RadiansRotation`s and `DegreesRotation`s.
All `DegreesRotation`s are converted to `RadiansRotation`s when the parameters for an animation are being prepared, because the `sin` and `cos` functions use radians.

### `Equation`

An `Equation` parameter specifies coefficients for x in an equation.
Each coefficient corresponds to the term with the degree equal to its index in the coefficients list.
For example, `Equation(5.0, 3.3, 1.3, 0.0, 2.4)` represents the equation `2.4x^4 + 1.3x^2 + 3.3x + 5.0`.
Animations such as [Pixel Run](Pixel-Run) use this to determine what line the pixel will follow.

## Defined Animations

A defined animation is an animation that modifies the LED strip or runs specific sub-animations.
Examples include [Sparkle](Sparkle), which modifies the strip directly, or [Cat Toy](Cat-Toy), which runs [Pixel Run](Pixel-Run) animations between specific start and end points.

Any definition of a `DefinedAnimation` requires two parts, an [`AnimationInfo` instance](#animationinfo), and a lambda with the actual animation logic that will be run.

This lambda is passed three arguments: an `AnimationManager` instance, which is handling the running of that animation, a `RunningAnimationParams` instance, with the parameters for the animation, and a `CoroutineScope` instance, in case the animation starts subanimations or child coroutines that aren't full animations (e.g. [Sparkle](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/blob/master/src/commonMain/kotlin/animatedledstrip/animations/predefined/sparkle.kt)).
This scope should be used for all child coroutines because it allows the full animation to be canceled all at once by [canceling the parent coroutine](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-job/index.html) that created the `CoroutineScope`.

### Example Defined Animation

```kotlin
val sparkle = DefinedAnimation(
    Animation.AnimationInfo(
        name = "Sparkle",
        abbr = "SPK",
        description = "Each LED is changed to `colors[0]` for `sparkleDuration` milliseconds " +
                      "before reverting.\n" +
                      "A separate coroutine is created for each pixel.\n" +
                      "Each coroutine waits up to `maxDelayBeforeSparkle` milliseconds before " +
                      "sparkling its pixel.",
        runCountDefault = -1,
        minimumColors = 1,
        unlimitedColors = false,
        dimensionality = Dimensionality.anyDimensional,
        intParams = listOf(AnimationParameter("sparkleDuration", "Length of sparkle", 50),
                           AnimationParameter("maxDelayBeforeSparkle",
                                              "Maximum amount of time before a pixel will sparkle",
                                              5000)),
    )
) { leds, params, scope ->
    val color = params.colors[0]
    val sparkleDuration = params.intParams.getValue("sparkleDuration").toLong()
    val maxDelayBeforeSparkle = params.intParams.getValue("maxDelayBeforeSparkle")

    leds.apply {
        validIndices.map { n ->
            scope.launch {
                delay((randomDouble() * maxDelayBeforeSparkle).toLong())
                yield() // don't set color if the animation was cancelled during the delay
                setPixelAndRevertAfterDelay(n, color, sparkleDuration)
            }
        }.joinAll()
    }
}
```

### Animation Utility Functions

There are a multitude of functions available to simplify the creation of new animations.
See [Animation Utils](core/animation-utils/animation-utils) and [Pixel Grouping](core/animation-utils/pixel-grouping) for more details.

## Animation Groups

An Animation Group is a list of animations that can be run one after the other.
The difference between an animation group like [Sorting Animations](Sorting-Animations) and a defined animation like [Cat Toy](Cat-Toy) is that the former is simply a list of animation names that can be run one after the other, while the latter has a lambda defined that performs calculations and runs specific animations at specific times and places.

An animation group can come in one of two types, ordered or randomized.
This is determined by the `GroupType`.

An animation group is created by creating a `NewAnimationGroupInfo` that contains information about the group, the `GroupType`, and the list of animations.
When the animation group is prepared, it will take all the parameters that are requested by the animations listed and add them to its own requested parameters, with suffixes denoting which parameters are used by which animation.
It also adds `postAnimationDelay` and `animationDuration` parameters for each animation.
It can also have its own parameters in addition to those of the listed animations.

If the `animationDuration` parameter for the specific animation is set to a non-negative value, then the animation will be run in a [`withTimeoutOrNull`](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/with-timeout-or-null.html) block that will cancel the animation if it doesn't complete before the timeout expires.

### Example Animation Group

```kotlin
val sortingAnimations = RandomizedAnimationGroup(
    groupInfo = Animation.AnimationInfo(name = "Sorting",
                                        abbr = "SRT",
                                        description = "Runs all of the sorting animations currently defined.",
                                        runCountDefault = -1,
                                        minimumColors = 1,
                                        unlimitedColors = false,
                                        dimensionality = Dimensionality.oneDimensional),
    animationList = listOf("Bubble Sort",
                           "Heap Sort",
                           "Merge Sort Parallel",
                           "Merge Sort Sequential",
                           "Quick Sort Parallel",
                           "Quick Sort Sequential"),
)
```

## Adding a New Animation

There are two places to create new animations.
One is to add them in the main method of your server, using the `addNewAnimation()` or `addNewGroup()` functions on the `LEDStrip` that you just created.
This is especially good for testing new animations before they are added to the library.
The other option is to add them as a predefined animation or animation group in the library.

### Adding a New Animation to the AnimatedLEDStrip Library

Adding a new animation to the library has a few steps.

- Create a file in either [`animations/predefined`](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/tree/master/src/commonMain/kotlin/animatedledstrip/animations/predefined) (if creating a `DefinedAnimation`) or [`animations/predefinedgroups`](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/tree/master/src/commonMain/kotlin/animatedledstrip/animations/predefinedgroups) (if creating an animation group). This file should be named with the name of the animation in snake case
- Create a `val` with your animation
- Add your animation to the `predefinedAnimations` list or `predefinedGroups` list in [`DefineAnimations.kt`](https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/blob/master/src/commonMain/kotlin/animatedledstrip/animations/DefineAnimations.kt) (depending on if it is an animation or a group). This is done so all animations can be found when the `LEDStripAnimationManager` needs them. The lists are separate so the animations the groups need are defined before the group needs information about them.
