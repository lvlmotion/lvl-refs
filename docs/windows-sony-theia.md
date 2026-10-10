---
title: Sony Cameras and Theia
parent: LEVEL Collector for Windows
description: starting Sony cameras from the recorder, timecode audio (LTC), pulling and aligning clips, Theia
nav_order: 5
---

# Sony Cameras and Theia

## How it connects

- The PC joins the cameras' network and talks to the Sony **camera control
  boxes** (one per camera; the first one is the master, usually
  `http://169.254.200.200`). The recorder starts and stops every camera and reads
  each camera's state.
- For the tightest timing, the recorder plays a **timecode audio signal (LTC)**
  from a PC audio output into **one camera's microphone input**. That camera's
  clip then carries PC time in its audio.
- Every camera also stamps its video with **timecode**, so the other cameras'
  clips line up with the LTC camera.

## Settings in the recorder

- **Settings > Sync:** tick **Sony** and choose who starts the cameras (usually
  the recorder). Needs the Python setup (see [Overview](desktop-recorder.html#python-setup-needed-for-polar-sony-vicon-and-plotting)).
- **Settings > Sony:** the control box address; the **LTC output** (press
  **Refresh outputs**, then pick the output cabled to the camera); the LTC level.
- **Recorder > Sony section:**
  - **Get Browser Key** (takes control of the cameras), **Link Date/Time** (sets
    the cameras' clocks from the PC), **Unmute and set to 50%** (the LTC output's
    volume), **Play LTC signal**. **Scan All** does the first three for you.
  - The camera list, named as in the Sony webapp (e.g. `001  DSC-RX0M2_3177801`),
    with each camera's state. Pick the **LTC** camera: the one with the LTC cable.
  - **Rig details** (folded) shows the full control-box status when something
    is wrong.

<!-- screenshot: Sony section - action buttons and camera rows with the LTC camera picked -->

**Close the Sony webapp's browser tab before recording.** While it is open it
holds the control box and the recorder's start/stop is ignored.

## Settings on the other system

On the **Sony webapp**: all cameras present, timecode sync on.

On the **LTC camera** (the camera menu, Movie settings):

- **Audio Recording: On.** (Theia's usual camera setup turns audio off, which
  removes the LTC.)
- **Audio Rec Level: manual, about 26 of 30.** Automatic level spoils the signal.
- **Audio Level Display** is optional; it shows the meters so you can see LTC
  arriving.
- Plugging the LTC cable into the microphone jack turns off that camera's own
  microphone.

Use a **USB audio adapter** for the LTC output. A PC's built-in headphone jack
can cut out after a couple of seconds when a camera is plugged in, even though
it works with headphones.

## Calibration

**Check the LTC once per setup:**

1. Tick **Play LTC signal**, pick the LTC camera, record a 30-second take.
2. **Postproc > Last Session > Pull Sony Clip + Align.**
3. The clip check should say **LTC decoded**. "Silent" means no LTC reached the
   camera: check Play LTC was on, the picked camera is the cabled one, Audio
   Recording is on, and the audio output. "Clipping" means turn the LTC level
   down.

**Optional visual check:** **Help > Open clock page** shows a large PC clock.
Film it with a camera for a few seconds at the start and end of a session; the
clock in the video should match the aligned time.

<!-- screenshot: Postproc after Pull Sony Clip + Align, clip check "LTC decoded" -->

## Post-processing

**Pull Sony Clip + Align** (Postproc tab, after a take):

- Copies the LTC camera's clip for that take into the session folder.
- Checks its timecode and LTC.
- Writes an `aligned` folder: each sensor's data on the video's timeline,
  `sync_map.json` (camera time to PC time), and `theia_timestamps.csv` (for every
  video frame: its timecode and its PC time).

Clips from the other cameras: copy them with the Sony webapp's **Import**. They
share timecode with the LTC camera, so `sync_map.json` applies to them too.
Without LTC, alignment uses timecode only (to about one frame).

### Theia

Theia processes the clips into a motion file (C3D) on the cameras' timecode.
The goal is to bring it onto the PC clock like everything else: pull the Sony
clips (timecode and LTC) and Theia's processed C3D, and re-time the C3D onto
the PC clock. **Automatic re-timing of the C3D is coming and not available
yet.** Until then, use `theia_timestamps.csv` to look up the PC time of any
Theia frame by its frame number or timecode.

## Files

| File | When | What |
|---|---|---|
| `sony-anchor.json`, `sony-events.csv` | at Stop | when the start and stop were sent and confirmed, on the PC clock |
| `<camera>_<clip>.MP4` | after Pull | the LTC camera's clip |
| `aligned\...` | after Align | aligned sensor files, `sync_map.json`, `theia_timestamps.csv` |
