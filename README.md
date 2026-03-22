# Auto Lights Blueprint

Automatically turn lights on and off based on binary sensors (motion sensors, door sensors, etc.), with optional lighting conditions and control switches.

[Lire en français](README.fr.md)

## Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fnicolinuxfr%2Fauto-lights-blueprint%2Fgh-pages%2Fen%2Fauto_lights.yaml)

Or copy this URL manually:

```
https://raw.githubusercontent.com/nicolinuxfr/auto-lights-blueprint/gh-pages/en/auto_lights.yaml
```

## Configuration

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| **Lights** | The lights to control automatically | Yes | — |
| **Sensors** | Binary sensors that trigger the lights (motion, door/window, etc.) | Yes | — |
| **Turn off delay** | Time to wait before turning off the lights after a sensor becomes inactive | No | 00:02:00 |

### Lighting conditions

| Input | Description | Default |
|-------|-------------|---------|
| **Night only** | Only turn on lights when the sun is below the horizon | Off |
| **Luminosity sensors** | Illuminance sensors to check before turning on (average is used if multiple) | — |
| **Luminosity threshold** | Lights turn on only if average luminosity is below this value | 30 lx |

### Advanced settings

| Input | Description | Default |
|-------|-------------|---------|
| **Keep lights on with open doors** | Open door/window sensors prevent lights from turning off | Off |
| **Control switches** | `input_boolean` entities that enable/disable the automation (all must be on) | — |

## How it works

1. When any selected sensor becomes active (motion detected, door opened, etc.), the lights turn on.
2. When all sensors become inactive, the blueprint waits for the configured delay before turning off the lights.
3. If a sensor becomes active again during the delay, the timer resets and the lights stay on.
4. By default, open door/window sensors do not prevent the lights from turning off — only motion/presence sensors are checked.

### Lighting conditions

The lighting conditions only affect **turning on** the lights. Turning off always works regardless of sun or luminosity.

- **Night only**: lights turn on only when the sun is below the horizon, using the built-in Home Assistant `sun.sun` entity.
- **Luminosity sensors + threshold**: lights turn on only when the average luminosity is below the threshold.
- **Both enabled**: lights turn on if **either** condition is met (night OR low luminosity).
- **Neither enabled**: lights always turn on when a sensor triggers.

### Control switches

If one or more **control switches** are configured, all of them must be on for the automation to work. When any switch is turned off, the lights turn off after the configured delay. When all switches are back on, the automation resumes immediately.
