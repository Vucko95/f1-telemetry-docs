---
title: Starting Grid
description: Reference for the StartingGrid object — the grid order for a race.
---

# Starting Grid

`StartingGrid` is the official grid order for a race. One record per
driver, mapping a `driver_number` to a `grid_position`. Position 1 is
pole; the highest position is the back of the grid.

The grid order is **not always the same as the qualifying result**.
After qualifying, the FIA may apply penalties — typically grid-drop
penalties from earlier sessions, or component-change penalties for
exceeding the season's allocation of engines and gearboxes. Those
penalties are baked into the grid; `StartingGrid` reflects the order
the cars actually lined up in on Sunday.

This object is in *beta* in the OpenF1 API.

## Fields

| Field            | Type   | Meaning |
| ---------------- | ------ | ------- |
| `session_key`    | int    | The race session this grid belongs to. Race-only — there is no grid for practice or qualifying. |
| `meeting_key`    | int    | The race weekend. |
| `driver_number`  | int    | Driver. |
| `grid_position`  | int    | Starting slot, 1 = pole, increasing toward the back of the grid. |

## Sample record

```json
{
  "driver_number": 55,
  "grid_position": 1,
  "meeting_key": 1219,
  "session_key": 9165
}
```

That record is Sainz on pole for the 2023 Singapore Grand Prix.
