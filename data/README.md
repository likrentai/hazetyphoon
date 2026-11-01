# Data for the two globes

Made by `12webdata.ipynb` from the project's processed data. Licence: CC BY 4.0 (credit this project and the original providers listed in the main README).

| File | What it holds |
|---|---|
| `event/`, `season/` | the Choi-wan event (28 Sep to 7 Oct 2026, every 3 hours, 80 steps) and the 2026 season (1 Aug to 25 Oct 2026, daily, 86 steps) |
| `smoke_NNN.png` | smoke PM2.5 near the ground (organic, brown and black carbon, NASA GEOS-FP), one transparent picture per step, north up; colour steps at 1, 2, 5, 10, 15, 25, 35, 55.5, 100 and 250 µg/m³, transparent below 1 |
| `wind.json` | short wind trails from ERA5 (event: 850 hPa; season: 10 m daily mean): `step_hours`, `level` and `trails`, each `[start_hours, [lon, lat, lon, lat, ...]]`. Contains modified Copernicus Climate Change Service information 2026 |
| `fires.json` | VIIRS fire hotspots from NASA FIRMS, counted per grid cell and day: `{"YYYY-MM-DD": [[lon, lat, count], ...]}` (event 0.1 degree, season 0.5 degree) |
| `meta.json` | times, map corners, colour legend, storm tracks from IBTrACS (`t_hours`, `lon`, `lat`, `wind_kt`) and the numbers shown in the side panel |

Hours are counted from `start` in `meta.json` (UTC).
