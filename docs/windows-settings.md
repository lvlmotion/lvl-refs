---
title: Settings
parent: LEVEL Collector for Windows
description: the Settings tab - Collector settings (root folder, on launch, Python), the sync table (who starts a take), and the per-system settings
nav_order: 2
---

# Settings

The **Settings** tab is a stack of panels, each with a title you can click to
fold it away: **Collector Settings**, **Sync**, then one
panel for each other system that is on.

![Settings tab: Collector Settings with the root folder, On launch switches and the Python interpreter](assets/windows-settings/collector-settings.png)
<p style="color:#FF3B30;font-size:1.3em"><strong>RETAKE SCREENSHOT: root folder `C:\lvlmotion` with the Recordings go to / settings stay in line; no LEVEL Sensors / Time Sync panel; no personal user paths</strong></p>

## Collector Settings

### Root folder

Where new recordings go. The Collector keeps its data in the root folder's
`collector` folder: each take in `collector\data`, and beside it `logs`,
`aligned` (post-processed takes), `calibration`, `sony` (pulled clips),
`support` and `images`. The default root folder is `C:\lvlmotion`, so takes
land in `C:\lvlmotion\collector\data\`. Type a path and press Enter, or
**Browse**. A folder not named `lvlmotion` gets one inside it: picking `D:\`
gives `D:\lvlmotion`. The line under the box shows where recordings now go.

A new root folder applies at once, to new takes only: existing recordings stay
where they are and are not moved. It cannot be changed while a take is
recording, or while a scan, connect, start or stop is under way.

The settings themselves and the Python environment always stay in
`C:\lvlmotion\settings`, whatever the root folder. Every Windows account on
the PC shares them and the data.

### On launch

Two switches, **Scan All** and **Connect All**: the Collector presses Scan All,
and then Connect All, for you as soon as it opens. Connect uses the sensors and
strap of your last recording, so it needs the LEVEL Hub plugged in and the
sensors awake at launch.

### Python interpreter

The Collector uses Python for plotting and for the Polar, Sony and Vicon
connections. Recording LEVEL sensors needs no Python.

**Path to Python** is the Python the Collector uses. At launch the Collector
fills it in with the Python it finds on the computer; type a path and press
Enter, or **Browse**, to pick a different one. At launch the Collector looks
for Python 3.10 to 3.13; a Python you pick yourself can be 3.10 or newer, but
Vicon does not work with 3.14 or newer. The line
under the path says which Python was found, and **Packages in this
environment** lists each package the Collector needs as present or missing. If
your Python already has them, nothing more is needed. Otherwise click one of:

- **Set up minimum environment**: what plotting needs.
- **Set up full environment**: everything the other systems need, including
  the video tools used to read Sony clips.

Either one builds a private Python environment, with its own Python 3.12, in
the Collector's settings folder (`C:\lvlmotion\settings`, shared by every
account on the PC), installs the packages
there, and switches the Collector to it. You do not need Python installed
first, but the first setup needs an internet connection. Your own Python is
never modified. The full environment download can take several minutes.

If a package later shows as missing, run the same button again and restart the
Collector.

## Sync

![Sync table with Polar H10, Sony and Vicon on and the Collector as master](assets/windows-settings/sync-table.png)
<p style="color:#FF3B30;font-size:1.3em"><strong>RETAKE SCREENSHOT: crop out the removed LEVEL Sensors / Time Sync panel above the table</strong></p>

One take, several systems, one clock: the sync table says which systems are in
the capture and which one starts a take (the **master**). The Collector relays
the start to the others.

| Column | Meaning |
|---|---|
| **On** | the system is part of the capture. The Collector is always on. |
| **Master** | the one system whose start begins the take. Only one can be master. |
| **Role** | what that setting means for the row, in words. |
| **Last connected** | what that system connected to last: the sensors of the last recording, the Polar strap, the LTC camera. **Scan + connect last** reconnects the sensors and the strap. |

| System | Can be master | As master | Otherwise |
|---|---|---|---|
| **Collector** | yes | **Start Stream** starts the take and records the LEVEL sensors | relays the master's start, records the LEVEL sensors |
| **Polar H10** | no | - | an ECG stream, started with the take |
| **Sony** | yes | the camera web app leads; the Collector follows | the Collector fires the cameras |
| **Vicon** | yes | Nexus leads; the Collector follows | the Collector fires Nexus |

Keep the **Collector** as master unless the other system has to lead for its
own reasons (each system's page says when). The table locks while a take is
armed or recording; stop or disarm it to change the table.

Turning a system on adds its panel below the table. The per-system pages
describe each one:

- **Polar H10**: nothing to set here; the strap is picked on the Collect tab,
  see [Polar H10](windows-polar-h10).
- **Sony**: the control box address, the Sony video folder (where the clips
  and Theia trial folders live; blank means `sony` in the root folder) and the
  auto-get-key option on the left; the LTC output device, gain and calibration
  (with the history of past calibrations) on the right, see
  [Sony Cameras and Theia](windows-sony-theia).

  ![Sony panel in Settings: control box address, Sony video folder and the auto-get-key option on the left; LTC output, gain and Calibrate LTC on the right](assets/windows-settings/sony-panel.png)
- **Vicon**: auto-arm, the DataStream SDK path and the Nexus session folder
  (normally left blank) on the left; the UDP port and the Nexus host on the
  right, see [Vicon](windows-vicon).
