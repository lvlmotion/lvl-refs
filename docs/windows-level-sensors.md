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
| Settings | **Time Sync** | On every time the Collector starts; keep it on. Turn it off only to save sensor battery (for that session). |
| Settings | **On launch: Scan / Connect** | find, or find and connect, sensors when the Collector opens |
| Collect | **Rate** and **Batch** | see [Rate and batch](#rate-and-batch) below (the sidebar warns if the batch is too low) |
| Collect | sensor **colour** and **location** | click the LED or Location cell while the sensor is connected; saved on the sensor and in the session files |

## Rate and batch

**Rate** is how many samples per second each sensor records. **Batch** is how
many samples each sensor sends per radio packet: larger batches let the LEVEL
Hub carry more sensors.

Recommended batch for a given number of sensors and rate, from our no-data-loss
tests (LEVEL Hub on Windows, Time Sync on, indoors):

| Sensors | Rate | Batch | Tested |
|---|---|---|---|
| up to 8 | 100 Hz | 12 | 6 and 8 sensors: no data lost (0.00-0.03%) in 15 and 30 minute takes |
| 6 | 100 Hz | 5 | may lose data (4-45% lost in tests): use 12 |
| 4 | 200 Hz | 12 | may lose data (about 0.5% on average, up to 2% on one sensor, 30 minutes) |
| 6 | 200 Hz | 12 | may lose data (about 44% lost) |

A combination not in the table has not been tested yet; use Batch 12. Outdoors,
in open air, any combination can lose a few percent.

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
