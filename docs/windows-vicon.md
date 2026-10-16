---
title: Vicon
parent: LEVEL Collector for Windows
description: starting Nexus from the Collector (or the reverse), Vicon frame timing, force plates
nav_order: 9
---

# Vicon

## How it connects

- **Start and stop** travel over the network as Nexus's remote-trigger messages
  (UDP port 30 by default): the Collector starts and stops Nexus.
- **Frame timing:** while Nexus captures, the Collector reads Vicon's live data
  stream and saves every Vicon frame number with the PC time it arrived. That
  places anything Nexus records on its own frames (markers, force plates) on the
  PC clock.
- **Force plates** wired into the Vicon system are recorded by Nexus, on Vicon's
  frames.

## Before you start

You need:

- a Vicon system with **Nexus 2** calibrated and capturing as your lab normally
  does, with the Collector PC on the same network as the Nexus PC (or Nexus on
  the Collector PC itself);
- the **Vicon DataStream SDK** installed on the Collector PC (free from
  [vicon.com](https://www.vicon.com/software/datastream-sdk/); the default
  folder is `C:\Program Files\Vicon\DataStream SDK\Win64\Python\vicon_dssdk`);
- the Collector with the **full** Python environment (see
  [Settings](windows-settings.html#python-interpreter)).

We assume you already run captures in Nexus on your own: camera calibration,
subjects and force plates are Vicon's business, see
[Vicon Help](https://help.vicon.com/). The only Nexus settings this page adds
are the ones that let the Collector start and read a capture, in Nexus's
**Capture Tools** pane (Vicon's description:
[Capture tools, Nexus 2.16](https://vicon-help.atlassian.net/wiki/spaces/Nexus216/pages/11602304/Capture+tools)):

- **Start/Stop over network** (called **Start/Stop on remote trigger** in older
  Nexus): on, set to **receive**, on the same UDP port as the Collector (30).
- Press **Arm** before the first take, and **Lock** so Nexus stays armed after
  each capture stops.
- Nexus in **Live** mode with the cameras running. The frame timing only flows
  while Nexus streams live data.
- Force plates enabled and zeroed before each take.

## How to connect

1. **Settings > Sync:** tick **Vicon**, with the Collector as master.
2. **Settings > Vicon:** the UDP port (match Nexus), the Nexus PC's address if
   Nexus runs on another computer (**Scan For IP** finds it), and the DataStream
   SDK folder.
3. On the **Collect** tab, **Scan All** then **Connect All** as for the sensors.
   The Vicon panel shows whether the trigger is armed and the live stream is
   reachable.

## Calibration

None for the link itself. Calibrate Vicon and take a static trial as your lab
normally does. Then do a short test take: the Vicon card in the sidebar should
turn **green** with frames arriving (about the Vicon frame rate).

<p style="color:#FF3B30;font-size:1.3em"><strong>TODO SCREENSHOT: Vicon panel in the Collect tab, connected (green), before Start Stream</strong></p>

## How to stream

**Start Stream** starts Nexus and **Stop Stream** stops it. Nexus uses the
Collector's trial name. Grey on the Vicon card between takes is normal: Nexus
gives no "ready" signal, only frames while it captures.

## Files generated

| File | What |
|---|---|
| `vicon-anchor.json` | trial name and the PC time of the start trigger |
| `timestamps-vicon.csv` | timestamps only: Vicon frame and PC time |
| `bridge.log` | log of the live-data reader (send it to us if frames are missing) |
| `aligned\vicon_frames_pc.csv` | after Align: every Vicon frame with its PC time |

Marker and force-plate data come from your Nexus export as usual (C3D or CSV);
keep the trial name so it matches the session folder.

## Post-processing

Align writes to `aligned\<session>\` beside `data\` in the root folder; the raw
session folder is never changed.

- `timestamps-vicon.csv` lists every Vicon frame with the PC time it arrived
  (timestamps only; marker data comes from your Nexus export).
- **Postproc > Align to PC clock** fits a line through those arrivals and writes
  `aligned\vicon_frames_pc.csv`: every Vicon frame with its PC time. If a Nexus
  C3D is in the session folder, its frame range is covered too. Use it to place
  any Nexus export (C3D, force plates) on the PC clock by frame number.

## FAQs

**Start Stream does nothing in Nexus.** Nexus is not armed, or the port or
network interface differs. Check **Start/Stop over network** is on, receiving,
on port 30, and press **Arm**. **Lock** keeps it armed for the next take.

**The Vicon card stays grey during a take.** Nexus is capturing but the live
stream is not reaching the Collector: Nexus must be in Live mode, and the
Nexus host address in **Settings > Vicon** must be right when Nexus is on
another PC.

**Frames are missing in `timestamps-vicon.csv`.** Send us `bridge.log` from the
session folder.

**Can Nexus start the take instead?** Yes: in **Settings > Sync** make Vicon the
master and set Nexus to **send**. The Collector then follows Nexus's trigger
and ticking **Arm This Session** on the Collect tab makes it listen.
