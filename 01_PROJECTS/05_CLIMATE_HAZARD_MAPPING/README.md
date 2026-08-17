# Syria Climate Hazard Mapping

## Overview

This folder contains an interactive map of reported flood-affected locations along the Euphrates corridor in Syria. The workflow reads an updatable project CSV, validates each record, converts the reported coordinates into spatial point data, and verifies the reported governorates through a spatial join with administrative boundaries.

The current dataset contains six reported locations associated with one flood event dated 25 May 2026. The reported locations are in Aleppo and Deir-ez-Zor Governorates, while Ar-Raqqa Governorate is displayed as geographical context for the Euphrates corridor.

## Project Overview

- Flood-affected location map created from an updatable CSV
- CSV schema, identifiers, dates, coordinates and duplicate records validated
- Reported and spatially assigned governorates compared through a spatial join
- Validated locations saved as a derived GeoPackage
- Analysis result exported as an interactive HTML file

| No. | Interactive map | Jupyter Notebook | Analysis method | Analysis area |
|---:|---|---|---|---|
| 01 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/05_CLIMATE_HAZARD_MAPPING/01_syria_euphrates_flood_affected_locations.html) | [Notebook](01_Syria_EuphratesFloodEvents_Map.ipynb) | CSV validation and point-in-polygon spatial join | Reported locations along the Euphrates corridor (currently six) |

## 01 — Reported Flood-Affected Locations Along the Euphrates

This analysis uses an updatable project CSV to visualise reported flood-affected locations along the Euphrates corridor. It creates spatial point data from latitude and longitude coordinates, assigns each location to a governorate through a spatial join using the `within` predicate, and verifies the result against the governorate recorded in the CSV.

Main processes:

- Validate the CSV schema and required values
- Validate the format and uniqueness of site IDs and event IDs
- Validate dates, latitude, longitude and duplicate locations
- Create EPSG:4326 point data from latitude and longitude
- Validate the attributes, CRS and geometries of the administrative boundary, river and water-body data
- Extract the Euphrates River from the river dataset
- Select Aleppo, Ar-Raqqa and Deir-ez-Zor Governorates as corridor context
- Perform a left spatial join using the `within` predicate
- Detect unmatched locations, locations assigned to multiple governorates and governorate mismatches
- Save and revalidate the verified locations as a derived GeoPackage
- Display the Euphrates River, water bodies, administrative boundaries and reported locations
- Add a legend, information panel, popups and layer controls
- Export the interactive HTML file

Derived data:

- `outputs/euphrates_flood_affected_locations_validated.gpkg`

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/05_CLIMATE_HAZARD_MAPPING/01_syria_euphrates_flood_affected_locations.html)

![Reported Flood-Affected Locations Along the Euphrates](images/01_syria_euphrates_flood_events_map.png)

## Implementation Specifications

- Updatable CSV used as the input dataset
- Required and unexpected columns validated
- Site ID and event ID formats validated with regular expressions
- Duplicate site IDs and event-location records validated
- Reported coordinates converted into a GeoDataFrame
- Spatial datasets aligned to WGS 84 (EPSG:4326)
- Spatial join results compared with governorates recorded in the CSV
- Validated attributes and geometries saved in a GeoPackage
- Feature count, CRS and site ID uniqueness revalidated after reading back the saved GeoPackage
- Interactive map created with Folium

## Data

Flood-affected location data:

- `climap_euphrates_flood_affected_locations.csv`

Source: User-maintained project dataset

Administrative boundary data:

- `syr_admin1.geojson`

Source: HDX OCHA, Syria subnational administrative boundaries

River and water-body data:

- `syr_rivers_3857.geojson`
- `syr_lakes_4326.geojson`

Source: OpenStreetMap contributors

## Technologies

- Python
- Pandas
- GeoPandas
- Folium
- Shapely
- Branca
- GeoPackage

## How to Run

Run `01_Syria_EuphratesFloodEvents_Map.ipynb` from top to bottom. The workflow validates the CSV and spatial data, creates the point dataset, performs the spatial join, verifies the governorate assignments and creates the visualisation.

The validated locations are saved as `outputs/euphrates_flood_affected_locations_validated.gpkg`. The interactive map is saved as `01_syria_euphrates_flood_affected_locations.html` and displayed in Jupyter Notebook.

## Notes

- The current CSV contains six reported locations associated with one flood event dated 25 May 2026.
- The reported locations currently occur in Aleppo and Deir-ez-Zor Governorates.
- Ar-Raqqa Governorate is displayed as geographical context, but the current CSV contains no reported location in that governorate.
- The data represents reported point locations and does not describe the complete spatial extent of flooding.
- Source organisations are recorded, but detailed source titles, URLs and access dates remain to be added.
- The map reflects the CSV at the time the Notebook is executed and will change when new locations or source information are added.
- The map should not be interpreted as a comprehensive inventory of all flood-affected locations in Syria.
- An internet connection is required to load the background tiles.
- The terms of use and attribution requirements of the respective providers apply to the background map, administrative boundaries, river data and water-body data.
- This project presents an analytical map of reported locations and does not represent the legal status of administrative boundaries.
