# Smoke in the Typhoon Zone: the 2026 Indonesian haze reaches the western Pacific

On 3 October 2026 a trail of smoke from the Indonesian fires could be seen on earth.nullschool.net curling into **Super Typhoon Choi-wan** in the Philippine Sea. This project follows the haze from the fires to the zone where Pacific typhoons form and travel, with two animated globes and thirteen Python notebooks built on open model, satellite and ground data.

- **Map globe** (works on phones): https://likrentai.github.io/hazetyphoon/
- **3D globe** (desktop only): https://likrentai.github.io/hazetyphoon/cesium.html
- **Case study**: https://likrentai.github.io/hazetyphoon/case-study.html (also as a [PDF](https://likrentai.github.io/hazetyphoon/case-study.pdf))

The point is the scale and reach of the haze, not a claim that smoke changes typhoons.

## Two parts

1. **Direct export**: how much smoke typhoons pull out of eastern Indonesia into the open Pacific, in the Choi-wan event, the 2026 season and every season since 2003.
2. **Indirect effect**: whether the same storms change the haze over Sumatra, Kalimantan, Kuala Lumpur and Singapore.

## Main findings

| Finding | Figure |
|---|---|
| Smoke in the Pacific corridor (128 to 150 E, 3 to 18 N), August to September | 2026 is 1st of 24 seasons since 2003: 1.94 µg/m³, against 1.14 in 2015 (NASA MERRA-2) |
| Smoke flowing into the corridor from the south on typhoon days | +29% in 24 seasons (+158 t/day, 95% range 29 to 288); +80% in El Niño seasons |
| Corridor under smoke during the Choi-wan event | 1.1 million km² on 29 September to 2.7 million km² on 6 October |
| Where the storm's air came from (850 hPa trajectories) | 47% of parcels from eastern Indonesia reached the corridor; 24% from Kalimantan; none from Sumatra |
| Smoke over Sumatra on typhoon days | -7%; no clear change in Kalimantan, Kuala Lumpur or Singapore |
| People in unhealthy fire smoke on the worst day | Indonesia 17 to 45 million, Malaysia 3.7 to 19 million, all of Singapore |

"Smoke" means organic, brown and black carbon in the models, not total PM2.5: near a typhoon most fine particles are sea salt. A **typhoon day** is a day with a storm of at least 64 knots in the Philippine Sea box (120 to 150 E, 5 to 25 N). GEOS-FP reads about 1.8 times higher than Singapore's official monitors, so exposure figures are given as a range.

## What is in the repository

```
00setup.ipynb          account and connection tests (NASA Earthdata, Copernicus, FIRMS, OpenAQ, data.gov.sg)
01event.ipynb          downloads for the Choi-wan event, 28 Sep to 7 Oct 2026 (GEOS-FP, CAMS, ERA5, FIRMS)
02eventmaps.ipynb      event maps, smoke versus sea salt, smoke area and distance to the storm, animation
03trajectories.ipynb   air trajectories forward from the fire regions and backward from the storm
04export.ipynb         smoke budgets for each region: inflow, outflow, storage and removal
05season.ipynb         downloads for the season, 1 Aug to 25 Oct 2026 (GEOS-FP, ERA5, FIRMS, tracks)
06season.ipynb         the season: typhoon days, smoke by region, difference maps, animation
07exposure.ipynb       people exposed to smoke (WorldPop), four versions of the calculation
08groundcheck.ipynb    model against ground monitors (Singapore NEA, OpenAQ)
09tracks.ipynb         typhoon tracks since 2003 (IBTrACS), typhoon days, El Niño and IOD indices
10merra2.ipynb         daily MERRA-2 aerosol for every August to October since 2003
11climatology.ipynb    the long record: seasons ranked, typhoon-day effects, arrival composite
12webdata.ipynb        the small files the two globes load (docs/data)
docs/index.html        map globe: MapLibre GL JS with deck.gl
docs/cesium.html       3D globe: CesiumJS
docs/case-study.html   case study (and case-study.pdf, fonts/, images/)
docs/data/event/       Choi-wan event: 80 smoke pictures (3-hourly), wind trails, fires, storms and numbers
docs/data/season/      2026 season: 86 smoke pictures (daily), wind trails, fires, storms and numbers
requirements.txt       Python packages
```

The downloaded and processed data (`data/`, several GB) and the private keys (`config/keys.toml`) are not in the repository; the notebooks download the data again.

