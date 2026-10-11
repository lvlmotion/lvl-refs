---
title: LEVEL Sensors
parent: LEVEL Collector for Windows
description: recording LEVEL Inez sensors through the LEVEL Hub - settings, time sync, files
nav_order: 3
---

# LEVEL Sensors

## How it connects

LEVEL Inez sensors talk to the **LEVEL Hub** (USB, plugged into the PC) over
Bluetooth. One sensor acts as the **time beacon**; the others follow its clock,
so all sensors share one timeline. Connecting is covered in
[Connecting Sensors](windows-connecting-sensors.html).

## Settings in the Collector

| Where | Setting | Use |
|---|---|---|
| Settings | **Time Sync** | On (default). Applied when sensors connect. |
| Settings | **On launch: Scan / Connect** | find, or find and connect, sensors when the Collector opens |
| Collect | **Rate** | 100 Hz standard |
| Collect | **Batch** | 12 for more than 4 sensors (the sidebar warns if it is too low) |
| Collect | sensor **colour** and **location** | click the LED or Location cell; saved on the sensor and in the session files |

## Settings on the other system

None. Keep sensors charged and awake (see [About Sensors](about-sensors.html)).

## Calibration

- After connecting, every sensor's **Sync** cell should read **B** (the beacon)
  or **S** (following). A red **✗** means it did not join the time sync:
  disconnect and connect again.
- During a take, the Sync cell shows each sensor's offset from the beacon in
  milliseconds. It should stay near 0. A red **⚠** with a number means that
  sensor drifted off the beacon at some point; consider re-taking.

## Post-processing

- Each sensor file has the sensor's own time, the PC arrival time of every
  packet, and a `time` column already placed on the PC clock when the take
  started.
- For long takes, the sensor clock can be refitted to the PC clock afterwards
  (a host-clock fit). We can run this for you on request; it is not a button in
  the Collector yet.

## Files

| File | What |
|---|---|
| `imu-<location>-<id>.csv` | one per sensor: time, accelerometer, gyroscope, magnetometer, sensor time, PC arrival time |
| `meta-summary.json`, `meta-debug.json`, `meta-telemetry.csv` | session details, time-sync record, data-quality log |
| `sync.json` | which systems were on and which one started the take |
