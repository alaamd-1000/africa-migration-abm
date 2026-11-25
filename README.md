# Internal Migration Flow Simulation in NetLogo

An agent-based simulation model built in **NetLogo** using internal migration flow data from `cleaned_migration_flows.csv`. The model represents geographical origins and destinations as weighted network nodes (`zones`), migration corridors as directed links (`PrdMIG`, `dist_km`, `mig_rate_per_1k`, `size_tier`), and migrating individuals as mobile agents (`migrants`) tracked over a 10-step (`Year`) horizon.

## Dataset Overview (`cleaned_migration_flows.csv`)

- **Total Migration Flows (Rows):** 32,116 directed origin–destination records
- **Countries (`ISO`):** 46 countries (including top total flow contributors such as `NGA`, `UGA`, `KEN`, `CMR`, and `SEN`)
- **Geographical Zones:** 971 unique `(ISO, zone_id)` zones mapped from `LONFR`/`LATFR` and `LONTO`/`LATTO`
- **Migration Volume (`PrdMIG`):** Ranges from `2.19` to `85,431.00` (total across dataset: `~22,091,209.87`)
- **Travel Distance (`dist_km`):** Ranges from `2.30 km` to `2,029.91 km`
- **Flow Size Tiers (`size_tier`):**
  - `Small (<250)`: 15,674 links
  - `Medium (250-1k)`: 11,118 links
  - `Large (1k-5k)`: 4,820 links
  - `Mega (>5k)`: 504 links

## Project Structure

- `migration_sim.nlogo` — NetLogo model containing the interface widgets and simulation code
- `cleaned_migration_flows.csv` — Input dataset of cleaned migration flows and spatial attributes
- `README.md` — Model documentation and setup guide

## Requirements

- **NetLogo** (with the `csv` extension enabled; `extensions [ csv ]` is declared in the code)
- Place `cleaned_migration_flows.csv` in the same directory as the `.nlogo` model file (or select it via the file dialog if prompted during `setup`)

## Interface Controls & Plots

- **Sliders:**
  - `number-of-agents` — Number of migrant agents spawned at setup (default in UI: `3300`)
  - `migration-rate` — Multiplier controlling movement probability per step (default in UI: `1.00`)
- **Buttons:**
  - `Setup` (`setup`) — Loads the CSV data, builds zones and links, spawns migrants, resets ticks, and updates plots
  - `Go` (`go`) — Advances the simulation step by step (or continuously when **Forever** is enabled) up to `ticks >= 10`
  - `simulation-summary` (`simulation-summary`) — Prints key simulation metrics to the Command Center
  - `network-summary` (`network-summary`) — Prints link counts, flow sums by `size_tier`, and mean link distance
  - `show-all-countries` (`show-all-countries`) — Toggles visibility of migration flow links in the view
- **Plots (X-axis `Year` from `0` to `10`):**
  - `Moving Agents` — Tracks agents currently in motion (`count migrants with [ moving? ]`)
  - `Migration Activity` — Tracks movements initiated in the current step (`last-step-movements`)
  - `Average Travel Distance` — Tracks mean trip distance (`dist_km`) for movements started in the current step (`last-step-distance`)

## Optional Country Filtering via Command Center

By default, the model simulates all countries (`active-iso = "ALL"`). To filter by a specific ISO country code from the Command Center:

```netlogo
set-country "NGA"
