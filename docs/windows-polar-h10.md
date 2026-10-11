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

## Settings in the Collector

- **Settings > Sync:** tick **Polar H10**. Needs the Python setup (see
  [Overview](desktop-recorder.html#python-setup-needed-for-polar-sony-vicon-and-plotting)).
- **Collect > Polar section:** after **Scan All**, the straps in range are
  listed with their signal strength. Pick yours (**Use**). The Collector
  remembers the strap it last connected to.

<!-- screenshot: Polar rows on the Collect tab, strap picked -->

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
- If the ECG stops while heart rate keeps going, the Collector restarts the ECG
  stream by itself.
- If no ECG has arrived after about 75 seconds, the Polar line turns red with
  **No ECG**: re-wet the electrodes or reseat the strap, then press **Start
  warm-up** in the Collect tab's Polar section to start the warm-up again.
- If the strap's Bluetooth link drops, the Polar line says so. Press **Start
  warm-up** to reconnect.

## Post-processing

- Every row has the strap's own timestamp and the PC time it arrived.
- **Postproc > Align to PC clock** writes `aligned\polar_<id>_<ecg|acc|hr>_pc.csv`:
  the same rows plus a `pc_ms` column. It maps the strap's clock onto the PC
  clock along the fastest arrivals, which removes most of the Bluetooth delay.
  Heart rate has no strap timestamp, so its `pc_ms` is the arrival time.
- Polar times are in **milliseconds**; sensor times are in **microseconds**.
  Multiply Polar times by 1000 before comparing.

## Files

| File | What |
|---|---|
| `polar_<id>_ecg_<time>.csv` | ECG at about 130 Hz |
| `polar_<id>_acc_<time>.csv` | accelerometer at about 200 Hz |
| `polar_<id>_hr_<time>.csv` | heart rate and beat-to-beat intervals |
| `aligned\polar_<id>_<kind>_pc.csv` | after Align: the same rows with PC time |
