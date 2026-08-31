---
title: Syncing with other systems
parent: Desktop recorder
description: how sensor data lines up with Polar, Vicon, and Sony/Theia - what to set up before, and the fixed offsets to remove after
nav_order: 3
---

# Syncing with other systems

Every stream the recorder writes is stamped with an **absolute timestamp on the
same computer clock** - IMU sensors, Polar H10, Vicon triggers, and Sony
cameras. So files line up by timestamp without any live "sync cable." What
differs per system is:

- whether you need a **one-time setup / calibration before recording**, and
- whether a **fixed offset** should be **subtracted afterward**.

This page covers both, per system.

## One-time setup: turning on the sync features

IMU time-sync works out of the box. The camera, Vicon, and Polar features run a
small Python helper, so the **first time you use them on a computer**, open
**Settings** and click **Set Up Python Environment**. It builds an isolated
Python (the newest 3.10-or-later it can find) and installs everything those
features need - one click, needs internet the first time, and it leaves the rest
of your computer's Python untouched. If no suitable Python is found, it tells you
to install one from python.org first.

For **Vicon**, also point **Vicon SDK path** (under Sync Sources in Settings) at
your Vicon DataStream SDK's Python folder. That is kept separate from the setup
above, so the two never interfere.

## Quick reference

| System | How it lines up | Before you record | Offset to remove after |
|---|---|---|---|
| **IMU sensors** (to each other) | shared time-sync counter | turn **Time Sync ON** before connecting | none (~5 ms between sensors) |
| **Polar H10** | same PC clock (stamped on receive) | pair in Bluetooth + wear the strap | subtract **~50-65 ms** (Polar lags the IMU); also convert **ms -> microseconds** |
| **Vicon** | start/stop trigger + Nexus frame count | run the trigger (either direction) | none fixed - trigger aligns it |
| **Sony / Theia** | timecode / LTC on the same PC clock | **one-time K_av calibration per computer** | none by hand on LTC (K_av is applied to every clip when aligning); timecode-only ~150 ms |

We can compute your offsets and hand back **time-aligned files** - see
[Getting aligned files](#getting-aligned-files) below.

## IMU sensors (time-sync between sensors)

Turn **Time Sync ON** before you connect. All sensors then share one counter, so
they are aligned to about **5 ms** of each other for the whole session. Nothing to
remove afterward. (Time Sync off leaves each sensor on its own start, ~100 ms
apart.)

## Polar H10

The H10 is captured on the **same PC clock** as the IMUs, stamped when the
computer receives each sample - so ECG, accelerometer, and heart rate
cross-reference against the IMU data directly. Two things to know:

- **Units differ.** The Polar timestamp column is in **milliseconds**; the IMU
  timestamp is in **microseconds**. Multiply the Polar timestamp by 1000 before
  comparing.
- **Fixed offset: the Polar lags the IMU by ~50-65 ms** (Bluetooth receive
  latency). It is stable - not drift - so subtract that constant. You can measure
  it yourself for a session: hold a sensor against the strap, do a few squats or
  taps, and line up the accelerometer traces.

No calibration is needed before recording. Just **pair the strap in your
computer's Bluetooth settings first, and wear it** (a dry strap will not stream
ECG).

## Vicon

Vicon lines up by the **start/stop trigger plus Nexus frame count** - the
recorder either starts Nexus or listens for Nexus to start it, and the sensor
folder is matched to the Vicon capture by trial name. There is **no fixed offset
to remove**: the trigger aligns the start and the frame count locates frames.

For a tight check, do a **shared physical event** (a hop or heel-drop) at the
start of the trial - it appears in both the marker data and the IMU accel, so you
can confirm the alignment to a frame.

## Sony cameras (and Theia)

This is the most involved, because the cameras have **no shared sync cable to the
computer** - alignment is done from timecode. There are two routes:

- **LTC (recommended, sub-frame).** An audio cable carries a timing signal;
  clips are aligned from it. This needs **K_av**, a small **per-computer**
  audio-to-video offset. It is measured **once per computer** (from a short
  calibration clip) and saved - after that, alignment is sub-frame. K_av is
  specific to a given laptop/audio setup, so **re-measure it on a new machine**.
- **Timecode only (no extra gear, ~150 ms).** Align from the camera timecode.
  This carries a per-power-on wobble of about **150 ms**; anchoring to a shared
  event (again, a hop) at record time tightens it.

**Before recording:** have K_av calibrated for the computer you are using -
**measure it once per computer** (it is saved), not once per session.

**After recording:** you do not subtract anything by hand, but **K_av is applied
to every clip** when the files are aligned - each clip's PC time is its LTC time
plus K_av (the fixed structural timecode offset is applied for you too). So K_av
is measured once for the machine, then baked into *every* aligned file. (A
capture taken before K_av was calibrated is still recoverable - K_av is applied
as a separate step, so it can be measured from a calibration clip later and
applied after the fact.)

(Things that look alarming but cost nothing: cameras can *start* up to ~12 frames
apart, and there is a ~375 ms record-start delay - both are absorbed because
alignment is by timecode, not by file start.)

## Getting aligned files

The recorder's job is to **capture every stream on one clock**; combining them
into aligned files is a post-step. We can:

- **measure your offsets** (K_av for a computer, the Polar constant, a Vicon/Sony
  anchor), and
- **produce time-aligned output** across IMU, Polar, Vicon, and Sony/Theia.

If a capture was taken before K_av was calibrated, it can still be salvaged later
- K_av is applied as a separate step, so a clip recorded with it uncalibrated is
recoverable from a calibration clip. Reach out with your session folder and we
will return the aligned files and the offsets used.
