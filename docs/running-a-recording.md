---
title: Running a Recording
parent: LEVEL Collector for Windows
description: a take with sensors, Polar, Sony and Vicon together, and how the streams are lined up on one clock
nav_order: 2
---

# Running a Recording

## Turn on the systems you are using

**Settings > Sync** lists every system. Tick the ones you use (Polar H10, Sony,
Vicon) and pick which one **starts** a take (the master). Usually the Collector
is the master: **Start Stream** on the Collector starts everything. Each system's
own setup is on its page: [LEVEL Sensors](windows-level-sensors.html),
[Polar H10](windows-polar-h10.html), [Sony Cameras and Theia](windows-sony-theia.html),
[Vicon](windows-vicon.html).

<!-- screenshot: Settings > Sync table with Polar, Sony and Vicon on, Collector as master -->

## A take, step by step

1. **Scan All** (top of the window). It finds the sensors and the Polar strap and
   readies the Sony cameras. Pick what you want in each section.
2. **Connect All.** The sensors connect and the Polar strap starts its warm-up
   (about 30-40 seconds), so connect a minute before you start.
3. Check the **status sidebar**: green or yellow for everything you need. Polar
   turns green once its ECG is live.
4. Type a **Trial Name** (it names the session folder) and any **Notes**.
5. Press **Start Stream**. The Collector starts the sensors, Polar, the Sony
   cameras and Nexus together.
6. Do **3 hops** at the start and end of the take. They show up in every system
   and make a quick visual check of the alignment easy.
7. Press **Stop**. Everything stops; the sensors stay connected for the next
   take.

<!-- screenshot: footer with Trial Name, Notes and Start Stream; sidebar all green while recording -->

**Other ways to start a take:** if Nexus or the Sony webapp is set as the master
in Settings > Sync, start the capture there instead; the Collector follows and
starts the other systems. The sidebar diagram always shows which system starts
the take.

If a system fails mid-take, its sidebar card turns red and the others keep
going. Stop when you are ready. If the cameras are still recording when no take
is running, the main button still reads **Stop Stream** and stops them.

## Where the files go

Each take is a folder under `LEVEL_Sensor\data\` in your user folder, named
`<date>_<time>-<trial name>`:

| Written | Files |
|---|---|
| During the take | one sensor file per sensor; Polar ECG, accelerometer and heart-rate files |
| At Stop | session details and quality summary; the Sony and Vicon timing records |
| After post-processing | the pulled camera clip and an `aligned` folder |

What each system writes is listed on its page.

## How time alignment works

Every system keeps its own clock. The Collector puts them all on **the PC's
clock**, then post-processing uses those records to line everything up:

- **LEVEL sensors** share one clock, driven by a time beacon through the LEVEL
  Hub, so they agree with each other to a few milliseconds. The arrival time of
  every packet at the PC is saved too, which ties the sensors' clock to the PC's.
- **Polar H10** samples carry the strap's own timestamps, and the PC's arrival
  time is saved next to each one.
- **Vicon**: while Nexus is capturing, the Collector reads Vicon's live data and
  saves each Vicon frame number with the PC time it arrived. Anything Nexus
  records on its own frames (markers, force plates) can then be placed on the
  PC clock.
- **Sony cameras** stamp every video frame with timecode from the control
  box's clock, and the Collector saves that clock next to the PC's during every
  take. For the tightest timing, the Collector also plays a timecode audio
  signal (LTC) into one camera's audio input, generated from the PC clock, so
  the clip itself carries PC time.

Because each system's timing is saved in its own form, a short
**post-processing** step converts everything to the PC clock:
**Postproc > Align to PC clock**. Every finished take is added to its table;
tick the takes and press **Run on ticked**. Each external system gets a file
with a PC-time column in the take's `aligned` folder, and
`pc_alignment.json` says which method each one used and how well it fitted. The
sensor files are already on the PC clock and are not changed.
