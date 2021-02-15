---
title: Animation Utility Functions
nav_order: 1
parent: Defining a New Animation
grand_parent: Core
---

# Animation Utility Functions

## Subanimation Creation

These functions are used by animations to start subanimations.

### `runParallel`

Takes one `SubAnimationToRunParams` parameter and starts a new animation in the specified `CoroutineScope`, returning without waiting for the animation to complete.

### `runParallelAndJoin`

Takes multiple `SubAnimationToRunParams` parameters and starts new animations with [`runParallel`](#runparallel) in the specified `CoroutineScopes`, then waits for all animations to finish before returning.

### `runSequential`

Takes one `SubAnimationToRunParams` parameter and starts a new animation in the specified `CoroutineScope`, waiting for the animation to complete before returning.

## Pixel Grouping




