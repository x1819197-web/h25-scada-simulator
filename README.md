# H25 Gas Turbine Generator — UNIT-20 | SCADA Simulator

Pixel-perfect, 1:1 replica of the **DIASYS Netmation SCADA** system with a coupled
**real-time physics engine (10 Hz)** for the Honeywell / Hitachi / Mitsubishi
**H25 (C32 model) Gas Turbine Generator — UNIT-20**.

Zero-dependency — just open `index.html` in any modern browser.
Live demo via GitHub Pages: `https://<username>.github.io/<repo>/`

## Run locally

Double-click `index.html` — no build step, no server required.

## Startup sequence (test it)

1. `AUX START` — MOP, vent fans, JOP start, lube header → 0.49 MPa
2. `CRANK` — 0 → 2000 rpm (requires `READY TO START`)
3. `FIRE` — ignition, ramp → 7260 rpm / 50 Hz (`FSNL`)
4. `SYNC 52G` — breaker closes, synchronize to grid
5. `LOAD +` — raise to ~28.5 MW (FOFFD ~65%, exhaust ~594 °C)

## Screens (19)

START-UP · FFD CONTROL · SYNCHRO & EXC OPE · FUEL GAS · LUBE OIL · GENERATOR ·
VENTILATION · IBH CONTROL · MOTORS (13 aux motors) · BEARING OIL ·
EXHAUST (18-TC polar radar) · VIBRATION · WHEELSPACE · START CHECK 0–7 ·
TIMERS · TRIP MONITOR · DATA REPORT 1 & 2 · OVERSPEED

## Physics engine

| Model | Formula / logic |
|---|---|
| Shaft speed | 0 → 2000 crank → 7260 rpm (50 Hz), coast-down on trip |
| Power | P = √3·V·I·cosφ / 1000 (10.92 kV × 1515 A × 0.99 ≈ 28.4 MW) |
| Exhaust | T = 25 + 6·Fuel + 44.5·N/1000 − 1.7·IGV ± 15 °C spread |
| CPD | 1.30·(N/7260)²·(0.35 + 0.65·IGV/82.7) MPa |
| Lube oil | 0 → 0.49 MPa on MOP/EOP |
| Auto-trips | lube < 0.1 MPa · vib > 100 um · Texh > 620 °C · speed > 7788 rpm · flame loss |

## Deploy (GitHub Pages)

Settings → Pages → Deploy from branch → `main` / `/ (root)` → open the Pages URL.
