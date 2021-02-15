---
title: Pixel Grouping
nav_order: 2
parent: Defining a New Animation
grand_parent: Core
---

# Pixel Grouping

Pixel Grouping is how an animation pre-calculates which pixels will be changed on each iteration of the animation.
This allows these calculations to be done before the animation starts, reducing lag during the animation.

## How it Works

Pixels are grouped based on a characteristic, which is determined by which function you use.
The lists of grouped pixels are returned as a `PixelModificationLists` instance.

### `PixelModificationLists`

A `PixelModificationLists` instance contains a list of `PixelsToModify` instances, one per iteration of the animation.

### `PixelsToModify`

A `PixelsToModify` instance contains five lists that tell the animation what pixels to set and revert during this iteration:

- `allSetPixels` - All pixels that should be set during this iteration
- `allRevertPixels` - All pixels that should be reverted during this iteration
- `pairedSetRevertPixels` - A list of paired up pixels from the set and revert lists (used by animations like Runway lights so pixels are set and reverted at nearly the exact same time instead of setting all and then reverting all)
- `unpairedSetPixels` - A list with any remaining pixels that should be set that are not included in `pairedSetRevertPixels` (due to `allRevertPixels` being smaller than `allSetPixels`)
- `unpairedRevertPixels` - A list with any remaining pixels that should be reverted that are not included in `pairedSetRevertPixels` (due to `allSetPixels` being smaller than `allRevertPixels`)

## Functions

There are currently four pixel grouping functions:

- [Group by X location](#grouppixelsbyxlocation)
- Group by distance from a central point
- Group along a line
- Group along a line in spaced groups
