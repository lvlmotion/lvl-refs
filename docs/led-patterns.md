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
| Idle, waiting for connection    | User Define       | Breathing (smooth fade up and down)      |
| Connected, not recording        | User Define       | Solid                                    |
| Recording (streaming data)      | User Define       | Blinking (short on, longer off)          |
| Error                           | Red               | Solid                                    |
| Deep sleep                      | No light          | -                                        |

## Pattern details

**Breathing** means the light fades smoothly up and down. You see this while the
sensor is powered on and waiting to connect (or after it disconnects and returns
to waiting).

**Blinking (recording)** is a distinct on/off rhythm. This is the pattern to
look for to confirm a sensor is actively recording.

**Solid** means steady, constant light with no change. Used for connected,
charging, charge complete, and the brief power-on and error states.

## Notes

- **Colours can be customised.** The sensor colour (used for both the connected
  and recording states) can be changed per sensor from the app, so a deployment
  may use a different colour than the green default described here.
- **No light at all** means the sensor is off or the battery is fully depleted.