## Run it yourself

The pages are static files. To view them on your own computer:

```
cd docs
python -m http.server 8000
```

then open http://localhost:8000 (map globe) or http://localhost:8000/cesium.html (3D globe). Each page has a SETTINGS block at the top (lines marked `// <-`) for speed, colours and camera.

The 3D globe uses Cesium ion imagery (Bing Maps aerial) and needs a Cesium ion access token in `ionToken`. The token in this repository only works on https://likrentai.github.io. For your own copy, make a free token at https://ion.cesium.com, or set `imagery: "bluemarble"` or `"naturalearth"`, which need no account.

To rebuild the data, make an environment with Python 3.12 and run the notebooks in order:

```
uv venv --python 3.12
uv pip install -r requirements.txt
```

You need free accounts for NASA Earthdata, NASA FIRMS (map key), the Copernicus Climate and Atmosphere Data Stores, OpenAQ and data.gov.sg. Put the keys in `config/keys.toml` (sections `[firms]`, `[cds]`, `[ads]`, `[openaq]`, `[datagovsg]`); `00setup` explains each one and tests the connections.

## Credits and sources

- **Smoke and aerosols**: NASA Global Modeling and Assimilation Office (GMAO), GEOS-FP and MERRA-2 (M2T1NXAER). Gelaro, R. and others (2017), The Modern-Era Retrospective Analysis for Research and Applications, Version 2 (MERRA-2), J. Climate 30, 5419 to 5454. Buchard, V. and others (2016), Evaluation of the surface PM2.5 in Version 1 of the NASA MERRA Aerosol Reanalysis over the United States, Atmos. Environ. 125, 100 to 111.
- **Second model**: Copernicus Atmosphere Monitoring Service (CAMS) global forecasts. Contains modified Copernicus Atmosphere Monitoring Service information 2026.
- **Winds**: ERA5, Copernicus Climate Change Service (Hersbach, H. and others 2020, Q. J. R. Meteorol. Soc. 146, 1999 to 2049). Contains modified Copernicus Climate Change Service information 2026.
- **Fires**: NASA Fire Information for Resource Management System (FIRMS), VIIRS active fires.
- **Typhoon tracks**: IBTrACS, NOAA National Centers for Environmental Information. Knapp, K. R. and others (2010), The International Best Track Archive for Climate Stewardship (IBTrACS), Bull. Amer. Meteor. Soc. 91, 363 to 376.
- **Population**: WorldPop (www.worldpop.org), 2020, 1 km (CC BY 4.0).
- **Ground monitors**: Singapore National Environment Agency through data.gov.sg (Singapore Open Data Licence); OpenAQ (https://openaq.org) with AirGradient community sensors.
- **Climate indices**: NOAA Climate Prediction Center (Oceanic Niño Index) and NOAA Physical Sciences Laboratory (Dipole Mode Index).
- **Boundaries**: Natural Earth (public domain).
- **Map globe imagery**: NASA Global Imagery Browse Services (GIBS), Blue Marble Shaded Relief and Bathymetry. https://www.earthdata.nasa.gov/gibs
- **3D globe imagery and globe**: CesiumJS and Cesium ion (https://cesium.com), with Bing Maps aerial imagery from Microsoft via Cesium ion.
- **Inspiration**: earth.nullschool.net by Cameron Beccario.
- **Related work**: Reid, J. S. and others (2025), Atmos. Chem. Phys. 25, 18639, on smoke reaching the Philippines with developing typhoons in 2019.
- **Libraries**: MapLibre GL JS, deck.gl, CesiumJS; in Python: xarray, pydap, netCDF4, earthaccess, cdsapi, pandas, NumPy, Matplotlib, rasterio.

## Licence

- **Code** (the notebooks and the web pages): MIT licence, see `LICENSE`.
- **Data made in this project** (`docs/data`: smoke pictures, wind trails, fire counts, storm tracks and numbers; the case study and its pictures): Creative Commons Attribution 4.0 (CC BY 4.0). They are derived from the sources above, so please credit both this project and the original data providers. The wind trails contain modified Copernicus Climate Change Service information 2026.
- **Not covered**: the imagery shown on the pages (NASA GIBS, Bing Maps via Cesium ion) is streamed from its providers and stays under their own terms. The fonts in `docs/fonts` (Archivo and Source Serif 4) are under the SIL Open Font License.

## Author

Lik Ren Tai
