---
title: LEVEL Collector for Windows
description: LEVEL Collector for Windows - what it does, installing it, and keeping it up to date
nav_order: 4
has_children: true
---

# LEVEL Collector for Windows

LEVEL Collector for Windows is the Windows app (separate from the phone app) for lab and
clinic PCs. It records **LEVEL Inez sensors** through the **LEVEL Hub** plugged
into the PC, and runs up to three other systems alongside them:

- **Polar H10** chest strap (ECG, accelerometer, heart rate)
- **Sony cameras** (and Theia markerless motion capture from their video)
- **Vicon** motion capture (Nexus, including force plates on the Vicon system)

## How everything lines up

Every stream is placed on **one clock: the PC's clock**. Each system gets there a
different way, described under "How it connects" on its page
([LEVEL Sensors](windows-level-sensors.html), [Polar H10](windows-polar-h10.html),
[Sony Cameras and Theia](windows-sony-theia.html), [Vicon](windows-vicon.html)),
and the Collector saves what each needs during the take. Post-processing then
turns those records into files that all share the PC clock, so a moment in one
stream can be found in every other.

## Installing

1. Ask for the installer by email at [info@lvlmotion.com](mailto:info@lvlmotion.com).
2. Run `LEVEL_Sensor-<version>.exe`. It installs for your Windows user only, so
   it does not need administrator rights.
3. Open it from the Start menu (**LvlMotion > LEVEL_Sensor**). It opens with or
   without the LEVEL Hub plugged in.

### Python setup (needed for Polar, Sony, Vicon and plotting)

Skip this only if you record LEVEL sensors and nothing else.

1. Open the **Settings** tab and click **Set Up Python Environment**.
2. Wait for the **Logs** tab to say it finished. The first run needs internet. It
   builds a private Python for the Collector and installs everything the other
   systems need (including the video tools used to read Sony clips), without
   changing anything else on the computer.
3. If it says no Python 3.10 or newer was found, install Python from
   [python.org](https://www.python.org/downloads/) and click the button again.

Every time the Collector starts, the **Logs** tab lists what it found: the
computer, the Bluetooth adapter, the LEVEL Hub port, the networks, and a
**PASS / NOT FOUND** line for each Python package. If something is missing,
run **Set Up Python Environment** again and restart the Collector.

## Updating

- New versions come as a new installer (by email). Run it over the old one: it
  upgrades in place and **keeps your settings, recordings and Python setup**.
- The window title and the first line of the **Logs** tab show the version.
- A version can only be installed over an **older** one. If Windows refuses,
  uninstall the old version first (Settings > Apps); your settings and
  recordings are kept.

## The pages in this guide

- [Connecting Sensors](windows-connecting-sensors.html) - the Collect tab and the status sidebar
- [Running a Recording](running-a-recording.html) - a take with every system, and how time alignment works
- [LEVEL Sensors](windows-level-sensors.html) - sensor settings, time sync and files
- [Polar H10](windows-polar-h10.html) - pairing, picking the strap, warm-up, files
- [Sony Cameras and Theia](windows-sony-theia.html) - camera control, LTC timecode audio, pulling and aligning clips
- [Vicon](windows-vicon.html) - Nexus triggering, frame timing, force plates

## Getting help

- The **Help** tab links here and has quick tools (the Sony control box
  address, the clock page used to check camera timing).
- On the **Logs** tab, **Copy all** puts the whole log on the clipboard so you
  can paste it into an email to [info@lvlmotion.com](mailto:info@lvlmotion.com).
  The full log of each run is also saved under `LEVEL_Sensor\logs` in your user
  folder.
