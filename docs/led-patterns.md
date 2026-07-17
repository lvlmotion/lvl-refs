---
title: LED Light Patterns
description: what each colour and blink pattern on a sensor means
nav_order: 5
---

# LED Light Patterns

Each sensor has a single multi-colour LED that shows what the device is doing.
The colour tells you the broad state; the pattern (solid, breathing, or
blinking) tells you the mode within that state.

## Quick reference

| What the sensor is doing        | Colour            | Pattern                                  |
|---------------------------------|-------------------|------------------------------------------|
| Powering on                     | White             | Solid, briefly                           |
| Waiting to connect              | Green             | Breathing (smooth fade up and down)      |
| Connected, not recording        | Green             | Solid                                    |
| Recording (streaming data)      | Green             | Blinking (short on, longer off)          |
| Charging                        | Red               | Solid                                    |
| Charge complete                 | Green             | Solid                                    |
| Error                           | Red               | Solid                                    |
| Off                             | No light          | -                                        |

## Pattern details

**Breathing** means the light fades smoothly up and down. You see this while the
sensor is powered on and waiting to connect (or after it disconnects and returns
to waiting).

**Blinking (recording)** is a distinct on/off rhythm. This is the pattern to
look for to confirm a sensor is actively recording.

**Solid** means steady, constant light with no change. Used for connected,
charging, charge complete, and the brief power-on and error states.

## Notes

- **Green is the normal colour, and pattern tells the state apart.** Waiting to
  connect breathes, connected is solid, and recording blinks - all green. If
  the light is green and steady the sensor is connected and ready; if it is
  green and blinking it is recording.
- **Red means charging or an error.** A steady red while on a charger means
  charging; a steady red off the charger means the device has hit an error.
- **Solid green can mean two things.** Off the charger it means connected and
  ready; on the charger it means charging is complete.
- **Colours can be customised.** The sensor colour (used for both the connected
  and recording states) can be changed per sensor from the app, so a deployment
  may use a different colour than the green default described here.
- **No light at all** means the sensor is off or the battery is fully depleted.
- **Battery level is not shown on the LED.** Check the sensor's battery level in
  the app rather than on the device.
