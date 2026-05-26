---
title: Weather
description: Reference for the Weather object — meteorological conditions during a session.
---

# Weather

`Weather` is the meteorological feed for a session. One record is one
sample — air temperature, track temperature, wind, humidity, pressure,
and a binary rainfall flag — taken roughly every 60 seconds.

Track temperature is its own measurement, separate from air
temperature, because the tarmac heats up in the sun and cools at
night. It's typically **10–15 °C hotter than the air** in dry
conditions, which has a much bigger effect on tire behaviour than
air temperature alone.

## Fields

| Field                | Type   | Unit / Range  | Meaning |
| -------------------- | ------ | ------------- | ------- |
| `date`               | string | ISO 8601 UTC  | Timestamp of this sample. |
| `session_key`        | int    | —             | The session this record belongs to. |
| `meeting_key`        | int    | —             | The race weekend. |
| `air_temperature`    | float  | °C            | Ambient air temperature. |
| `track_temperature`  | float  | °C            | Track surface temperature. |
| `humidity`           | float  | 0–100 %       | Relative humidity. |
| `pressure`           | float  | mbar          | Atmospheric pressure. |
| `wind_speed`         | float  | m/s           | Wind speed. |
| `wind_direction`     | int    | 0–360 °       | Wind bearing. `0` / `360` = North, `90` = East, `180` = South, `270` = West. |
| `rainfall`           | int    | 0 or 1        | Rain indicator — `0` = dry, `1` = wet. **Not** an amount of rain. |

## Sample record

```json
{
  "air_temperature": 30.5,
  "date": "2023-09-17T13:05:00.000000+00:00",
  "humidity": 78,
  "meeting_key": 1219,
  "pressure": 1008.5,
  "rainfall": 0,
  "session_key": 9165,
  "track_temperature": 36.2,
  "wind_direction": 140,
  "wind_speed": 2.5
}
```

## Rainfall is binary

`rainfall` is `0` or `1` — it tells you whether it is raining, not how
hard. There is no public millimetres-per-hour figure. To detect when
the rain started or stopped, look for the timestamp where the
`rainfall` flag changes within a session.
