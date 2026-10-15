---
title: LEVEL Sensor SDK for Android
description: stream LEVEL Inez sensors into your own Android app
nav_order: 5
---

# LEVEL Sensor SDK for Android

The LEVEL Sensor SDK lets your own Android app receive data from LEVEL Inez
sensors over the phone's Bluetooth, without the LEVEL Collector app. It is a
single `.aar` library: scan for sensors, connect, and receive accelerometer and
gyroscope samples at 100 Hz per sensor. The SDK is in beta.

The SDK is distributed as a zip (`level-sdk-<version>.zip`) with the library,
a starter app, the licenses and a changelog. To get it, email
[info@lvlmotion.com](mailto:info@lvlmotion.com) with what you plan to build; we
send a download link. The SDK only works with genuine LEVEL sensors, uses the phone's own
Bluetooth (not the LEVEL Hub), and does no time synchronisation between
sensors or any processing: for recordings with everything on one clock, use the
LEVEL Collector app.

Stream IMU data from Level sensors into your own Android app over phone Bluetooth LE.
Tested with 2 sensors at once. Each sensor streams 100 Hz accelerometer + gyroscope.

## Setup

1. Unzip the download and copy `libs/level-sdk.aar` into your app module's `libs/` folder.
2. In the app module's `build.gradle.kts`:

   ```kotlin
   android { defaultConfig { minSdk = 31 } }

   dependencies {
       implementation(files("libs/level-sdk.aar"))
       implementation("com.google.guava:guava:33.5.0-android")
       implementation("commons-codec:commons-codec:1.20.0")
   }
   ```

3. Request `BLUETOOTH_SCAN` and `BLUETOOTH_CONNECT` at runtime before scanning
   (the SDK's manifest already declares them).

## Usage

```kotlin
// Scan (callback on the main thread; repeats per advertisement)
val scanner = LevelScanner(context)
scanner.start { found -> /* found.address, found.label, found.rssi, found.batteryVolts */ }
scanner.stop()

// Connect and stream, one LevelSensor per sensor
val sensor = LevelSensor(context, address, object : LevelSensor.Listener {
    // Called once per sample (100 Hz per sensor) between startStreaming() and stopStreaming()
    override fun onSample(sensor: LevelSensor, sample: ImuSample) {
        val a = sample.accel  // m/s^2, [x, y, z]
        val g = sample.gyro   // rad/s, [x, y, z]
        Log.d("LevelSdk", "%d accel %.3f %.3f %.3f  gyro %.3f %.3f %.3f".format(
            sample.timeUs, a[0], a[1], a[2], g[0], g[1], g[2]))
    }
    override fun onStateChanged(sensor: LevelSensor, state: LevelSensor.State) { }
    override fun onError(sensor: LevelSensor, message: String) { }
})
sensor.connect()          // -> CONNECTING -> CONNECTED (about 1-3 s)
sensor.startStreaming()   // -> STREAMING
sensor.stopStreaming()    // -> CONNECTED
sensor.disconnect()       // -> DISCONNECTED
```

Calls return immediately; commands run in order on a per-sensor thread.
`startStreaming()` before CONNECTED is ignored, so wait for the state change.

Listener callbacks arrive on a Bluetooth thread. Return quickly and post to the
main thread before touching UI. The `Log.d` output above shows in Logcat
(filter on tag `LevelSdk`); at 100 Hz per sensor it is verbose, so use it for a
quick check, not for recording.

## Sample fields (`ImuSample`)

| Field | Meaning |
|---|---|
| `accel` | m/s^2, x/y/z in the sensor frame (+Z out of the LED face). An axis pointing up reads about +9.81. |
| `gyro` | rad/s, x/y/z in the sensor frame |
| `calibrated` | true when the sensor's factory calibration was applied; if false (calibration could not be read), accel/gyro are NaN |
| `timeUs` | continuous time in microseconds since 1970: phone time at the first sample, then advanced by the sensor clock. Never wraps, no Bluetooth jitter; restarts with each `startStreaming()`. Use this to timestamp samples. |
| `sensorTimeMs` | sensor clock in ms, 16-bit, wraps at 65536. Steps 10 ms per sample; a larger step means lost samples. |
| `frame` | 8-bit sample counter, wraps at 256 |
| `hostTimeMs` | phone clock (ms) when the Bluetooth packet arrived; 5 consecutive samples share it |

Sensors are not time-synchronized with each other. `timeUs` of two sensors
started together lines up to within tens of ms (each anchors to the phone clock
at its own first sample); for tighter alignment use a shared event such as a tap.

## Known limitations (beta)

- About 1 in 6 phone Bluetooth connection attempts fails at the link layer (Android reports GATT status 133). The SDK retries twice, a second apart, so this is rarely visible; if all three attempts fail it reports `onError`, and calling `connect()` again normally succeeds.
- If a sensor stops responding to a command for 5 s, the link is dropped
  (`onError("connection lost")`). Reconnect with `connect()`.
- More than 2 sensors per phone is untested.

## Demo app

`demo/` in the zip is a one-screen starter app built against `libs/level-sdk.aar`: scan, tap
a sensor to connect, start/stop streaming, and show per-sensor sample and loss
counts. Build it with `./gradlew :demo:assembleDebug`.

Each "Start streaming" press creates a recording folder with one CSV per sensor:

    Documents/LEVEL_SDK/<yyyy_MM_dd_HH_mm_ss>/imu-[<label>-]<last 4 of MAC>.csv

CSV columns (same layout as the LEVEL Sensor app):

| Column | Meaning |
|---|---|
| `time` | microseconds since 1970: phone time at the first sample, then advanced by the sensor clock |
| `accel_x..z` | m/s^2, 6 decimals |
| `gyro_x..z` | rad/s, 6 decimals |
| `frame_sensor` | 8-bit counter |
| `time_sensor` | raw sensor clock in ms, signed 16-bit (wraps) |
| `time_host` | phone time in ms when the packet arrived |

## Reporting a problem

Email [info@lvlmotion.com](mailto:info@lvlmotion.com) with the SDK version
(`LevelSdk.VERSION`, also shown under About in the demo app), the phone model
and Android version, and what you saw.

## License

The SDK library is licensed under the LEVEL Motion Terms of Service, which
allow you to include it unmodified in your own applications for use with LEVEL
sensors. The demo app and documentation are open source under Apache 2.0.
Both licenses are in the zip (`LICENSE` and `libs/TERMS_OF_SERVICE.md`).
