---
title: Updating Firmware
description: how to update a sensor or the dongle over Bluetooth, or recover the dongle over USB
nav_order: 6
---

# Updating Firmware

Sensor and dongle firmware is normally updated **over Bluetooth (BLE)** from a
phone, one device at a time, using a firmware image we provide. The procedure is
identical for a sensor and for the dongle; only the way you bring the device
into an updatable state differs (step 3).

If a device cannot be reached over BLE - it never advertises for update, or we
instruct you that a particular release must be applied by cable - the dongle can
instead be recovered **over USB** with Nordic's desktop tooling. That path is in
[Recovering over USB](#recovering-over-usb) at the end of this guide; use the
BLE procedure below unless one of those conditions applies.

You need three things: the firmware image we send you, the nRF Connect Device
Manager app, and the device being updated. Budget a couple of minutes per
device.

## 1. Obtain the firmware image

We supply the firmware image directly, by email or download link. It is a single
`.bin` file. Save it somewhere accessible on the phone (the Downloads folder is
fine) and do not rename it.

The image is specific to the device type: the sensor image and the dongle image
are not interchangeable. If you are updating both, keep the two files clearly
labelled, and confirm with us which image applies to which device if there is
any ambiguity.

## 2. Install nRF Connect Device Manager

Updates are performed with **nRF Connect Device Manager**, a free Nordic
Semiconductor application. Install it from the appropriate store:

- **Android** - Google Play, *nRF Connect Device Manager*
- **iOS / iPadOS** - App Store, *nRF Connect Device Manager*

Enable Bluetooth on the phone and grant the app Bluetooth / nearby-device
permission on first launch. This is a separate application from the LEVEL Sensor
recording app and is used only for firmware updates.

## 3. Bring the device into an updatable (idle) state

A device is updatable only while **idle** - powered on but not in an active BLE
session. A sensor engaged in a recording session, or a dongle actively connected
to sensors, will not advertise for update and will not appear in the app.
Isolate the single device you intend to update:

**Sensor.** Ensure the sensor is not connected in a session - close the LEVEL
Sensor app, or disconnect it. Wake the sensor by moving it; the LED indicates it
is powered. An idle, awake sensor advertises for update.

**Dongle.** Power the dongle over USB (a host PC or a USB power supply). Keep all
sensors powered off or out of range. The dongle advertises for update only while
it holds no sensor connections; if a sensor is awake nearby it will connect,
the dongle becomes busy, and its update advertisement stops. With no sensors
present it remains idle and available.

Update one device at a time, with only that device awake. This keeps the
discovery list unambiguous and prevents the dongle from acquiring a sensor
mid-procedure.

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
   **Test and Confirm**. See [Test and confirm](#test-and-confirm) for why the
   confirm stage is required.
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
previous firmware. A skipped confirm therefore presents as an update that
"did not take."

## 7. Repeat for remaining devices

The device now runs the updated firmware. Return to step 3, bring the next
device into an idle state, and repeat. When all devices are updated, resume
normal use with the LEVEL Sensor app.

## Test and confirm

Every update is applied in two stages, by design:

1. **Test** - the device reboots and runs the new image provisionally.
2. **Confirm** - the new image is marked permanent.

If a device boots a new image but is never confirmed, it assumes the update is
faulty and rolls back to the previous firmware on the next reset. This guarantees
a bad or interrupted update cannot leave a device unusable, but it also means an
unconfirmed update silently reverts. Always complete the confirm stage: select
**Test and Confirm** where available, or issue **Confirm** after the reboot. If a
device appears to lose an update after a power cycle, an unconfirmed image is the
most likely cause - repeat the procedure and confirm.

## Recovering over USB

Use this path only when a device cannot be updated over BLE. Two cases call for
it:

- the dongle does not advertise for update and cannot be reached with nRF
  Connect Device Manager, or
- we tell you that a particular release is not compatible with over-the-air
  update and must be applied once by cable. (After a device is on that release,
  BLE updates resume as normal.)

Recovery is a wired operation and applies to the **dongle**, which connects over
USB. Sensors are updated over BLE only; if a sensor is unresponsive and will not
advertise, contact us rather than attempting a recovery yourself.

For this you use Nordic's desktop tool, **nRF Connect for Desktop**, and its
**Programmer** app. `nrfutil` on the command line is an equivalent alternative if
you prefer it.

1. **Install the tooling.** Install nRF Connect for Desktop, open it, and add the
   **Programmer** app from the app list.
2. **Obtain the recovery image.** We provide the image to flash over USB. It is
   distinct from the BLE `.bin`; use the file we designate for USB recovery.
3. **Connect the dongle** to the computer over USB.
4. **Enter the bootloader.** Press the dongle's **reset** button. The LED begins
   to pulse, indicating the dongle is in its USB bootloader and ready to be
   written.
5. **Write the image.** In Programmer, select the dongle (it appears as the
   bootloader device), add the recovery image from step 2, and **Write**. The
   progress is shown in the app.
6. **Done.** When the write completes the dongle reboots into the new firmware.
   A USB write installs the full image directly, so the test / confirm stage used
   for BLE updates does not apply here - there is nothing further to confirm.

If Programmer does not detect the dongle, re-seat the USB connection and press
reset again to re-enter the bootloader; the LED should pulse each time the
dongle is in bootloader mode.

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
