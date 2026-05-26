---
title: Pit
description: Reference for the Pit object — one record per pit lane visit.
---

# Pit

A `Pit` record describes one pit stop: which driver, on which lap, and
how long they spent in the pit lane in total.

`pit_duration` is **total pit-lane time**: the moment the car crosses
the pit-entry line until the moment it crosses the pit-exit line. It
covers slowing for the pit lane, the stationary stop (tire change,
adjustments), and accelerating back out. It does *not* break down the
stationary time on its own — public data doesn't expose that.

## Fields

| Field            | Type   | Unit / Range  | Meaning |
| ---------------- | ------ | ------------- | ------- |
| `date`           | string | ISO 8601 UTC  | Timestamp of the pit entry. |
| `session_key`    | int    | —             | The session this stop belongs to. |
| `meeting_key`    | int    | —             | The race weekend. |
| `driver_number`  | int    | 1–99          | Driver who pitted. |
| `lap_number`     | int    | 1–max laps    | Lap on which the stop happened. |
| `pit_duration`   | float  | seconds       | Total time spent in the pit lane (entry + stationary + exit). |

## Sample record

```json
{
  "date": "2023-09-17T13:45:00.000000+00:00",
  "driver_number": 55,
  "lap_number": 20,
  "meeting_key": 1219,
  "pit_duration": 24.5,
  "session_key": 9165
}
```

A `pit_duration` of around 20–30 seconds is typical for a race. Very
short values (under 20 s) are unusual; very long values (over 40 s)
usually indicate a problem — a wheel that wouldn't fit, a penalty
served, or a long repair stop.
