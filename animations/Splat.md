---
title: Splat
parent: Animations
---

<!-- THIS FILE IS AUTOMATICALLY GENERATED -->
<!-- MAKE CHANGES TO THE AnimationInfo INSTANCE ASSOCIATED WITH THIS ANIMATION -->

# Splat

## Animation Info

|Quality|Value|
|:-:|:-:|
|name|Splat|
|abbr|SPT|
|runCount default|1|
|minimum colors|1|
|unlimited colors|false|
|dimensionality|ONE_DIMENSIONAL, TWO_DIMENSIONAL, THREE_DIMENSIONAL|

|Parameter|Type|Default Value|Description|
|:-:|:-:|:-:|:-:|
|interMovementDelay|Int|15|Delay between movements in the animation|
|movementPerIteration|Double|10.0|How far to move during each iteration of the animation|
|center|Location|Center of all pixels|The center of the splat|
|distance|Distance|100.0%, 100.0%, 100.0%|How far the splat should reach|

## Description
Similar to a [Ripple](Ripple) but the pixels don't fade back.
Runs two Wipe animations in opposite directions starting from `center`, stopping after traveling `distance` or at the end of the section, whichever comes first.
