---
title: Core
nav_order: 2
has_children: true
---

# AnimatedLEDStrip Core Library

The AnimatedLEDStrip core library handles:

- Changing the pixels' colors
- Tracking the location in 3D space of each pixel (even for 1- and 2-dimensional arrangements)
- Running animations on the LEDs, including running multiple animations simultaneously
- Specifying how these animations can be customized
- Creating sections of the strip that can be controlled as if they were an independent strip

## Structure

The core functionality of the library revolves around the `LEDStrip` class.
This class manages instances of other classes that manage various aspects of the strip, such as:

- Communicating with the LEDs ([`LEDStripRenderer`](#communicating-with-the-leds))
- Starting and stopping animations ([`LEDStripAnimationManager`](#starting-and-stopping-animations))
- Tracking the color of each pixel (`LEDStripColorManager`)
- Logging the color of each pixel if render logging is enabled (`LEDStripColorLogger`)
- Tracking the location of each pixel in 3D space (`PixelLocationManager`)
- Creating and tracking sections of the strip (`LEDStripSectionManager`)

## Communicating with the LEDs

The `LEDStripRenderer` uses a `NativeLEDStrip` defined by a [device library](/devices) for communicating with the strip.

## Starting and Stopping Animations

The `LEDStripAnimationManager` class implements the `AnimationManager` interface.
This interface denotes that the class is able to start and stop animations.

When the `LEDStripAnimationManager` is created, it determines which animations it is capable of supporting, based on the dimensions listed as supported in the `StripInfo` class and based on the dimensions the animation reports it is able to work in.
It then adds these animations to two maps, one mapping the animation's name to the animation and one mapping the animation's abbreviation to the animation.
The name and abbreviation are converted to lowercase and all whitespace, brackets, parentheses, hyphens and underscores are removed.
This allows multiple versions of the name to be used to identify the same animation.

A specific animation supported by the `LEDStripAnimationManager` can be found with the `findAnimation` and `findAnimationOrNull` commands.

When an animation is started with the `startAnimation` function, it uses an `AnimationToRunParams` instance to determine what animation to run and how to configure it.
A custom ID can be passed, otherwise a number between 0 and 99999999 will be chosen at random.
A `RunningAnimation` instance is created and returned.
(The `RunningAnimation` instance is what actually runs the animation)

An animation can be stopped by calling the `endAnimation` function with the ID that identifies that animation.
This will cancel the coroutine associated with the animation, which will cancel any child coroutines and animations.

### How Animations are Run

The running of a specific animation is handled by a `RunningAnimation` instance.
The `RunningAnimation` instance is given a set of parameters that define how to run the animation (as a `RunningAnimationParams`, which was created based on the `AnimationToRunParams` passed to the `AnimationManager`).
It is also given a `CoroutineScope` to run the animation in, a section to run the animation on, a reference to the `AnimationManager` instance that created it, and is told if it is a top-level animation.

A top-level animation is created by the `LEDStripAnimationManager`.
A non-top-level animation is created by a `RunningAnimation` as part of the animation it is running.

The `RunningAnimation` creates a new Coroutine to run the animation in, and then starts the animation.
The animation will be run repeatedly until either the coroutine is stopped, or the `runs` counter exceeds the number of runs specified by the parameters (the `runCount` parameter).
A negative `runCount` will tell the animation to run the default number of times, as specified in the [animation info](/core/new-animations#animationinfo).

### How Animations are Defined

See [Defining a New Animation](/core/new-animation)

