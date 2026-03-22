# Changelog

## 2026.03.2

The sophisticated edition.

- Multiple control entities: all selected switches must be on for the automation to work ;
- Optional luminosity sensors with threshold: if multiple sensors are selected, the average value is used ;
- Night only: lights turn on only when the sun is below the horizon ;
- Luminosity override : an entity that bypasses the luminosity check when on (e.g. a night mode switch or schedule) ;
- Settings reorganized.

## 2026.03.1

The door edition.

- Different default behaviour for binary entities : if it's door or opening, lights go on when open, but can go off when they stay open. Only motion sensor going off will turn the lights off.
- Can be deactivated using a new parameter (then, there should be now movement AND all doors should be closed to turn the lights off).

## 2026.03

- Initial release.
