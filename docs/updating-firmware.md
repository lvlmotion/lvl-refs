---
title: Updating Firmware
description: how to update a sensor or the dongle over Bluetooth with nRF Connect Device Manager
nav_order: 6
---

# Updating Firmware

Sensor and dongle firmware is updated **over Bluetooth (BLE)** from a phone, one
device at a time, using a firmware image we provide. The procedure is identical
for a sensor and for the dongle; only the way you bring the device into an
updatable state differs (step 3).

You need three things: the firmware image we send you, the nRF Connect Device
Manager app, and the device being updated. Budget a couple of minutes per
device.

## 1. Obtain the firmware image

We supply the firmware image directly, by email or download link. It is a single
`.bin` file. Save it somewhere accessible on the phone (the Downloads folder is
fine) and do not rename it.

At present a single image covers both the sensor and the dongle, so the same
file applies whichever device you are updating. If that ever changes we will
label the files and tell you which applies to which device. When in doubt, check
with us before flashing.

## 2. Install nRF Connect Device Manager

Updates are performed with **nRF Connect Device Manager**, a free Nordic
Semiconductor application. Install it from the appropriate store:

- **Android** - [nRF Connect Device Manager on Google Play](https://play.google.com/store/apps/details?id=no.nordicsemi.android.nrfconnectdevicemanager)
- **iOS / iPadOS** - [nRF Connect Device Manager on the App Store](https://apps.apple.com/us/app/nrf-connect-device-manager/id1519423539)

Enable Bluetooth on the phone and grant the app Bluetooth / nearby-device
permission on first launch. This is a separate application from the LEVEL Sensor
recording app and is used only for firmware updates.

## 3. Bring the device into an updatable (idle) state

A device is updatable only while **idle** - powered on, but not connected or
streaming. A device in an active session does not advertise for update and will
not appear in the app. Update one device at a time:

- **Sensor** - powered on and awake (move it to wake it), but not connected in a
  session; close the LEVEL Sensor app if needed.
- **Dongle** - powered over USB, with no sensors connected to it. Keep sensors
  off or out of range, since the dongle stops advertising for update as soon as
  it connects to one.

## 4. Connect to the device

Open nRF Connect Device Manager. It lists nearby devices available for update.
Identify the target by name and tap to connect.

Idle devices advertise at a slow interval (roughly one to two seconds), so
discovery may take a moment. If the device is not listed immediately, wait a few
seconds and refresh.

## 5. Upload the firmware image

With the device connected, open the firmware update view (labelled **Firmware
Upgrade** or **Image**, depending on platform and version):

1. Select the `.bin` file saved in step 1.
2. Choose the update mode that both tests and confirms the image - typically
   **Test and Confirm**.
3. Start the upload. Keep the phone within short range and leave both devices
   undisturbed until the transfer completes. The device reboots into the new
   image automatically.

## 6. Confirm the image

After the reboot, the new image must be **confirmed** to become permanent.

- If you selected **Test and Confirm**, the app performs this automatically and
  reports the update as successful.
- If the app only offered **Test**, tap **Confirm** manually once the device has
  rebooted.

Do not omit this step. An image that is uploaded and booted but never confirmed
is treated as provisional: at the next power cycle the device reverts to the
previous firmware.

## Troubleshooting

- **Device not listed.** Verify it is powered and idle (step 3), that Bluetooth
  is enabled, and that no other app or session holds a connection to it. Refresh
  and allow a few seconds for the slow advertisement.
- **Dongle appears, then disappears.** A nearby sensor woke and the dongle
  connected to it. Power off or remove the sensors and retry.
- **Transfer fails partway.** The device is not harmed and retains its previous
  firmware. Bring it back to an idle state, reconnect, and restart the upload
  from step 4.
- **Unresolved.** Contact us with the device and the firmware image you were
  provided.
