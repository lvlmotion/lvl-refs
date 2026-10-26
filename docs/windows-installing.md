---
title: Installing and Updating
parent: LEVEL Collector for Windows
description: installing the Collector, updates, and getting help
nav_order: 1
---

# Installing and Updating

For the latest installer, email [info@lvlmotion.com](mailto:info@lvlmotion.com).

## Installing

1. Run `LEVEL_Collector-<version>.exe`. It installs the Collector for every
   Windows account on the PC (in Program Files), so Windows asks for
   administrator permission. All accounts share the same settings, recordings
   and Python environment.
2. Open **LEVEL Collector** from the Start menu (under **LEVEL Motion**) or the
   desktop shortcut.

After installing, open **Settings** once: see [Settings](windows-settings) for
the Python setup (plotting, Polar, Sony and Vicon need it) and the sync table.

## Updating

- Run the new installer: it replaces the old version and keeps your settings,
  recordings and Python environment.
- Updating from an older version that kept its settings somewhere else (such as
  your user folder): nothing is carried over except an old LEVEL Python
  environment, which moves into `C:\lvlmotion\settings`. The Collector starts
  with its default settings, so set the root folder again, and press **Set up
  minimum/full environment** (it reuses the moved environment) or **Browse** to
  your Python (see [Settings](windows-settings)). Older recordings stay where
  they were.
- Versions before 0.1.34 were installed for one Windows account only. Uninstall
  such a version first (Settings > Apps), or both stay installed side by side.
- The **Help** tab shows the version at the top (also in the first lines of the **Logs** tab).
- If Windows refuses to install (the new version is not newer than the one
  installed), uninstall the old one first (Settings > Apps). Your settings and
  recordings are kept.

## Getting help

- The **Help** tab's **Open help site** button opens these guides.
- On the **Logs** tab, **Copy all** puts the whole log on the clipboard so you
  can paste it into an email to [info@lvlmotion.com](mailto:info@lvlmotion.com).
  The full log of each run is also saved as a file in the root folder's
  `collector\logs` folder (by default `C:\lvlmotion\collector\logs`); the
  **Logs** tab shows its exact path.
- On the **Postproc** tab, **Package for support** copies the last take (or the
  takes you ticked in the table), the logs and your settings into one new
  folder in the root folder's `collector\support` folder, ready to send to us.
  Video clips are left out unless you tick **include video clips**. Nothing is uploaded and
  your recordings are not changed.
