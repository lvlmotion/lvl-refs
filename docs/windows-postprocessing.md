---
title: Post-processing a Recording
parent: LEVEL Collector for Windows
description: the Postproc tab - opening and plotting the last take, and putting every system on the PC clock with Align
nav_order: 5
---

# Post-processing a Recording

The **Postproc** tab works on takes you have already recorded. It has two
parts: a shortcut to the last take, and **Align to PC clock**, which puts the
other systems' data on the same clock as the LEVEL sensors.

<p style="color:#FF3B30;font-size:1.3em"><strong>TODO SCREENSHOT: Postproc tab with the Last session row and the Align to PC clock table holding a few takes</strong></p>

## Last session

The take you recorded last is named at the top of the tab.

- **Open folder** opens its session folder in Explorer.
- **Plot** draws the take's sensor data and opens the first figure. It needs
  the plotting setup from the [Settings](windows-settings) page; until that is
  done the button is off and a note says so.

## Align to PC clock

Every system records on its own clock. The LEVEL sensor files are already on
the PC clock when the take starts; Sony clips, Theia motion files, Vicon frames
and the Polar strap are not. **Align to PC clock** maps each of them onto the
PC clock and writes the result beside the raw data, under
`aligned\<take>\` in the root folder's `collector` folder (by default
`C:\lvlmotion\collector\aligned\`). The raw session folder is never changed.

The table has one row per take, and inside it one line per system that is on
in **Settings > Sync** (LEVEL sensors always; Theia comes with Sony). Each line
has a **Raw** and an **Aligned** cell side by side. **Raw** is what is on disk
for the take: the folder, then the file names (for Sony, every camera's clip of
the take, with the LTC camera's marked `(LTC)`). **Aligned** is what the last
run wrote, the same way: green when it worked, with the method, the number of
frames or files and the fit error, and red with the reason when it did not. A
system with nothing shows `—`. Once a run has written its report, a
**Report** line shows `pc_alignment.json`.

Under each take's name, **Raw** and **Aligned** draw a quick plot of the take
(the systems on their recorded times, or on the PC clock after a run), save it
under `collector\images\` in the root folder and open it. They need the plotting
setup from the [Settings](windows-settings) page.

1. Each take is added to the table by itself when it finishes. To fill the
   table from disk instead, press **Enumerate**. It lists every take under
   `data\`, then earlier camera-only runs under `aligned\`, then (with Sony
   on) matches the clips in the Sony video folder to those takes by start
   time (a Theia trial folder by its first clip). The order is fixed, so the table
   comes out the same every time.
2. If you use Sony cameras, get the clips into the Sony video folder first:
   **Pull all clips** on the Collect tab does it and refreshes this table by
   itself; clips copied in by hand are picked up by **Enumerate**.
3. Tick the takes to process (the box in the header ticks or unticks them
   all), then press **Run on ticked**. The takes run in order; a running take
   says so in its row. You cannot run while a take is recording ("stop the
   take to run").
4. Read the **Aligned** column. Green is done, with the files written and the
   method used. Red is a failure, with the reason under it. Lines under the
   whole row add what the run found for that take: red ones are warnings to
   act on (for example Sony video that does not line up with the take), grey
   ones are notes (for example how long the LTC signal gapped during the take).

The tick box above the table, **Sony: use the current K_av calibration
instead of the one each take recorded**, matters only for Sony and is off each
time the Collector opens: each take is aligned with the LTC calibration saved
when it was recorded. See the
[Sony page](windows-sony-theia#post-processing).

**Clear table** empties the table (nothing on disk changes); **Enumerate**
fills it again.

What the run does for each system, and the files it writes, is on that
system's page:

| System | What Align writes | Details |
|---|---|---|
| LEVEL sensors | nothing for short takes; a drift-corrected copy for takes of 5 minutes or longer | [LEVEL Sensors](windows-level-sensors#post-processing) |
| Polar H10 | ECG, accelerometer and heart-rate files with a PC-time column | [Polar H10](windows-polar-h10#post-processing) |
| Sony and Theia | the PC time of every video frame (one file per camera of the take), and of every Theia frame; pulls the LTC camera's clip first if needed | [Sony Cameras and Theia](windows-sony-theia#post-processing) |
| Vicon | the PC time of every Vicon frame, covering a Nexus C3D's frame range | [Vicon](windows-vicon#post-processing) |

Every run also writes `pc_alignment.json` in the take's aligned folder, with
the result and any warnings for each system.

## If something goes wrong

- **Run on ticked is off:** nothing is ticked, a run is already going, or a
  take is recording.
- **A take is missing from the table:** press **Enumerate**. Takes recorded by
  another PC, or moved, are found the same way as long as they are under
  `collector\data\` in the root folder.
- **The batch did not line something up:** use **Align one folder** under the
  table. It is separate from the table: pick one system's folder with
  **Browse…** (a take's folder for IMU, Vicon or Polar; a folder of clips for
  Sony), then press **Align to PC clock** on that row. It runs the same
  alignment on just that folder, writes to the same `aligned\<folder>` place,
  and shows only that system's result. A folder of Sony clips is aligned clip
  by clip from the LTC in each one.
- **An Aligned cell is red:** the reason is under it, and the system's page has
  the fixes. The other systems in the same take are still aligned.
- **The Sony line shows a different method than you expected:** the
  [Sony page](windows-sony-theia#post-processing) explains the three methods,
  and its [FAQs](windows-sony-theia#faqs) how to get the best one.
- **You need help from LEVEL:** press **Package for support**. It copies the
  ticked takes (or, with none ticked, the last one), their aligned folders, the
  logs, the settings and the `calibration` folder into a new folder under
  `collector\support\` in the root folder, and opens it. Nothing is uploaded and
  nothing in the recordings changes. Tick **include video clips** to add the
  clips too (hundreds of MB each). Send us that folder.
