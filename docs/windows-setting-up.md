---
title: Setting Up for a Recording
parent: LEVEL Collector for Windows
description: turning on the systems you use, getting them ready on the Collect tab, and reading the status sidebar
nav_order: 2
---

# Setting Up for a Recording

<!-- screenshot: Collect tab, sensors connected, all four systems in the sidebar -->

## Turn on the systems you are using

**Settings > Sync** lists every system. Tick the ones you use (Polar H10, Sony,
Vicon) and keep the **Collector** as the one that starts a take (the master):
**Start Stream** on the Collector starts everything.

<!-- screenshot: Settings > Sync table with Polar, Sony and Vicon on, Collector as master -->

## Get everything ready

1. Prepare each system as its page describes:
   [LEVEL Sensors](windows-level-sensors.html), [Polar H10](windows-polar-h10.html),
   [Sony Cameras and Theia](windows-sony-theia.html), [Vicon](windows-vicon.html).
2. On the **Collect** tab, press **Scan All** (top of the window). It finds or
   readies every system you turned on. Each system has its own section on the
   tab; pick what you want in each.
3. Press **Connect All**. Some systems take a moment to get ready after
   connecting; each system's page says what to expect.

**Settings > On launch** can do the scanning and connecting for you when the
Collector opens.

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
| Collector | - | whether the LEVEL Hub is plugged in |
| LEVEL | the sensors you picked | connected / time-synced / streaming with elapsed time and loss |
| Polar | the strap you picked | searching, warming up, then live ECG / ACC / heart rate |
| Sony | the camera carrying the LTC timecode audio | cameras ready / recording / problems |
| Vicon | Nexus | frames arriving during a take; grey between takes |

Nothing here stops you recording except a missing LEVEL Hub (the button then
reads **Awaiting LEVEL Hub**). If a line is red, it is your call whether to record
anyway.

## If something goes wrong

- **Collector says "no LEVEL Hub detected":** re-plug the LEVEL Hub, then press
  **Re-scan for Hub**.
- **A system's card is red:** its page has the fixes for that system.
- **A system drops out during a take:** its card turns red and says so. The other
  systems keep recording; press **Stop Stream** when you decide to end the take.
