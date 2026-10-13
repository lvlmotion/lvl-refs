---
title: LEVEL Sensors
parent: LEVEL Collector for Windows
description: connecting and recording LEVEL Inez sensors through the LEVEL Hub - rate and batch, the sensor table, time sync, files
nav_order: 3
---

# LEVEL Sensors

## How it connects

LEVEL Inez sensors talk to the **LEVEL Hub** (USB, plugged into the PC) over
Bluetooth. One sensor acts as the **time beacon**; the others follow its clock,
so all sensors share one timeline, to a few milliseconds. The PC's arrival time
of every packet is saved too, which ties the sensors' clock to the PC clock, the
timeline every other system is aligned to.

## Before you start

- Charge the sensors (see [About Sensors](about-sensors.html)). Pick one up to
  wake it: an asleep sensor has no light and will not be found.
- Plug the **LEVEL Hub** into the PC. A direct USB port is better than a hub.

## Connect

1. In the **Collect** tab's LEVEL section, press **Scan** (or **Scan All** at the
   top). Found sensors are listed. The sensors from your last recording are
   ticked for you.
2. Tick or untick sensors as needed.
3. Set **Rate** and **Batch**: look up your number of sensors and rate in
   [Rate and batch](#rate-and-batch).
4. Press **Connect** (or **Connect All**). Each sensor's light goes solid and its
   row shows **Connected**.

<!-- screenshot: IMU card with Scan / Connect / Rate / Batch and the sensor table -->

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

## The sensor table

| Column | What it shows |
|---|---|
| LED | the sensor's colour (click to change; only while connected) |
| MAC | the 4-character ID printed on the sensor |
| Location | where it is worn (click to set; only while connected) |
| Battery | charge level; recharge at LOW |
| Status | Found / Connecting / Connected / Streaming |
| Sync | **B** = the time beacon, **S** = following it, then its offset from the beacon in ms. A red **✗** means the sensor is not time-synced: disconnect and reconnect it. A red **⚠** with a number means it drifted off the beacon during the take. |
| Packet Loss | data lost on the way to the PC; red above 0.1% |
| Rows | samples written this take |

What each light pattern on the sensor means, plus waking and resetting a sensor:
[About Sensors](about-sensors.html#led-light-patterns).

## Settings on the other system

None. Keep sensors charged and awake (see [About Sensors](about-sensors.html)).

## Calibration

- After connecting, every sensor's **Sync** cell should read **B** (the beacon)
  or **S** (following). A red **✗** means it did not join the time sync:
  disconnect and connect again.
- During a take, the Sync cell shows each sensor's offset from the beacon in
  milliseconds. It should stay near 0. A red **⚠** with a number means that
  sensor drifted off the beacon at some point; consider re-taking.

## If something goes wrong

- **No sensors found:** wake them (pick them up), then Scan again. Sensors held by
  a phone or another computer do not show; disconnect them there first.
- **A sensor shows a red ✗ in Sync:** press Disconnect, then Connect again.
- **During a take the sensors drop out:** the LEVEL card turns red and says so.
  The other systems keep recording; press **Stop Stream** when you decide to end
  the take.

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
