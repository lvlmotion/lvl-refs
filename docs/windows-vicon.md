---
title: Vicon
parent: LEVEL Collector for Windows
description: starting Nexus from the Collector (or the reverse), Vicon frame timing, force plates
nav_order: 6
---

# Vicon

## How it connects

- **Start and stop** travel over the network as Nexus's remote-trigger messages
  (UDP port 30 by default). Either the Collector starts Nexus, or Nexus starts
  the Collector.
- **Frame timing:** while Nexus captures, the Collector reads Vicon's live data
  stream and saves every Vicon frame number with the PC time it arrived. That
  places anything Nexus records on its own frames (markers, force plates) on the
  PC clock.
- **Force plates** wired into the Vicon system are recorded by Nexus, on Vicon's
  frames.

## Settings in the Collector

- **Settings > Sync:** tick **Vicon** and choose who starts a take:
  - **Collector as master:** **Start Stream** starts Nexus and **Stop** stops it.
    Nexus uses the Collector's trial name.
  - **Vicon as master:** you start the capture in Nexus; the Collector follows.
    Tick **Arm This Session** in the Collect tab's Vicon section.
- **Settings > Vicon:** the UDP port (match Nexus), the Nexus PC's address if
  Nexus runs on another computer, and the Vicon DataStream SDK folder (default
  `C:\Program Files\Vicon\DataStream SDK\Win64\Python\vicon_dssdk`). Needs the
  Python setup (see [Overview](desktop-recorder.html#python-setup-needed-for-polar-sony-vicon-and-plotting)).

## Settings on the other system

In **Nexus**:

- Remote trigger on, on the same UDP port: **receive** triggers (Collector as
  master) or **send** them (Vicon as master).
- Nexus in **Live** mode with the cameras running. The frame timing only flows
  while Nexus streams live data.
- Force plates enabled and zeroed before each take.

## Calibration

- Calibrate Vicon and take a static trial as your lab normally does.
- Do a short test take: the Vicon card in the sidebar should turn **green** with
  frames arriving (about the Vicon frame rate). Grey between takes is normal;
  Nexus gives no "ready" signal.
- Hops at the start and end of each take show in the markers, the force plates
  and the sensors: a quick check that everything lines up.

## Post-processing

- `timestamps-vicon.csv` lists every Vicon frame with the PC time it arrived
  (timestamps only; marker data comes from your Nexus export).
- **Postproc > Align to PC clock** fits a line through those arrivals and writes
  `aligned\vicon_frames_pc.csv`: every Vicon frame with its PC time. If a Nexus
  C3D is in the session folder, its frame range is covered too. Use it to place
  any Nexus export (C3D, force plates) on the PC clock by frame number.
- Export from Nexus as usual (C3D or CSV); keep the trial name so it matches the
  session folder.

## Files

| File | What |
|---|---|
| `vicon-anchor.json` | trial name and the PC time of the start trigger |
| `timestamps-vicon.csv` | timestamps only: Vicon frame and PC time |
| `bridge.log` | log of the live-data reader (send it to us if frames are missing) |
| `aligned\vicon_frames_pc.csv` | after Align: every Vicon frame with its PC time |
