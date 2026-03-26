# Changelog

## 2026.3.5

- Fix: control switches no longer turn on lights unconditionally. 

## 2026.3.4

- Fix: correct lights going on after a sensor goes from unvailable to on after restart ;
- Fix: correct handling of doors on restart.

## 2026.3.3

- Startup trigger: after Home Assistant restarts and sensors become available again, wait the configured turn-off delay then turn off lights if no sensor is active. Prevents lights from staying on after a reboot.
- Code reorg.

## 2026.3.2

- Multiple control entities: all selected switches must be on for the automation to work ;
- Optional luminosity sensors with threshold: if multiple sensors are selected, the average value is used ;
- Night only: lights turn on only when the sun is below the horizon ;
- Luminosity override : an entity that bypasses the luminosity check when on (e.g. a night mode switch or schedule) ;
- Settings reorganized.

## 2026.3.1

- Different default behaviour for binary entities : if it's door or opening, lights go on when open, but can go off when they stay open. Only motion sensor going off will turn the lights off.
- Can be deactivated using a new parameter (then, there should be now movement AND all doors should be closed to turn the lights off).

## 2026.3

- Initial release.
