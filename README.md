# Auto Lights Blueprint

Automatically turn lights on and off based on binary sensors (motion sensors, door sensors, etc.), with an optional control switch to enable or disable the automation.

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
| **Control switch** | An `input_boolean` to enable/disable the automation | No | — |

## How it works

1. When any selected sensor becomes active (motion detected, door opened, etc.), the lights turn on.
2. When all sensors become inactive, the blueprint waits for the configured delay before turning off the lights.
3. If a sensor becomes active again during the delay, the timer resets and the lights stay on.
4. If a **control switch** is configured:
   - When the switch is **on**, the automation works normally.
   - When the switch is **off**, the automation stops responding to sensors.
   - When the switch is turned **on** again, the automation resumes immediately: if any sensor is currently active, the lights turn on.

## Known limitations

- The turn-off delay applies equally to all sensor types. If you mix motion sensors (where a delay is useful) with door sensors (where you might want instant off), you may need separate automations.
