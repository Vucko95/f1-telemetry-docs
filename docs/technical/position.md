---
title: Position
description: Reference for the Position object — discrete position updates for each driver throughout a session.
---

# Position

`Position` is the running order of the race. One record is one
update: at this moment in time, this driver was in this position.
Records are emitted throughout a session — often, but not only,
when the order changes.

`Position` is discrete. It tells you who is in 1st, 2nd, 3rd …
20th — but not by how much. For the time gaps between drivers, see
[Intervals](intervals.md).

## Fields

| Field           | Type   | Unit / Range | Meaning |
| --------------- | ------ | ------------ | ------- |
| `date`          | string | ISO 8601 UTC | Timestamp of this update. |
| `session_key`   | int    | —            | The session this record belongs to. |
| `meeting_key`   | int    | —            | The race weekend. |
| `driver_number` | int    | 1–99         | Driver this update applies to. |
| `position`      | int    | 1–20         | Current race position (1 = leader). |

## Sample record

```json
{
  "date": "2023-09-17T13:10:05.123000+00:00",
  "driver_number": 1,
  "meeting_key": 1219,
  "position": 1,
  "session_key": 9165
}
```
