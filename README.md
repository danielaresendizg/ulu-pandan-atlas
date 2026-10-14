# Ulu Pandan Atlas

An interactive map atlas of the twelve URA subzones along Ulu Pandan Canal, Singapore. It was built for the LA5222 Urban Ecology team project at the National University of Singapore (2026).

**Live site:** https://danielaresendizg.github.io/ulu-pandan-atlas/

The atlas opens with the study area only. Layers are switched on from the left rail, grouped as: study area, land use and form, water, catchment (modelled), mobility, public space, planned investment and nature. Clicking a subzone shows its raw Census 2020 values; nothing is recalculated to buffers or walking catchments.

## What is in the repo

- `index.html` is the whole app: Leaflet 1.9.4 from cdnjs, with the CSS inlined.
- `data/` holds the GeoJSON layers, already clipped to the study area. Forests and catchment layers extend past the subzones on purpose. `meta.json` holds the bounds and extent.

To run it locally, serve the folder rather than opening the file directly, because the browser blocks `fetch` from `file://`:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Methods and caveats

- **Units:** URA Master Plan 2019 subzones. Census 2020 publishes age, sex, dwelling type and floor area by subzone. Income and transport mode are published by planning area only, so they are not shown per subzone. SingStat rounds counts to the nearest 10.
- **Catchment (modelled):** PUB does not publish catchment boundaries. These layers are derived from the Copernicus GLO-30 DSM:
  - grey opening to approximate the ground surface;
  - stream burning with OSM waterways and URA waterbodies;
  - priority-flood fill, D8 flow directions and flow accumulation.

  The modelled catchment is 16.7 km², below the >25 km² reported by Saxena et al. (2015), partly because the Bukit Timah diversion is engineered. Read it as indicative only.
- **Planned investment:**
  - The PUB canal improvement reach (Commonwealth Ave West to Clementi Rd) is drawn by hand from the project description.
  - HDB contract areas are approximate hulls of the new blocks.
  - Contract values come from GeBIZ awards, Apr 2021 to Mar 2026.
- **Gaps:** layers with no features inside the study area are left out, not shown empty.

## Sources and licences

- **data.gov.sg**, under the [Singapore Open Data Licence](https://data.gov.sg/open-data-licence). Contributing agencies: URA, SingStat, PUB, NParks, LTA, HDB, NEA, SLA, People's Association, SportSG and ECDA.
- **GeBIZ** government procurement awards, via data.gov.sg.
- **OpenStreetMap contributors**, under [ODbL](https://opendatacommons.org/licenses/odbl/): forests, waterways and drainage lines.
- **Copernicus DEM GLO-30**: © DLR e.V. 2010–2014 and © Airbus Defence and Space GmbH 2014–2018, provided under COPERNICUS by the European Union and ESA; all rights reserved.
- **Basemap:** [OneMap](https://www.onemap.gov.sg/), Singapore Land Authority. Tiles load live and are shown in greyscale.

This is a student project and is not an official product of any Singapore agency.
