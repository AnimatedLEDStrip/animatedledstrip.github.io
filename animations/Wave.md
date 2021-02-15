---
title: Wave
parent: Animations
---

<!-- THIS FILE IS AUTOMATICALLY GENERATED -->
<!-- MAKE CHANGES TO THE AnimationInfo INSTANCE ASSOCIATED WITH THIS ANIMATION -->

# Wave

## Animation Info

|Quality|Value|
|:-:|:-:|
|name|Wave|
|abbr|WAV|
|runCount default|Endless|
|minimum colors|1|
|unlimited colors|false|
|dimensionality|ONE_DIMENSIONAL, TWO_DIMENSIONAL, THREE_DIMENSIONAL|

|Parameter|Type|Default Value|Description|
|:-:|:-:|:-:|:-:|
|interMovementDelay|Int|30|Delay between movements in the animation|
|interAnimationDelay|Int|500|Time between start of one animation and start of the next|
|movementPerIteration|Double|1.0|How far to move during each iteration of the animation|
|rotation|Rotation|RadiansRotation(xRotation=0.0, yRotation=0.0, zRotation=0.0, rotationOrder=[ROTATE_Z, ROTATE_X])|Rotation of the plane around the XYZ axes|

## Description
Wipes a plane through all pixels, leaving a fading trail behind.

Note: Two-dimensional operation requires plane to be rotated around the X axis (probably by Pi/2 radians in most use cases)
