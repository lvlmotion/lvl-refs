---
title: Installing and Updating
parent: LEVEL Collector for Windows
description: installing the Collector, the Python setup for Polar, Sony and Vicon, updates, and getting help
nav_order: 1
---

# Installing and Updating

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

## Getting help

- The **Help** tab links here and has quick tools (the Sony control box
  address, the clock page used to check camera timing).
- On the **Logs** tab, **Copy all** puts the whole log on the clipboard so you
  can paste it into an email to [info@lvlmotion.com](mailto:info@lvlmotion.com).
  The full log of each run is also saved under `LEVEL_Sensor\logs` in your user
  folder.
