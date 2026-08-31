---
title: First install
parent: Desktop recorder
description: step-by-step first-time setup of the desktop recorder, with optional sync sections
nav_order: 1
---

# First install: the desktop recorder

A step-by-step first-time setup. Do **Part 1** on every machine. The sync parts
(2b onward) are **optional** - only do the one you actually use, and each says
exactly where to click. This is a working draft and will be tidied up.

## Part 1 - Install and open (everyone)

1. Run the installer, `LEVEL_Sensor-<version>.exe`. A newer installer upgrades an
   existing install in place - no need to uninstall first.
2. Launch it. It opens with or without the sensor dongle plugged in.
3. Plug in the dongle, go to the **Recorder** tab, and press **Scan**. Your
   sensors appear; press **Stream** to record. That is all you need for plain IMU
   recording.

## Part 2a - Set up Python (do this if you use ANY sync feature or plotting)

Skip this only if you record IMU sensors and nothing else.

1. Open the **Settings** tab.
2. Under **Python Interpreter**, click **Set Up Python Environment**.
3. Wait for the log to say it finished (first run needs internet). It builds an
   isolated Python and installs what the sync features need, leaving the rest of
   your computer untouched.
4. If it says no Python 3.10+ was found, install one from python.org and click the
   button again.

## Part 2b - Vicon (optional: only if you trigger Vicon/Nexus)

Vicon and the app talk over the network by UDP start/stop trigger packets. Both
sides must use the **same UDP port**, and Nexus must have remote/UDP triggering
enabled (Nexus's remote-trigger setup, so it either broadcasts start/stop or
listens for them). Then pick who leads.

Common to both directions, in **Settings -> Sync Sources**:

1. Turn **Vicon** on.
2. Set the **Vicon UDP port** to match Nexus.
3. Set the **Vicon SDK path** to your DataStream SDK's Python folder (default
   `C:/Program Files/Vicon/DataStream SDK/Win64/Python/vicon_dssdk`). This is only
   needed to pull mocap frames into the aligned output, not to trigger.

### Vicon as master - "start on remote trigger" (Nexus leads, app auto-captures)

You start the capture in Nexus; the app hears it and records automatically.

1. Under **mode**, choose **Vicon as master**.
2. In Nexus, enable its remote trigger to **send** UDP start/stop on that port.
3. On the **Recorder** tab, in the **Sync** panel, tick **Arm This Session (Listen
   For Nexus Trigger)** (or leave auto-arm on).
4. Start/stop the capture in Nexus - the app starts and stops with it, per trial,
   and matches the trial name.

### App as master - "start/stop over network" (app leads, Nexus follows)

You press Stream in the app; it sends the start/stop to Nexus.

1. Under **mode**, choose **App as master**, and set the **Nexus host** if Nexus
   is on another PC.
2. In Nexus, set it to **receive** remote triggers and arm it to capture on that
   port.
3. On the **Recorder** tab, press **Stream** to send START (Nexus begins), and
   **Stop** to send STOP.

Either way, the **Sync** panel shows the wiring and where to press. Do a shared
hop at the start of each trial to confirm alignment later.

## Part 2c - Sony cameras (optional: only if you trigger Sony/Theia)

In **Settings -> Sync Sources**:

1. Turn **Sony** on.
2. Set the **Sony base URL** (the CCB address).
3. Choose the **mode**: *App as master* (the app fires the cameras) or *Sony
   webapp as master* (you start on the Sony webapp, the app follows).

On the **Recorder** tab, in the **Sync** panel, click **Get Browser Key** to
confirm the rig is reachable before recording. If you want sub-frame LTC sync,
tick **Play LTC signal** there too.

## Part 2d - Sync relay, no IMU (optional: Sony starts Vicon, e.g. force plates)

Use this to make a Sony recording start a Vicon capture with no sensors - e.g. to
line up force plates (on Vicon's sync) with the cameras.

1. Do Part 2b steps 2-3 and Part 2c step 2 (the app needs the Vicon port + Sony
   URL), but you do **not** need sensors or the dongle.
2. In **Settings -> Sync Sources**, at the top, find **Sync relay (no IMU): Sony
   -> Vicon** and click **Start relay**.
3. Record from the Sony console. The app detects the start and fires Nexus.

## Part 2e - Polar H10 (optional: heart-rate / ECG)

1. Pair the H10 in **Windows Bluetooth settings** first, and wear the strap (a dry
   strap will not stream).
2. In **Settings -> Sync Sources**, turn **Polar / H10** on.

## Reading the Sync panel

On the Recorder page the **Sync** panel draws your current setup as a small
diagram - who starts a capture, which way each trigger runs, and where to press,
with IMU on its own line. It updates as you change master/slave or arm the relay.
Check it matches what you intend before recording.

For the fixed offsets and calibration between systems (Polar, Vicon, Sony/K_av),
see [Syncing with other systems](syncing-with-other-systems.html).
