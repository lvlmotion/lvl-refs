---
title: Connecting Sensors
parent: LEVEL Collector for Windows
description: the Collect tab, the status sidebar colours, and what the sensor lights mean
nav_order: 1
---

# Connecting Sensors

<!-- screenshot: Collect tab, sensors connected, all four systems in the sidebar -->

## Before you start

- Charge the sensors (see [About Sensors](about-sensors.html)). Pick one up to
  wake it: an asleep sensor has no light and will not be found.
- Plug the **LEVEL Hub** into the PC. A direct USB port is better than a hub.

## Connect

1. On the **Collect** tab, press **Scan** (or **Scan All** at the top, which also
   readies the Polar strap and Sony cameras). Found sensors are listed. The
   sensors from your last recording are ticked for you.
2. Tick or untick sensors as needed.
3. Set **Rate** and **Batch**: look up your number of sensors and rate in
   [Rate and batch](windows-level-sensors.html#rate-and-batch).
4. Press **Connect** (or **Connect All**). Each sensor's light goes solid and its
   row shows **Connected**.

**Settings > On launch** can do this for you when the Collector opens: **Scan**
lists the sensors, **Connect** also connects them (turning Connect on turns Scan
on).

<!-- screenshot: IMU card with Scan / Connect / Rate / Batch and the sensor table -->

## The sensor table

| Column | What it shows |
|---|---|
| LED | the sensor's colour (click to change) |
| MAC | the 4-character ID printed on the sensor |
| Location | where it is worn (click to set) |
| Battery | charge level; recharge at LOW |
| Status | Found / Connecting / Connected / Streaming |
| Sync | **B** = the time beacon, **S** = following it, then its offset from the beacon in ms. A red **✗** means the sensor is not time-synced: disconnect and reconnect it. A red **⚠** with a number means it drifted off the beacon during the take. |
| Packet Loss | data lost on the way to the PC; red above 0.1% |
| Rows | samples written this take |

## The status sidebar

The right-hand panel shows every system you have turned on, and how each is
doing. Each card reads **name - what you picked**, then a coloured status line,
then any warnings.

<!-- screenshot: status sidebar with a red, yellow, green and grey line -->

| Colour | Meaning |
|---|---|
| Green | ready, or recording and healthy |
| Yellow | warming up, in progress, or recording with a warning |
| Red | not ready or failed |
| Grey | nothing to report (e.g. Vicon between takes) |

While a take is recording, the dot beside each system that is recording
blinks, at the same pace as a LEVEL sensor's light. The bar along the bottom of
the window takes the colour of the worst system.

| Card | Shows after the dash | Status line |
|---|---|---|
| SRD (the Collector itself) | - | whether the LEVEL Hub (dongle) is plugged in |
| LEVEL | the sensors you picked | connected / time-synced / streaming with elapsed time and loss |
| Polar | the strap you picked | searching, warming up, then live ECG / ACC / heart rate |
| Sony | the camera carrying the LTC timecode audio | cameras ready / recording / problems |
| Vicon | Nexus | frames arriving during a take; grey between takes |

Nothing here stops you recording except a missing LEVEL Hub (the button then
reads **Awaiting Dongle** - the Collector calls the LEVEL Hub the dongle). If a line is red, it is your call whether to record
anyway.

## Sensor lights

| What the sensor is doing | Colour | Pattern |
|---|---|---|
| Waiting to connect | sensor colour | breathing (fades up and down) |
| Connected, not recording | sensor colour | solid |
| Recording | sensor colour | blinking |
| Error | red | solid |
| Asleep / battery empty | none | - |

More detail on the lights, waking and resetting: [About Sensors](about-sensors.html).

## If something goes wrong

- **No sensors found:** wake them (pick them up), then Scan again. Sensors held by
  a phone or another computer do not show; disconnect them there first.
- **SRD says "no dongle detected":** re-plug the LEVEL Hub, then press **Re-scan for Dongle**.
- **A sensor shows a red ✗ in Sync:** press Disconnect, then Connect again.
- **During a take the sensors drop out:** the LEVEL card turns red and says so.
  Polar, Sony and Vicon keep recording; press **Stop** when you decide to end the
  take.
