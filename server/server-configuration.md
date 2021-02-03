---
title: Server Configuration
parent: Server
---

# Server Configuration

The AnimatedLEDStrip server can be configured via the command line and/or with a config file.

## Command Line Options

- `--log-level [error|warn|info|debug|verbose]` - Set the minimum severity level for logs that will be printed
- `-f, --config FILE` - Specify a config to load instead of `/etc/leds/led.config`
- `--persist` - Persist animations across restarts
- `--nopersist` - Don't persist animations across restarts (overrides --persist and persist=true in config)
- `-n, --numleds NUM` - Specify number of LEDs in the strip (default `240`)
- `-P, --pin PIN` - Specify the pin number the LED strip is connected to (default `12`)
- `--render-delay DELAY` - Specify the time in milliseconds between renders of the LED strip (default `10`)
- `--log-renders` - Enable strip color logging
- `--log-file` - Specify the output file name for strip color logging
- `--log-render-count` - Specify number of renders between saves to log file (default `1000`)
- `-1, --1d` - Support one-dimensional animations
- `--no1d` - Don't support one-dimensional animations
- `-2, --2d` - Support two-dimensional animations
- `--no2d` - Don't support two-dimensional animations
- `-3, --3d` - Support three-dimensional animations
- `--no3d` - Don't support three-dimensional animations

## `led.config` Options

Command line arguments always take priority over the config file.

## `log-level`

The minimum severity level for logs can be set using `log-level=[error|warn|info|debug|verbose]`.

### `persist`

The server will persist animations across restarts if persist is set to true using `persist=true`.
The default is `false`.

### `numLEDs`

The number of LEDs in the strip can be set using `numLEDs=#`.
The default is `240` LEDs.

### `pin`

The pin can be set using `pin=#`.
The default is pin `12`.

### `render-delay`

The time in milliseconds between renders of the LED strip can be set with `render-delay=#`.
The default is `10` milliseconds.

### `log-renders`

Enable strip color logging with `log-renders=true`.

### `log-file`

The output file name for strip color logging can be set with `log-file=name`.

### `log-render-count`

The number of renders between saves to log file can be set using `log-render-count=#`.
The default is `1000` renders.

### `1d`

One-dimensional animation support can be enabled with `1d=true`.
The default is `true`.

### `2d`

Two-dimensional animation support can be enabled with `2d=true`.
The default is `false`.

### `3d`

Three-dimensional animation support can be enabled with `3d=true`.
The default is `false`.
