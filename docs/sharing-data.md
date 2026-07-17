---
title: Sharing Recorded Data
---

# Sharing Recorded Data

Every recording session saves one CSV file per sensor to the phone's internal
storage, in a folder named after the date and time of the session:

```
Internal storage / Documents / LEVEL_Sensor / 2026_07_17_12_13_50 /
    imu-chest-1847.csv
    imu-right knee-70a8.csv
```

There are two ways to get that data off the phone:

- **[Option A](#option-a-share-right-after-recording)** - share directly from
  the LEVEL Sensor app, right after you finish a recording. Fastest when you
  are still holding the phone at the end of a session.
- **[Option B](#option-b-share-later-with-my-files)** - use the My Files app
  (pre-installed on Samsung phones) to find, zip, and send a session folder
  after the fact. Use this for older sessions or when sending several sessions
  at once.

---

## Option A: Share right after recording

This walks the whole flow from connecting sensors to sharing the files, as it
happens during a normal session.

### 1. Connect your sensors

Open the LEVEL Sensor app. It scans for nearby sensors automatically. Make sure
your sensors are turned on and nearby - each one appears in the list with its
ID and battery level.

<img src="assets/sharing-data/app-01-scan-searching.jpg" alt="The app searching for sensors, with two sensors listed under Available Sensors" width="280">

Tick the sensors you want to use, then tap **CONNECT N SENSORS**.

<img src="assets/sharing-data/app-02-select-sensors.jpg" alt="Both sensors ticked, with the Connect 2 Sensors button at the bottom" width="280">

### 2. Create a profile (first time only)

Once the sensors connect, the app asks you to add them to a profile. A profile
groups the sensors you use together, so next session you can reconnect the
whole set in one tap. Tap **CREATE A PROFILE**, give it a name, and tap
**CREATE PROFILE & CONTINUE**.

<img src="assets/sharing-data/app-03-sensors-connected.jpg" alt="Sensors Connected screen with Create a Profile button" width="280">
<img src="assets/sharing-data/app-04-create-profile.jpg" alt="Create a Profile screen with a name typed in" width="280">

### 3. Label each sensor's placement

For each sensor, the app highlights the sensor ID and asks where on the body it
is placed. Pick the label that matches (or **ADD CUSTOM LABEL**), then tap
**SAVE SENSOR LOCATION**. The label ends up in the CSV filename, so accurate
labels make the data much easier to work with later.

<img src="assets/sharing-data/app-05-place-sensor-1.jpg" alt="Place Your Sensors screen for the first sensor with Chest selected" width="280">
<img src="assets/sharing-data/app-06-place-sensor-2.jpg" alt="Place Your Sensors screen for the second sensor with Right Knee selected" width="280">

### 4. Record the session

The profile screen shows every sensor with its placement, ID, battery, and
connection status. When everything reads CONNECTED, tap **START SESSION**.

<img src="assets/sharing-data/app-07-start-session.jpg" alt="Profile screen listing both sensors as connected, with Start Session button" width="280">

While recording, each sensor shows STREAMING. Run your movement or test, then
tap **STOP RECORDING**.

<img src="assets/sharing-data/app-08-recording.jpg" alt="Now Recording screen with both sensors streaming" width="280">

### 5. Share the files from the Recording Saved screen

The confirmation screen lists the CSV file saved for each sensor and shows the
folder they were saved to. Tap the **Documents/LEVEL_Sensor/...** link to open
that session folder in your Files app, straight from the confirmation screen.

<img src="assets/sharing-data/app-09-recording-saved.jpg" alt="Recording Saved screen listing one CSV per sensor and the folder path" width="280">

From there, select the files (or go up one level and select the whole session
folder), tap **Share**, and pick how to send them - email, Drive, or any other
app on the phone. If you are sharing the whole folder, zip it first: see
[Compress the session folder](#3-compress-the-session-folder-to-a-zip) below.

<!-- TODO: add screenshots of the share sheet from this entry point, and
     confirm exactly what tapping the folder link opens on stock Samsung
     (My Files at the session folder?). -->

---

## Option B: Share later with My Files

Any past session can be found and sent with the My Files app that comes
pre-installed on Samsung phones. (On other Android phones the equivalent app
is usually called Files or Files by Google - the steps are the same, but the
screens look different.)

### 1. Open My Files and go to Internal storage

Open **My Files** (swipe up on the home screen and search for it if you don't
see the icon). On the home screen of My Files, scroll to and tap
**Internal storage**.

<img src="assets/sharing-data/myfiles-01-home.jpg" alt="My Files home screen showing Internal storage" width="280">

### 2. Navigate to Documents, then LEVEL_Sensor

Inside Internal storage, open the **Documents** folder, then open
**LEVEL_Sensor**. Each recording session is a folder named by its date and
time, for example `2026_07_14_17_50_47` for a session recorded on
July 14 at 5:50 p.m.

<img src="assets/sharing-data/myfiles-02-internal-storage.jpg" alt="Internal storage folder list including Documents" width="280">
<img src="assets/sharing-data/myfiles-03-documents.jpg" alt="Documents folder showing the LEVEL_Sensor folder" width="280">
<img src="assets/sharing-data/myfiles-04-level-sensor.jpg" alt="LEVEL_Sensor folder showing one session folder named by date and time" width="280">

### 3. Compress the session folder to a zip

Long-press the session folder to select it, tap **More** (the three dots at
the bottom right), and choose **Compress**. Keep the suggested name and the
**Zip** format, then tap **Compress**. The zip file appears next to the folder.

Zipping keeps the files of a session together in one attachment and makes them
smaller to send. Leave **Protect with password** off unless you have been asked
to password-protect the data.

<img src="assets/sharing-data/myfiles-05-folder-menu.jpg" alt="Session folder selected, with the More menu open showing Compress" width="280">
<img src="assets/sharing-data/myfiles-06-compress.jpg" alt="Compress folder dialog with Zip format selected" width="280">

### 4. Share the zip

Long-press the new zip file to select it, then tap **Share** in the bottom bar
and pick how to send it - email, Drive, or any other app on the phone.

<!-- TODO: add screenshots of selecting the zip and the share sheet. -->

---

## Tips

- **One folder per session.** If you ran several trials, each STOP RECORDING
  created its own timestamped folder. Check the date and time in the folder
  name to pick the right one.
- **Filenames carry the placement.** Files are named
  `imu-<placement>-<sensor id>.csv` (for example `imu-chest-1847.csv`), so
  labelling placements correctly during setup (step 3 of Option A) is what
  makes the data identifiable afterwards.
- **Sending many sessions:** in My Files you can select several session
  folders at once before tapping Compress, which produces a single zip.
