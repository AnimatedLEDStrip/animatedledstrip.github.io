---
title: Subanimation Functions
nav_order: 2
parent: Defining a New Animation
grand_parent: Core
---

# Subanimation Creation

These functions are used by animations to start subanimations.

## `runParallel`

Takes one `SubAnimationToRunParams` parameter and starts a new animation in the specified `CoroutineScope`, returning without waiting for the animation to complete.

## `runParallelAndJoin`

Takes multiple `SubAnimationToRunParams` parameters and starts new animations with [`runParallel`](#runparallel) in the specified `CoroutineScopes`, then waits for all animations to finish before returning.

## `runSequential`

Takes one `SubAnimationToRunParams` parameter and starts a new animation in the specified `CoroutineScope`, waiting for the animation to complete before returning.
