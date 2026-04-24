# Transport Dataset

A collection of JSON instances for Profitable Full-Truckload Assignment and Driver Scheduling Problem (P-FTL-ADSP) with drivers and routes that include time windows, operational constraints, and vehicle attributes.

## What This Repository Contains

This repository includes many instances named as:

- `instance_<id>_<ndrivers>_<nroutes>_<variant>.json`

Example:

- `instance_10_100_200_loose.json`

Where usually:

- `<id>`: instance identifier (for example 10, 11, 12, ...).
- `<ndrivers>`: number of drivers (matches `body.ndrivers`).
- `<nroutes>`: number of routes/orders (matches `body.nroutes`).
- `<variant>`: type of time-window constraints (`loose` or `tight`).

## General Structure of Each File

Each instance has this shape:

```json
{
  "op": "solve",
  "body": {
    "currentime": "01/08/2023 01:00:00",
    "ndrivers": 100,
    "nroutes": 200,
    "ndays": 30,
    "npositions": 3,
    "drivers": [ ... ],
    "routes": [ ... ]
  }
}
```

### Main Fields in `body`

- `currentime`: planning reference date/time.
- `ndrivers`: expected cardinality of `drivers`.
- `nroutes`: expected cardinality of `routes`.
- `ndays`: time horizon of the instance.
- `npositions`: additional scenario parameter.
- `drivers`: list of resources (drivers) with availability, rest status, and driving-time tracking.
- `routes`: list of routes/orders with cost, duration, and load/unload time windows.

### Common Fields in `drivers`

- availability windows: `available_1`, `available_2`.
- driving-time tracking: `driven_hours_today`, `remain_driven_hours_today`, `driven_hours_since_rest`.
- rest-related values: `end_date_last_weekly_rest`, `current_driven_hours_block`, `current_start_date_block`, `next_rest`.
- remaining time budgets: `remaining_driving_time`, `remaining_rest_time`, `remaining_total_time`.
- initial time window at depot: `min_unload_t0`, `max_unload_t0`.
- `tstart`: list of feasibility data per route, each entry containing `codeorder`, `cost`, `time`, `min_load`, `max_load`, `min_unload`, `max_unload`.

### Common Fields in `routes`

- identifier: `codeorder`.
- time windows: `min_load`, `max_load`, `min_unload`, `max_unload`.
- metrics: `cost`, `time`, `profit`.
- operational values: `num loads`, `num unloads`, `time loads`, `time unloads`, `mandatory`, `links`.

## `loose` vs `tight` Variant

- `loose`: scenarios with wider time windows and/or more relaxed constraints.
- `tight`: scenarios with stricter time windows and/or tighter constraints.

## Notes

- This repository is an input dataset.
