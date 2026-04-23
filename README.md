# Transport Dataset

A collection of JSON instances for Profitable Full-Truckload Assignment and Driver Scheduling Problem (P-FTL-ADSP) with drivers and routes that include time windows, operational constraints, and vehicle attributes.

## What This Repository Contains

This repository includes many instances named as:

- `instance_<id>_<ndrivers>_<nroutes>_<variant>.json`

Example:

- `instance_10_100_200_loose.json`

Where usually:

- `<id>`: instance identifier (for example 10, 11, 12, ...).
- `<ndrivers>`: number of drivers (matches `body.nconductores`).
- `<nroutes>`: number of routes/orders (matches `body.nrutas`).
- `<variant>`: type of time-window constraints (`loose` or `tight`).

## General Structure of Each File

Each instance has this shape:

```json
{
  "op": "solve",
  "body": {
    "horactual": "01/08/2023 01:00:00",
    "nconductores": 100,
    "nrutas": 200,
    "ndias": 30,
    "nposiciones": 3,
    "conductores": [ ... ],
    "rutas": [ ... ]
  }
}
```

### Main Fields in `body`

- `horactual`: planning reference date/time.
- `nconductores`: expected cardinality of `drivers`.
- `nrutas`: expected cardinality of `routes`.
- `ndias`: time horizon of the instance.
- `nposiciones`: additional scenario parameter.
- `conductores`: list of resources (drivers) with availability, rest status, and capabilities.
- `rutas`: list of routes/orders with cost, duration, and load/unload time windows.

### Common Fields in `conductores`

Some common fields:

- availability and time values: `disp_1`, `disp_2`, `horas_conducidas_dia_actual`, `horas_restantes_dia_actual`, `prox_descanso`.
- rest-related values: `fecha_fin_ultimo_descanso_semanal`, `bloque_horas_conducidas_actual`, `trest_conduccion`, `trest_descanso`, `trest_total`.
- vehicle capabilities/attributes: `basculante`, `bitemperatura`, `multitemperatura`, `dolly`, `rampa hidraulica`, etc.
- `tinicial`: matrix/list of initial times and costs per order.

### Common Fields in `rutas`

Some common fields:

- identifiers: `codexpediente`, `codigo`, `codpedido`.
- time windows: `min_carga`, `max_carga`, `min_descarga`, `max_descarga`.
- metrics: `coste`, `tiempo`, `beneficio`, `incremento`.
- operational values: `numero cargas`, `numero descargas`, `tiempo cargas`, `tiempo descargas`, `obligatoria`, `aleatorio`, `enlaces`.
- vehicle/equipment requirements: `monocuba`, `multicompartimento`, `portabobinas`, `usa ganchos`, etc.

## `loose` vs `tight` Variant

- `loose`: scenarios with wider time windows and/or more relaxed constraints.
- `tight`: scenarios with stricter time windows and/or tighter constraints.

## Notes

- This repository is an input dataset.
