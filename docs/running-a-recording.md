---
title: Running a Recording
parent: LEVEL Collector for Windows
description: a take with every system you turned on, and where the files go
nav_order: 4
---

# Running a Recording

Set up first: [Setting Up for a Recording](windows-setting-up.html).

## A take, step by step

1. **Scan All** (top of the window). It finds or readies every system you turned
   on. Pick what you want in each section.
2. **Connect All.** Some systems take a moment to get ready after connecting;
   each system's page says what to expect.
3. Check the **status sidebar**: start when everything you need is green or
   yellow.
4. Type a **Trial Name** (it names the session folder) and any **Notes**.
5. Press **Start Stream**. The Collector starts every system you turned on
   together.
6. Press **Stop Stream**. Everything stops; the sensors stay connected for the
   next take.

![A take in progress: the footer with Trial Name, Notes, the elapsed time and Stop Stream; the sidebar all green](assets/running-a-recording/recording.png)


If a system fails mid-take, its sidebar card turns red and the others keep
going. Stop when you are ready. If the cameras are still recording when no take
is running, the main button still reads **Stop Stream** and stops them.

## Where the files go

Each take is a folder under `LEVEL_Collector\data\` in your user folder, named
`<date>_<time>-<trial name>`:

| Written | Files |
|---|---|
| During the take | one sensor file per sensor; Polar ECG, accelerometer and heart-rate files |
| At Stop | session details and quality summary; the Sony and Vicon timing records |
| After post-processing | `aligned\<take>\` beside `data\`, with every system's `*_pc.csv` |

What each system writes is listed on its page.
