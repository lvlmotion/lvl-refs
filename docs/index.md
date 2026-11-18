---
title: Home
nav_order: 1
redirect_from:
  - /sensors-and-apps.html
---

# LEVEL References

Reference material for LEVEL Motion sensors and apps. 

## Latest versions

| App | Latest version | Get it |
|---|---|---|
| LEVEL Collector for Android | 0.1.13 | [Google Play](https://play.google.com/store/apps/details?id=com.lvlmotion.appsensor) |
| LEVEL Collector for Windows | 0.1.43 | Email [info@lvlmotion.com](mailto:info@lvlmotion.com) |
| LEVEL Mobility for Android | 0.1.0 | Email [info@lvlmotion.com](mailto:info@lvlmotion.com) |
| LEVEL ROM for Android | 0.1.0 | Email [info@lvlmotion.com](mailto:info@lvlmotion.com) |
| LEVEL Sensor SDK for Android | 1.4.4-5bc46e5-1.0 | Email [info@lvlmotion.com](mailto:info@lvlmotion.com) |

### [Hardware](hardware)

The LEVEL Inez wearable motion sensor and the LEVEL Hub USB receiver.

**LEVEL Inez** - a small wearable motion sensor that clips or straps onto the body.

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
| Firmware | updated over Bluetooth (see [Updating Firmware](updating-firmware)) |
| File format | CSV |
| Certifications | radio module: CE, FCC, ISED, RCM, TELEC, SAR evaluated; full product-level FCC/ISED in progress, CE pending |

**LEVEL Hub** - a small USB-C receiver that collects data from several sensors at once and hands it to the phone or computer over USB. Use it when you need more sensors than the phone's Bluetooth handles comfortably, or when recording on a PC.

| Feature | Specification |
|---|---|
| Connects to | an Android phone (USB-C) or a Windows PC (USB) |
| Sensors per Hub | up to 7 sensors at 100 Hz |
| Without a Hub | a phone's own Bluetooth handles up to 3 sensors at 100 Hz |

### [LEVEL Collector for Android](android)

The phone app for recording LEVEL sensors in the lab or in the field.

- Runs on Android 12 or later
- Records the phone's GPS, barometer and step counter with the sensors
- Records heart rate, RR intervals and ECG from a Polar H10 chest strap
- Everything on one clock

### [LEVEL Collector for Windows](desktop-recorder)

The Windows app for recording LEVEL sensors together with lab systems.

- Records alongside Vicon motion capture, lined up by start/stop trigger and frame count
- Records alongside Sony RX0 II cameras with Theia markerless tracking, lined up by timecode
- Records heart rate, RR intervals and ECG from a Polar H10 chest strap
- Everything on one clock

### [LEVEL Mobility for Android](mobility)

The clinical phone app that turns sensor recordings into gait and mobility results. In development.

- Three built-in tests: walking, Timed Up and Go, and balance
- Live feedback during walking and balance

### [LEVEL ROM for Android](rom)

The phone app for measuring joint range of motion.

- Live joint range of motion from sensors on the thigh, shank, chest, upper arm or forearm
- Up to 2 measured segments against an optional reference sensor

### [LEVEL Sensor SDK for Android](sdk)

A library for building LEVEL sensors into your own Android app.

- One library file to add to your app
- Streams calibrated accelerometer and gyroscope data at 100 Hz per sensor
- Starter app included

## Works with

| Device or system | What it adds | Phone | Desktop |
|---|---|---|---|
| **Polar H10** chest strap | heart rate, RR intervals, ECG, chest motion | yes | yes |
| **Phone sensors** | GPS, barometer, step counter | yes | - |
| **Vicon** motion capture | start/stop trigger and frame count to line the recordings up | - | yes |
| **Sony RX0 II cameras** with **Theia** markerless tracking | timecode so video and sensor data line up | - | yes |

How each one lines up with the sensor data is on its own page in the [LEVEL Collector for Windows](desktop-recorder) guide.

For more information, see [lvlmotion.com](https://lvlmotion.com), or email [info@lvlmotion.com](mailto:info@lvlmotion.com).
