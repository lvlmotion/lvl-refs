---
title: Polar H10
parent: LEVEL Collector for Windows
description: recording ECG, accelerometer and heart rate from a Polar H10 chest strap alongside the sensors
nav_order: 4
---

# Polar H10

## How it connects

The strap connects to the **PC's own Bluetooth** (not the LEVEL Hub). It starts
when you connect the sensors and stays connected across takes. Each take gets
its own ECG, accelerometer and heart-rate files.

## Settings in the recorder

- **Settings > Sync:** tick **Polar H10**. Needs the Python setup (see
  [Overview](desktop-recorder.html#python-setup-needed-for-polar-sony-vicon-and-plotting)).
- **Recorder > Polar section:** after **Scan All**, the straps in range are
  listed with their signal strength. Pick yours (**Use**). The recorder
  remembers the strap it last connected to.

<!-- screenshot: Polar rows on the Recorder page, strap picked -->

## Settings on the other system

**Pair the strap with Windows once per PC.** Without pairing, the strap sends
heart rate only - no ECG or accelerometer.

1. Put the strap on with the electrodes wet. It only appears while worn.
2. Windows **Settings > Bluetooth & devices > Add device > Bluetooth**, pick
   **Polar H10 \<ID\>** (the ID is printed on the pod). Never remove it afterwards.
3. If pairing fails: remove the strap in Windows, take the pod's battery out for
   10 seconds, and pair again.

## Calibration

- The strap needs a **warm-up of about 30-40 seconds** after connecting before
  ECG flows. The sidebar shows it in yellow: searching, connecting, warming up.
- Start the take once the Polar card is **green** with ECG about 130 Hz,
  accelerometer about 200 Hz, and heart rate.
- Right after the warm-up the ECG rate can read low for a few seconds before it
  settles; that is normal.
- If the ECG stops while heart rate keeps going, the recorder restarts the ECG
  stream by itself.

## Post-processing

- Every row has the strap's own timestamp and the PC time it arrived, so Polar
  lines up with the other systems on the PC clock.
- Polar times are in **milliseconds**; sensor times are in **microseconds**.
  Multiply Polar times by 1000 before comparing.
- The arrival time runs slightly behind the true sample time (Bluetooth delay).
  For tight comparisons, line it up on the start and end hops against a sensor
  worn near the strap.

## Files

| File | What |
|---|---|
| `polar_<id>_ecg_<time>.csv` | ECG at about 130 Hz |
| `polar_<id>_acc_<time>.csv` | accelerometer at about 200 Hz |
| `polar_<id>_hr_<time>.csv` | heart rate and beat-to-beat intervals |
