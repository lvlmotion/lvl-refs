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
`LEVEL_Collector\aligned\<take>\`. The raw session folder is never changed.

The table has one row per take. The **Raw** column lists what is on disk for
the take, one line per system that has something: the folder, then the file
names (for Sony, every camera's clip of the take, with the LTC camera's marked).
The **Aligned** column lists what the last run wrote the same way, green when it
worked and red with the reason when it did not. Systems with nothing are left
out of the cell.

1. Each take is added to the table by itself when it finishes. To fill the
   table from disk instead, press **Enumerate IMU folder**: it lists every take
   under `data\`.
2. If you use Sony cameras, get the clips into the Sony video folder: **Pull
   all clips** on the Collect tab does it and refreshes this table by itself.
   For clips copied in by hand, press **Enumerate Sony folder**. Either way
   each clip is matched to the take recorded at the same time, and a Theia
   trial folder to its clips.
3. Tick the takes to process, then press **Run on ticked**. The takes run in
   order; a running take says so in its row. You cannot run while a take is
   recording.
4. Read the **Aligned** column. Green is done, with the files written and the
   method used. Red is a failure, with the reason under it.

What the run does for each system, and the files it writes, is on that
system's page:

| System | What Align writes | Details |
|---|---|---|
| LEVEL sensors | nothing for short takes; a drift-corrected copy for takes of 5 minutes or longer | [LEVEL Sensors](windows-level-sensors#post-processing) |
| Polar H10 | ECG, accelerometer and heart-rate files with a PC-time column | [Polar H10](windows-polar-h10#post-processing) |
| Sony and Theia | the PC time of every video frame, and of every Theia frame; pulls the LTC camera's clip first if needed | [Sony Cameras and Theia](windows-sony-theia#post-processing) |
| Vicon | the PC time of every Vicon frame, covering a Nexus C3D's frame range | [Vicon](windows-vicon#post-processing) |

Every run also writes `pc_alignment.json` in the take's aligned folder, with
the result and any warnings for each system.

## If something goes wrong

- **Run on ticked is off:** nothing is ticked, a run is already going, or a
  take is recording.
- **A take is missing from the table:** press **Enumerate IMU folder**. Takes
  recorded by another PC, or moved, are found the same way as long as they are
  under `data\`.
- **An Aligned cell is red:** the reason is under it, and the system's page has
  the fixes. The other systems in the same take are still aligned.
- **The Sony column shows a different method than you expected:** the
  [Sony FAQs](windows-sony-theia#faqs) explain the three methods and how to
  get the best one.
