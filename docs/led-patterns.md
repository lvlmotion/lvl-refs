---
title: LED Light Patterns
description: what each colour and blink pattern on a sensor means
---

# LED Light Patterns

Each sensor has a single multi-colour LED that shows what the device is doing.
The colour tells you the state; the pattern (solid, breathing, blinking, or
flashing) tells you the mode within that state.

## Quick reference

| What the sensor is doing        | Colour            | Pattern                                  |
|---------------------------------|-------------------|------------------------------------------|
| Powering on                     | White             | Solid, briefly                           |
| Waiting to connect              | Green             | Breathing (smooth fade up and down)      |
| Connected, not recording        | Green             | Solid                                    |
| Recording (streaming data)      | Yellow            | Blinking (short on, longer off)          |
| Low battery, not recording      | Yellow with red   | Yellow, then a short red flash, repeating|
| Low battery, recording          | Dark with red     | Off, then a short red flash, repeating   |
| Charging                        | Red               | Solid                                    |
| Charge complete                 | Green             | Solid                                    |
| Error                           | Red               | Solid                                    |
| Off                             | No light          | -                                        |

## Pattern details

**Breathing** means the light fades smoothly up and down over roughly a
four second cycle. You see this while the sensor is powered on and waiting to
connect (or after it disconnects and returns to waiting).

**Blinking (recording)** is a distinct on/off rhythm: the light is on for about
0.4 seconds, then off for about 0.9 seconds, repeating on a roughly 1.3 second
cycle. This is the pattern to look for to confirm a sensor is actively recording.
When several sensors record together, their blinks are time-aligned so they pulse
in unison.

**Solid** means steady, constant light with no change. Used for connected,
charging, charge complete, and error.

**Low battery flash** overlays a short red flash on the current state. When the
sensor is not recording, you see the normal colour for about 0.9 seconds followed
by a red flash for about 0.2 seconds. When the sensor is recording, the light
stays off for about 0.9 seconds between red flashes so the recording rhythm is
still visible. Charge the sensor when you see this.

## Notes

- **Red appears in three situations:** charging, error, and the low-battery flash.
  Context tells them apart. A steady solid red while on a charger means charging;
  a steady solid red off the charger means the device has hit an error; a brief
  red flash mixed with another colour or with darkness means low battery.
- **Colours can be customised.** The default recording colour is yellow and the
  default idle/connected colour is green. These can be changed per sensor from the
  app, so a deployment may use different colours than the defaults listed here.
- **No light at all** means the sensor is off or the battery is fully depleted.
