---
title: Collecting Data
description: how to connect sensors, set up a profile, and record a session
nav_order: 4
---

# Collecting Data

This guide walks a full recording session in the LEVEL Sensor app, from
connecting sensors to saving the data. To send the recorded files off the
phone afterwards, see [Sharing recorded data](sharing-data).

## 1. Prepare the sensors

Make sure the sensors are charged. Each sensor charges from any USB-C cable and
charger - there is nothing special to plug in.

A sensor is either awake or asleep. It sleeps to save battery and wakes
automatically when you pick it up or move it. If a sensor does not wake on
movement, press the small reset button next to its USB-C port.

Once a sensor is awake you can connect to it. For what the light on the sensor
means and other sensor basics, see [About sensors](about-sensors).

## 2. Connect your sensors

Open the LEVEL Sensor app. It scans for nearby sensors automatically. Make sure
your sensors are turned on and nearby - each one appears in the list with its
ID and battery level.

<img src="assets/sharing-data/app-01-scan-searching.jpg" alt="The app searching for sensors, with two sensors listed under Available Sensors" width="280">

Tick the sensors you want to use, then tap **CONNECT N SENSORS**.

<img src="assets/sharing-data/app-02-select-sensors.jpg" alt="Both sensors ticked, with the Connect 2 Sensors button at the bottom" width="280">

## 3. Create a profile (first time only)

Once the sensors connect, the app asks you to add them to a profile. A profile
groups the sensors you use together, so next session you can reconnect the
whole set in one tap. Tap **CREATE A PROFILE**, give it a name, and tap
**CREATE PROFILE & CONTINUE**.

<img src="assets/sharing-data/app-03-sensors-connected.jpg" alt="Sensors Connected screen with Create a Profile button" width="280">
<img src="assets/sharing-data/app-04-create-profile.jpg" alt="Create a Profile screen with a name typed in" width="280">

## 4. Label each sensor's placement

For each sensor, the app highlights the sensor ID and asks where on the body it
is placed. Pick the label that matches (or **ADD CUSTOM LABEL**), then tap
**SAVE SENSOR LOCATION**. The label ends up in the CSV filename, so accurate
labels make the data much easier to work with later.

<img src="assets/sharing-data/app-05-place-sensor-1.jpg" alt="Place Your Sensors screen for the first sensor with Chest selected" width="280">
<img src="assets/sharing-data/app-06-place-sensor-2.jpg" alt="Place Your Sensors screen for the second sensor with Right Knee selected" width="280">

## 5. Record the session

The profile screen shows every sensor with its placement, ID, battery, and
connection status. When everything reads CONNECTED, tap **START SESSION**.

<img src="assets/sharing-data/app-07-start-session.jpg" alt="Profile screen listing both sensors as connected, with Start Session button" width="280">

While recording, each sensor shows STREAMING. Run your movement or test, then
tap **STOP RECORDING**.

<img src="assets/sharing-data/app-08-recording.jpg" alt="Now Recording screen with both sensors streaming" width="280">

## 6. Done - your data is saved

The Recording Saved screen confirms where the files went: one CSV per sensor,
in a folder named after the date and time of the session under
`Documents/LEVEL_Sensor/`. Each recording session creates its own folder.

From here you can share the data straight away - see
[Sharing recorded data](sharing-data).
