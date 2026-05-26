---
title: Race Control
description: Reference for the RaceControl object — official messages broadcast by the FIA during a session.
---

# Race Control

`RaceControl` is the feed of official messages from the FIA during a
session: flags, safety cars, DRS status, penalties, investigations,
and post-race notes. One record is one message.

These messages are the narrative spine of a race — knowing *when* a
safety car came out, *which sector* had a yellow flag, or *which
driver* picked up a 5-second penalty is what turns a stream of lap
times into a story.

## Fields

| Field            | Type           | Meaning |
| ---------------- | -------------- | ------- |
| `date`           | string         | Timestamp of the message, ISO 8601 UTC. |
| `session_key`    | int            | The session this message belongs to. |
| `meeting_key`    | int            | The race weekend. |
| `lap_number`     | int            | Lap on which the message was issued. |
| `category`       | string         | Message type. See *Categories* below. |
| `flag`           | string         | Flag colour. See *Flags* below. Empty/unused if the message isn't a flag. |
| `scope`          | string         | What the message applies to: `"Track"`, `"Sector"`, or `"Driver"`. |
| `sector`         | int \| null    | Track sector (1, 2, or 3) for local flags. `null` for track-wide messages. |
| `driver_number`  | int \| null    | Affected driver. `null` for track-wide messages. |
| `message`        | string         | Full message text, as written by race control. |

## Categories

| Category     | What it covers |
| ------------ | -------------- |
| `Flag`       | Yellow, double yellow, red, green, blue flags. |
| `SafetyCar`  | Safety car or virtual safety car deployed/ending. |
| `Drs`        | DRS detection or activation zones opened or closed. |
| `Other`      | Penalties, investigations, post-race decisions, miscellaneous notes. |

## Flags

| Flag            | What it means |
| --------------- | ------------- |
| `GREEN`         | Normal racing conditions resumed. |
| `YELLOW`        | Danger ahead in this sector — no overtaking. |
| `DOUBLE YELLOW` | Greater danger — slow down, be prepared to stop. |
| `RED`           | Session stopped. |
| `BLUE`          | Faster car catching up — let it pass. Used for backmarkers in the race, and during practice/qualifying when a driver on an out-lap is being caught by a flying-lap car. |

## Sample record

```json
{
  "category": "Flag",
  "date": "2023-09-17T13:00:00.000000+00:00",
  "driver_number": null,
  "flag": "GREEN",
  "lap_number": 1,
  "meeting_key": 1219,
  "message": "GREEN LIGHT - PIT LANE OPEN",
  "scope": "Track",
  "sector": null,
  "session_key": 9165
}
```

## Null `driver_number`, null `sector`

- A track-wide event (a red flag stopping the session, a safety car
  deployed for the whole circuit) has `driver_number = null` and
  `sector = null`. It applies to everyone.
- A local yellow flag will have `scope = "Sector"` and `sector` set
  to 1, 2, or 3 — but still `driver_number = null`, because the flag
  applies to the part of the track, not to one driver.
- A penalty record (`category = "Other"`) will have the driver set:
  `driver_number = 44`, `message = "CAR 44 (HAM) 5 SECOND TIME PENALTY"`.
