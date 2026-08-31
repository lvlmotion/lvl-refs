---
title: Running a recording
parent: Desktop recorder
description: step-by-step - connect sensors and record a session on the desktop app
nav_order: 2
---

# Running a recording

Step by step, from a cold start to files on disk. Assumes the app is installed
(see [First install](installing-the-recorder.html)) and the sensors are charged.

## Basic recording (IMU only)

1. Plug the **USB dongle** into the computer.
2. Open the app.
3. If you want the sensors time-synced to each other, open **Settings**, turn
   **Time Sync** on, then come back to the **Recorder** tab. (Time Sync is applied
   when the sensors connect, so set it before step 5.)
4. On the **Recorder** tab, press **Scan**.
5. Your sensors appear and connect. Wait until each shows connected (the sensor
   LED goes solid). Check the battery level - recharge any showing LOW.
6. Type a **trial name** in the name box (optional; it labels the session folder).
7. Press **Stream** to start recording. The trial bar shows it is recording.
8. Press **Stop** to end. The files are written and the sensors stay connected, so
   you can name the next trial and press Stream again without re-scanning.

If a sensor or the dongle drops out mid-recording, the trial bar turns red and
says to check the log - stop, fix it, and re-take.

## Recording with a sync source

If you set up Vicon, Sony, or the relay (see First install, Part 2):

1. Do steps 1-5 above (for the no-IMU relay you can skip the dongle/sensors).
2. Confirm the **Sync** panel diagram shows the setup you intend - who is master,
   which way each trigger runs.
3. Start the capture from whichever side is **master**:
   - *App as master* - press **Stream** (it triggers the other system too).
   - *Vicon/Sony as master* - start in Nexus or on the Sony console; the app
     follows automatically.
4. Stop the same way (Stream/Stop if the app is master, or stop on the other
   system if it is master).

## Where the files go

Each session is a timestamped folder under the app's data directory
(`LEVEL_Sensor/data/`), named with your trial name. Each sensor's raw CSV is
inside, plus any sync anchor files. See
[Sharing your data](sharing-data.html) for getting them off the machine.
