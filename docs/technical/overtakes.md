---
title: Overtakes
description: Reference for the Overtakes object — records of one driver passing another on track.
---

# Overtakes

`Overtakes` records on-track passing moves. One record is one
overtake: the lap, the timestamp, the driver who made the move, and
the driver who got passed.

This object is in *beta* in the OpenF1 API. Coverage is generally
good for the obvious moves, but light contact, swaps under safety-car
restarts, and very tight battles may be miscounted or missed.

## What counts as an overtake

`Overtakes` records **on-track passes only**. A position change that
happens because one driver pits and the other doesn't will move them
in the running order, but it is *not* an overtake and will *not*
appear here. For pit-stop-driven swaps, look at [Position](position.md)
combined with [Pit](pit.md).

## Fields

| Field                       | Type   | Meaning |
| --------------------------- | ------ | ------- |
| `date`                      | string | Timestamp of the move, ISO 8601 UTC. |
| `session_key`               | int    | The session this overtake belongs to. |
| `meeting_key`               | int    | The race weekend. |
| `lap_number`                | int    | Lap on which the overtake happened. |
| `overtaking_driver_number`  | int    | Driver who completed the pass. |
| `overtaken_driver_number`   | int    | Driver who was passed. |

## Sample record

```json
{
  "date": "2023-09-17T14:05:30.123000+00:00",
  "lap_number": 15,
  "meeting_key": 1219,
  "overtaken_driver_number": 4,
  "overtaking_driver_number": 63,
  "session_key": 9165
}
```

That record is Russell (63) passing Norris (4) on lap 15 of the 2023
Singapore Grand Prix.
