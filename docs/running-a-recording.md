---
title: Running a Recording
parent: LEVEL Collector for Windows
description: a take with sensors, Polar, Sony and Vicon together, and how the streams are lined up on one clock
nav_order: 2
---

# Running a Recording

## Turn on the systems you are using

**Settings > Sync** lists every system. Tick the ones you use (Polar H10, Sony,
Vicon) and keep the **Collector** as the one that starts a take (the master):
**Start Stream** on the Collector starts everything. Each system's
own setup is on its page: [LEVEL Sensors](windows-level-sensors.html),
[Polar H10](windows-polar-h10.html), [Sony Cameras and Theia](windows-sony-theia.html),
[Vicon](windows-vicon.html).

<!-- screenshot: Settings > Sync table with Polar, Sony and Vicon on, Collector as master -->

## A take, step by step

1. **Scan All** (top of the window). It finds or readies every system you turned
   on. Pick what you want in each section.
2. **Connect All.** Some systems take a moment to get ready after connecting;
   each system's page says what to expect.
3. Check the **status sidebar**: start when everything you need is green or
   yellow.
4. Type a **Trial Name** (it names the session folder) and any **Notes**.
5. Press **Start Stream**. The Collector starts every system you turned on
   together.
6. Press **Stop Stream**. Everything stops; the sensors stay connected for the
   next take.

<!-- screenshot: footer with Trial Name, Notes and Start Stream; sidebar all green while recording -->


If a system fails mid-take, its sidebar card turns red and the others keep
going. Stop when you are ready. If the cameras are still recording when no take
is running, the main button still reads **Stop Stream** and stops them.

## Where the files go

Each take is a folder under `LEVEL_Sensor\data\` in your user folder, named
`<date>_<time>-<trial name>`:

| Written | Files |
|---|---|
| During the take | one sensor file per sensor; Polar ECG, accelerometer and heart-rate files |
| At Stop | session details and quality summary; the Sony and Vicon timing records |
| After post-processing | the pulled camera clip and an `aligned` folder |

What each system writes is listed on its page.
