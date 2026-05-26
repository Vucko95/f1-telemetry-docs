---
title: Session Result
description: Reference for the SessionResult object — the final classification of a session.
---

# Session Result

`SessionResult` is the **official final classification** of a
session. One record per driver per session, populated after the
session ends, with the driver's finishing position, the gap to the
winner, any championship points awarded, and flags for non-finishes.

This object is in *beta* in the OpenF1 API — it may occasionally lag
behind the end of a session, and the underlying field set can change.

## Fields

| Field            | Type    | Meaning |
| ---------------- | ------- | ------- |
| `session_key`    | int     | The session this result belongs to. |
| `meeting_key`    | int     | The race weekend. |
| `driver_number`  | int     | Driver this record is for. |
| `position`       | int     | Final classified position (1 = winner). |
| `gap_to_leader`  | float   | Time behind the winner, in seconds. `0.0` for the winner themselves. |
| `points`         | int     | Championship points awarded for this session. |
| `dnf`            | boolean | `true` if the driver did not finish. |
| `dns`            | boolean | `true` if the driver did not start. |
| `dsq`            | boolean | `true` if the driver was disqualified. |
| `status`         | int     | FIA status classification code. |

## Sample record

```json
{
  "dnf": false,
  "dns": false,
  "driver_number": 55,
  "dsq": false,
  "gap_to_leader": 0.0,
  "meeting_key": 1219,
  "points": 25,
  "position": 1,
  "session_key": 9165,
  "status": 1
}
```

That record is Carlos Sainz winning the 2023 Singapore Grand Prix.

## Points (2023 system)

| Position | Points | Position | Points |
| -------: | -----: | -------: | -----: |
| 1st      | 25     | 6th      | 8      |
| 2nd      | 18     | 7th      | 6      |
| 3rd      | 15     | 8th      | 4      |
| 4th      | 12     | 9th      | 2      |
| 5th      | 10     | 10th     | 1      |

A driver finishing in the top 10 also receives **+1 point** for the
fastest lap of the race. Sprint races award a separate, smaller
points spread (8 down to 1 for the top 8).

## DNF, DNS, DSQ

| Field  | Meaning |
| ------ | ------- |
| `dnf`  | Did Not Finish — started the session but failed to be classified at the end (mechanical, crash, retirement). |
| `dns`  | Did Not Start — was entered for the session but did not take part. |
| `dsq`  | Disqualified — finished, but post-session was excluded from the results. |

A driver can still have a `position` and `points` if their `dnf` is
`true`: in F1, finishing 90 % of the race distance counts as
classified, so a late retirement may still leave the driver with
points and a position.
