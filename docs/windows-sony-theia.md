---
title: Sony Cameras and Theia
parent: LEVEL Collector for Windows
description: starting Sony cameras from the Collector, timecode audio (LTC), the control box clock, aligning clips to the PC clock, Theia
nav_order: 5
---

# Sony Cameras and Theia

## How it connects

- The PC joins the cameras' network and talks to the Sony **camera control
  boxes** (one per camera; the first one is the master, usually
  `http://169.254.200.200`). The Collector starts and stops every camera and reads
  each camera's state.
- For the tightest timing, the Collector plays a **timecode audio signal (LTC)**
  from a PC audio output into **one camera's microphone input**. That camera's
  clip then carries PC time in its audio.
- Every camera also stamps its video with **timecode**, set by the control box
  from its own clock when recording starts. The Collector listens to that clock
  (PTP) the whole time and saves it with each take, so every take can be placed
  on the PC clock even without LTC, to within a few tens of milliseconds.

## Settings in the Collector

- **Settings > Sync:** tick **Sony** and choose who starts the cameras (usually
  the Collector). Needs the Python setup (see [Overview](desktop-recorder.html#python-setup-needed-for-polar-sony-vicon-and-plotting)).
- **Settings > Sony:** the control box address; the **LTC output** (press
  **Refresh outputs**, then pick the output cabled to the camera); the **LTC
  level** (type it and press **Set**). Start at **0.016** with the output's
  Windows volume at 50%.
  While LTC plays, the Collector takes the LTC output for itself (WASAPI
  exclusive mode): nothing else can play sound on that output. This keeps the
  timing the same every time LTC starts. If another program holds the output,
  the Collector falls back to the shared mode and the log says so.
- **Collect > Sony section:**
  - **Get Browser Key** (takes control of the cameras), **Link Date/Time** (sets
    the cameras' clocks from the PC), **Unmute and set to 50%** (the LTC output's
    volume), **Play LTC signal**. **Scan All** does the first three for you.
  - The camera list, named as in the Sony webapp (e.g. `001  DSC-RX0M2_3177801`),
    with each camera's state. Pick the **LTC** camera: the one with the LTC cable.
  - The **PTP** line under the cameras reads **grandmaster heard** with the
    clock offset. If it says **not heard**, allow UDP ports 319 and 320 in
    Windows Firewall on the camera network; takes then fall back to LTC or
    timecode only.
  - **Rig details** (folded) shows the full control-box status when something
    is wrong.

<!-- screenshot: Sony section - action buttons and camera rows with the LTC camera picked -->

**Close the Sony webapp's browser tab before recording.** While it is open it
holds the control box and the Collector's start/stop is ignored.

If you start a take with Sony on but **Play LTC signal** off, the log warns that
the take will align without LTC.

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

On the **PC**, turn off **Audio enhancements** for the LTC output (Windows
**Settings > System > Sound**, pick the output, **Audio enhancements: Off**).
Enhancements level the signal automatically and spoil the LTC.

A **USB audio adapter** is the most reliable LTC output. Some built-in
headphone jacks cut out when a camera is plugged in, even though they work
with headphones.

## Calibration

**Check the LTC once per setup:**

1. Tick **Play LTC signal**, pick the LTC camera, record a 30-second take.
2. On **Postproc > Align to PC clock**, the take is already in the table. Tick
   it and press **Run on ticked**. The run copies the LTC camera's clip first.
3. The Sony column should read **ltc**. If it reads **ptp** or **tc**, the log
   says why the LTC did not decode. Try, in this order:
   1. turn off Windows Audio enhancements on the LTC output;
   2. Windows volume 50% and LTC level about 0.016;
   3. lower the camera's Audio Rec Level;
   4. use a USB audio output instead of a laptop headphone jack;
   5. check the cable sits in the LTC camera's microphone input.

<!-- screenshot: Postproc Align to PC clock table, Sony column "ltc" -->

**No timing calibration is needed per session.** With the LTC output in its
default (exclusive) mode, the LTC camera's video lands within about **±12 ms**
of PC time, under one video frame at 60 fps, with no calibration at all.

**Calibrate LTC (optional, once per PC and LTC output).** It measures the small
remaining offset between the LTC in the audio and the video frames (K_av) for
your exact hardware, for labs that want to check it or report it:

1. In **Settings > Sony**, under **Calibrate LTC**, press **Open clock page** and
   make the page full screen. It shows the PC clock and three strips of squares.
2. Point the LTC camera at the screen, straight on, with all three strips in
   view.
3. Press **Calibrate**. The Collector plays LTC, records 12 seconds, copies the
   clip and reads the clock from the video. After about a minute it shows the
   result, for example "K_av = 9 ms (spread 18 ms)", and saves it for that LTC
   output.

Repeat it after changing the PC, the LTC output or the audio adapter. The
measured value includes the monitor's own display delay, so treat it as a check
to within a frame rather than an absolute figure.

## Post-processing

**Postproc > Align to PC clock** puts the external systems on the PC clock;
the sensor files are already on it and are not changed. Each finished take is
added to the table; you can also add folders or all of today's takes, and run
many at once. For each ticked take the run:

- copies the LTC camera's clip into the session folder if it is not there yet;
- writes `aligned\sony_frames_pc.csv`: every video frame with its PC time, and
  the method used for the take:
  - **ltc** - from the LTC in the clip's audio (within about one video frame);
  - **ptp** - from the control box clock saved during the take (to a few tens of
    milliseconds);
  - **tc** - from the camera timecode alone (can be about a second off);
- writes `aligned\pc_alignment.json` with the result and any warnings for every
  system.

Clips from the other cameras: copy them with the Sony webapp's **Import**. All
cameras share the control box's timecode, so the same frame times apply.

Long takes may be split into several files of about 4 GB on a camera whose
memory card is formatted FAT32. Format the cards in the camera (exFAT) to keep
one file per take.

### Theia

Theia processes the clips into a motion file (C3D) whose frames are the video's
frames. Put Theia's C3D in the session folder (name containing `theia`, or in a
`theia` subfolder) before running **Align to PC clock**: the run writes
`aligned\theia_frames_pc.csv` with the PC time of every Theia frame.

## Files

| File | When | What |
|---|---|---|
| `sony-anchor.json`, `sony-events.csv` | at Stop | when the start and stop were sent and confirmed, on the PC clock |
| `timestamps-sony_ptp.csv` | at Stop | timestamps only: the control box clock next to the PC clock, about twice a second, from 5 minutes before the start to about 2 minutes after the stop |
| `<camera>_<clip>.MP4` | after Align | the LTC camera's clip |
| `aligned\sony_frames_pc.csv` | after Align | every video frame with its PC time |
| `aligned\sony-clock.csv` | after Align | the camera timecode worked out from the control box clock, next to the PC clock |
| `aligned\theia_frames_pc.csv` | after Align | every Theia frame with its PC time (when a Theia C3D is present) |
| `aligned\pc_alignment.json` | after Align | the method and quality for every system |
