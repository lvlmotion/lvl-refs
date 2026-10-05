---
title: Home
nav_order: 1
---

# LEVEL References

Reference material for LEVEL Motion sensors and apps: what we make, and the guides for using it.

## Sensors and apps

LEVEL Motion makes wearable motion sensors and the software that records them.
A recording setup has three parts:

1. **LEVEL Inez sensors**, worn on the body.
2. A way to receive their data: your **phone's own Bluetooth**, or the
   **LEVEL Hub** USB receiver for larger setups.
3. An **app** that records everything to plain files: **LEVEL Collector**
   today, with **LEVEL Mobility** in development.

### LEVEL Inez - the sensor

A small wearable motion sensor that clips or straps onto the body - feet,
lower back, wrists, legs or chest. See [Sensor placement](sensor-placement).

| Feature | Specification |
|---|---|
| Motion sensing | 6-axis: 3-axis accelerometer (±16 g) and 3-axis gyroscope (±2000 deg/s) |
| Size and weight | 37.8 × 40.2 × 10.9 mm, 13 g |
| Sensors per recording | up to 3 at 100 Hz over a phone's own Bluetooth; up to 7 at 100 Hz through LEVEL Hub |
| Sampling rate | set per recording; 50, 100 and 200 Hz |
| Wireless | Bluetooth 5 (Low Energy) |
| Battery | 36 hours of continuous streaming at 100 Hz |
| Charging | USB-C |
| Other features | one multi-colour LED; programmable button to log events |
| Time sync | LEVEL Hub beacon clock ensures all sensors maintain under 5 ms drift of each other |
| Firmware | updated over Bluetooth (see [Updating firmware](updating-firmware)) |

For charging, waking and the light patterns, see [About sensors](about-sensors).

### LEVEL Hub - the USB receiver

A small USB-C receiver that collects data from several sensors at once and
hands it to the phone or computer over USB. Use it when you need more sensors
than the phone's Bluetooth handles comfortably, or when recording on a PC.

| Feature | Specification |
|---|---|
| Connects to | an Android phone (USB-C) or a Windows PC (USB) |
| Sensors per Hub | up to 7 sensors at 100 Hz |
| Without a Hub | a phone's own Bluetooth handles up to 3 sensors at 100 Hz |

### LEVEL Collector - the research app

The research app that records several LEVEL Inez sensors at once, together
with other devices, all on one clock, as plain documented CSV files you can
open in any tool.

- **On an Android phone** (Android 12 or later): records sensors over the
  phone's Bluetooth or a LEVEL Hub, plus the phone's own GPS, barometer and step
  counter. On the phone the app is labelled **LEVEL Sensor**. See
  [Collecting data](collecting-data) and [Sharing recorded data](sharing-data).
- **On a Windows PC** (the [desktop recorder](desktop-recorder)): records
  sensors over a LEVEL Hub and coordinates lab systems such as Vicon motion
  capture and Sony cameras.

### LEVEL Mobility - the gait app (in development)

A clinical app that turns sensor recordings into gait and mobility results for
standard tests, such as timed walks and the Timed Up and Go. LEVEL Mobility is
**in development** and not yet available.

### Works with

| Device or system | What it adds | Phone | Desktop |
|---|---|---|---|
| **Polar H10** chest strap | heart rate, RR intervals, ECG, chest motion | yes | yes |
| **Phone sensors** | GPS, barometer, step counter | yes | - |
| **Vicon** motion capture | start/stop trigger and frame count to line the recordings up | - | yes |
| **Sony RX0 II cameras** with **Theia** markerless tracking | timecode so video and sensor data line up | - | yes |

How each one lines up with the sensor data, and any fixed offsets to remove,
is on [Syncing with other systems](syncing-with-other-systems).

## Guides

{% assign guides = site.pages | where_exp: "p", "p.name != 'index.md'" | where_exp: "p", "p.title" | sort: "title" %}
{% for p in guides %}
- [{{ p.title }}]({{ p.url | relative_url | replace: '.html', '' }}){% if p.description %} - {{ p.description }}{% endif %}
{% endfor %}

More guides (manuals, FAQs) will be added here over time.

## Contact

For sales and partnerships, see [lvlmotion.com](https://lvlmotion.com) or email [info@lvlmotion.com](mailto:info@lvlmotion.com)
