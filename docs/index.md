---
title: Home
nav_order: 1
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
| Sensors with a Hub | up to 7 sensors at 100 Hz |
| Sensors with Android's own Bluetooth | up to 3 sensors at 100 Hz |
| Sensors with Windows' own Bluetooth | not supported |

### LEVEL Collector for [Android](android) and [Windows](desktop-recorder)

The research app for recording LEVEL sensors together with other devices, on a phone in the field or on a PC in the lab.

- Everything on one clock
- The phone app runs on Android 12 or later

| Device or system | What it adds | Android | Windows |
|---|---|---|---|
| **Android phone sensors** | GPS, barometer, step counter | yes | - |
| **LEVEL Inez sensors** | accelerometer and gyroscope motion data | yes | yes |
| **Polar H10** chest strap | heart rate, RR intervals, ECG, chest motion | yes | yes |
| **Sony RX0 II cameras** with **Theia** markerless tracking | timecode so video and sensor data line up | - | yes |
| **Vicon** motion capture | start/stop trigger and frame count to line the recordings up | - | yes |

How each one lines up with the sensor data is on its own page in the [LEVEL Collector for Windows](desktop-recorder) guide.

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

For more information, see [lvlmotion.com](https://lvlmotion.com), or email [info@lvlmotion.com](mailto:info@lvlmotion.com).
