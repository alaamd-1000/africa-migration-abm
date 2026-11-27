# Africa Internal Migration – Agent-Based Model (NetLogo)

An exploratory agent-based simulation of **internal migration across 46 African countries**, built in NetLogo from a dataset of 32,116 origin–destination flows between 971 zones.

![Simulation screenshot](images/screenshot.png)

> **Status:** exploratory / educational. Movement probabilities and trip durations are modelling assumptions. They have **not** been calibrated or validated against observed outcomes. See [Limitations](#limitations).

## What the model does

- **Zones** (nodes) are the 971 geographical units; **links** are the 32,116 directed flows (`PrdMIG`), coloured by size tier: Small (<250), Medium (250–1k), Large (1k–5k), Mega (>5k).
- **Agents** (`number-of-agents`, default 3,400) are placed on zones with probability proportional to each zone's total outflow.
- **Each tick (≈ one simulated year)** a stationary agent may start a trip. The probability grows with the outflow of its current zone and is scaled by `migration-rate`.
- **Destination choice:** proportional to the flow on each outgoing link.
- **Trips** last 2–5 ticks, depending on distance, and move in a straight line. On arrival the agent settles in the destination zone.
- The simulation runs for **10 ticks** and stops.

## Interface

| Widget | Purpose |
|---|---|
| `number-of-agents` (slider) | Number of simulated agents |
| `migration-rate` (slider) | Multiplier on the per-tick probability of starting a trip |
| `Setup` | Loads the CSV, builds zones/links, creates agents (do **not** set to *Forever*) |
| `Go` | Runs the simulation (*Forever*), stops automatically at year 10 |
| `show-all-countries` | Toggles all 32k links (slow to draw) |
| `show-top-links` *(optional button)* | Shows only the 500 strongest links |
| `network-summary` | Prints link counts and flow totals per tier |
| `simulation-summary` | Prints movements and distances so far |
| `Record Video` | Runs a full simulation and saves `africa_migration.mp4` next to the model (uses NetLogo's `vid` extension) |

Plots (X axis = Year, 0–10): **Moving Agents**, **Migration Activity** (new trips per year), **Average Travel Distance** (km, trips started in that year).

To focus on one country, run in the Command Center:

```
set-country "NGA"
```

## Requirements

- **NetLogo 7.x** (model file: `africa_model.nlogo.nlogox`)
- Extensions used (all bundled with NetLogo): `csv`, `table`, `rnd`, `vid`
- `cleaned_migration_flows.csv` placed **next to the model file**, or in a `data/` folder (the model also looks one folder up and otherwise opens a file dialog)

## How to run

1. Open `africa_model.nlogo.nlogox` in NetLogo.
2. Make sure the CSV is in the same folder (or in `data/`).
3. Press **Setup**, then **Go**.

## Data

`cleaned_migration_flows.csv` columns used: `ISO`, `origin_id`, `dest_id`, `LONFR`, `LATFR`, `LONTO`, `LATTO`, `PrdMIG`, `dist_km`, `ref_population`, `mig_rate_per_1k`, `size_tier`.

- 32,116 directed flows, 46 countries, 971 zones
- `PrdMIG` ranges from about 2 to 85,431 per flow
- `dist_km` ranges from about 2 km to 2,030 km

**Source and license:** TODO – add the original data source, citation and license here before publishing.

## Limitations

- Flows are fixed: there is no feedback such as congestion, employment or capacity.
- Agents have no memory, never return home and do not interact.
- A tick is treated as one year, and trip durations of 2–5 ticks are design choices, not estimates from the data.
- All agents start stationary, so the first years show a **warm-up** peak in activity before the system settles. This comes from the model's initial conditions, not from real migration behaviour.
- Choosing destinations in proportion to flow favours high-volume corridors, so average simulated trips are not the same as the average corridor in the data.
- Results depend on random draws; no fixed seed is set yet.

## Roadmap

- Add `random-seed` for reproducible runs
- Calibrate movement probabilities against observed data and validate the results
- Add return migration and capacity or attractiveness effects

## License

Code: add a license (e.g. MIT). Data: see the data section above.
