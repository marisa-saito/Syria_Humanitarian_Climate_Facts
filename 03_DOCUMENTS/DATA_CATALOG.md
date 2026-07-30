# Humanitarian GIS Data Catalogue

[日本語](DATA_CATALOG_JP.md)

## Overview

This catalogue documents the source datasets used across the six collections in the `Syria_Humanitarian_Climate_Facts` portfolio and distinguishes them from project-derived outputs.

Source datasets under `02_DATA/` are maintained locally and excluded from the public GitHub repository because of file size and source-provider terms. They must be obtained from their respective providers before the Jupyter Notebooks are executed. Small selected derived outputs are included with the project folders, while larger reproducible outputs are excluded from Git.

The catalogue describes the current local files inspected for this portfolio. A source URL, access date or document title is marked as not recorded when it cannot be verified from the local data or project documentation.

## Source Dataset Summary

| Category | Local file | Provider | Format | Used in | Public repository |
|---|---|---|---|---|---|
| Raster | `worldpop_syria_2026.tif` | WorldPop | GeoTIFF | 02, 04 | Not included |
| Tabular | `climap_euphrates_flood_affected_locations.csv` | Project-maintained data | CSV | 05 | Not included |
| Tabular | `iom_displacement_return_2026.xlsx` | International Organization for Migration (IOM) | XLSX | 06 | Not included |
| Vector | `hotosm_populated_places.gpkg` | Humanitarian OpenStreetMap Team (HOTOSM) / OpenStreetMap contributors | GeoPackage | 06 | Not included |
| Vector | `syr_admin0.geojson`–`syr_admin3.geojson` | HDX OCHA | GeoJSON | 01–06 | Not included |
| Vector | `syr_admincapitals.geojson` | HDX OCHA | GeoJSON | Reference data | Not included |
| Vector | `syr_adminlines.geojson` | HDX OCHA | GeoJSON | Reference data | Not included |
| Vector | `syr_adminpoints.geojson` | HDX OCHA | GeoJSON | 03 | Not included |
| Vector | `syr_rivers_3857.geojson` | OpenStreetMap contributors | GeoJSON | 03, 05, 06 | Not included |
| Vector | `syr_lakes_4326.geojson` | OpenStreetMap contributors | GeoJSON | 03, 05, 06 | Not included |

## Raster Source Data

### `worldpop_syria_2026.tif`

- Local path: `02_DATA/RASTER/worldpop_syria_2026.tif`
- Provider: WorldPop
- Dataset: Syrian Arab Republic — Spatial Distribution of Population, 2026 estimate
- Original document name: `syr_pop_2026_CN_100m_R2025A_v1`
- Version: R2025A v1
- Format: single-band GeoTIFF, `float32`
- CRS: EPSG:4326
- Grid: 7,992 × 6,011 cells
- Resolution: 3 arc-seconds, approximately 100 m at the equator
- Unit: estimated number of people per grid cell
- NoData: `-99999`
- Production date listed on the WorldPop source page: 1 September 2025
- Licence recorded in the file metadata: CC BY 4.0
- Used in: 02 Population Analysis; 04 Raster Operations
- Source page: [WorldPop dataset summary](https://hub.worldpop.org/geodata/summary?id=75632)
- DOI: [10.5258/SOTON/WP00839](https://doi.org/10.5258/SOTON/WP00839)

This is an estimated population surface rather than an observed census count. The WorldPop source page identifies the dataset as an alpha R2025A product that may be revised.

## Tabular Source Data

### `climap_euphrates_flood_affected_locations.csv`

- Local path: `02_DATA/TABULAR/climap_euphrates_flood_affected_locations.csv`
- Provider: project-maintained data compiled from humanitarian reporting
- Format: CSV
- Records: 6 reported locations
- Fields: 12
- Event date currently recorded: 25 May 2026
- Spatial fields: latitude and longitude in WGS 84
- Used in: 05 Climate Hazard Mapping
- Source documents:
  - [UNFPA — Euphrates Floods Flash Update (25 May–6 June 2026)](https://reliefweb.int/report/syrian-arab-republic/unfpa-syria-flash-update-euphrates-floods-raqqa-and-deir-ez-zor-25-may-6-june-2026)
  - [WFP — Euphrates River Flood Assessment (June 2026)](https://reliefweb.int/report/syrian-arab-republic/wfp-satellite-based-flood-extent-agricultural-impact-assessment-euphrates-river-flood-deir-ez-zor-governorate-june-2026)
  - [Oxfam — Euphrates River Flood Rapid Needs Assessment: Deir ez-Zor Irrigation Sites (May 2026)](https://reliefweb.int/report/syrian-arab-republic/rapid-needs-assessment-euphrates-river-flood-deir-ez-zor-rrigations-sites-may-2026)
  - [IFRC — Euphrates River Floods DREF Operation (MDRSY019)](https://reliefweb.int/report/syrian-arab-republic/syrian-arab-republic-euphrates-river-floods-2026-dref-operation-mdrsy019)
- Access date: 1 July 2026

### `iom_displacement_return_2026.xlsx`

- Local path: `02_DATA/TABULAR/iom_displacement_return_2026.xlsx`
- Provider: International Organization for Migration (IOM), Displacement Tracking Matrix (DTM)
- Original file name: `Baseline April 2026_public.xlsx`
- Format: XLSX
- Workbook sheets: `Short Baseline`; `Dataset`
- `Short Baseline`: 8,394 rows × 20 columns
- `Dataset`: 8,394 rows × 137 columns
- Analytical sheet used by the project: `Short Baseline`
- Coverage: settlement-level population, displacement and return indicators
- Used in: 06 Displacement and Return Atlas
- Official operation page: [IOM DTM — Syrian Arab Republic](https://dtm.iom.int/syrian-arab-republic)

The workbook contains population indicators but does not provide the point geometries used in the atlas. The project matches IOM locations to HOTOSM populated-place points under defined PCODE, name-similarity and one-to-one assignment criteria.

## Vector Source Data

### Syrian administrative datasets

- Local directory: `02_DATA/VECTOR/`
- Provider: HDX OCHA
- Dataset: Syria subnational administrative boundaries
- Format: GeoJSON
- CRS recorded in the files: OGC CRS84
- Boundary version recorded in the files: v02
- Boundary validity date recorded for ADM0–ADM3: 17 December 2020
- Source page: [HDX — Syrian Arab Republic administrative boundaries](https://data.humdata.org/dataset/cod-ab-syr)

| Local file | Geometry | Features | Primary use |
|---|---|---:|---|
| `syr_admin0.geojson` | MultiPolygon | 1 | National boundary |
| `syr_admin1.geojson` | Polygon / MultiPolygon | 14 | Governorate boundaries |
| `syr_admin2.geojson` | Polygon / MultiPolygon | 62 | District boundaries and PCODEs |
| `syr_admin3.geojson` | Polygon | 272 | Sub-district boundaries and PCODEs |
| `syr_admincapitals.geojson` | Point | 266 | Administrative-capital reference points |
| `syr_adminlines.geojson` | LineString | 811 | Administrative-line reference data |
| `syr_adminpoints.geojson` | Point | 349 | Administrative points used in Spatial Join |

The boundaries and names used in the portfolio do not imply legal status, official endorsement or acceptance.

### `hotosm_populated_places.gpkg`

- Local path: `02_DATA/VECTOR/hotosm_populated_places.gpkg`
- Provider: Humanitarian OpenStreetMap Team (HOTOSM) / OpenStreetMap contributors
- Local layer: `populated_places`
- Format: GeoPackage
- CRS: EPSG:4326
- Total source features: 29,863
- Geometry composition: 8,995 Point; 20,840 Polygon; 27 MultiPolygon; 1 LineString
- Point features used by Project 06: 8,995
- Key fields: OSM ID, multilingual names, place type, population and ADM0–ADM4 PCODEs
- Used in: 06 Displacement and Return Atlas
- Dataset page: [HDX — HOTOSM Syria populated places](https://data.humdata.org/dataset/hotosm_syr_populated_places)
- Licence and attribution: [OpenStreetMap copyright and licence](https://www.openstreetmap.org/copyright)

The project retains Point geometries only and excludes non-point features before matching them to IOM locations.

### `syr_rivers_3857.geojson`

- Local path: `02_DATA/VECTOR/syr_rivers_3857.geojson`
- Provider: OpenStreetMap contributors
- Format: GeoJSON
- CRS: EPSG:3857
- Features: 12,034
- Geometry: LineString / MultiLineString
- Used in: 03 Vector Operations; 05 Climate Hazard Mapping; 06 Displacement and Return Atlas
- Licence and attribution: [OpenStreetMap copyright and licence](https://www.openstreetmap.org/copyright)
- Original download URL and access date: not recorded

### `syr_lakes_4326.geojson`

- Local path: `02_DATA/VECTOR/syr_lakes_4326.geojson`
- Provider: OpenStreetMap contributors
- Format: GeoJSON
- CRS used by the project: EPSG:4326
- Features: 2,925
- Geometry: Polygon / MultiPolygon
- Used in: 03 Vector Operations; 05 Climate Hazard Mapping; 06 Displacement and Return Atlas
- Licence and attribution: [OpenStreetMap copyright and licence](https://www.openstreetmap.org/copyright)
- Original download URL and access date: not recorded

## Derived Project Data

The following files are generated by the Jupyter Notebooks and are not independent source datasets.

| Project | Derived output | Purpose | Public repository |
|---:|---|---|---|
| 02 | `outputs/worldpop_idleb_2026.tif` | WorldPop raster masked to Idleb Governorate | Included |
| 03 | `outputs/syr_river_buffer_10km.gpkg` | Full-resolution 10 km river buffer | Excluded; reproducible |
| 03 | `outputs/syr_custom_analytical_regions.gpkg` | Four dissolved project-defined analytical regions | Excluded; reproducible |
| 03 | `outputs/syr_adminpoints_with_governorate.gpkg` | Administrative points with validated governorate attributes | Excluded; reproducible |
| 03 | `outputs/syr_hydrography_aligned_4326.gpkg` | Full-resolution river and water-body data aligned to EPSG:4326 | Excluded; reproducible |
| 04 | `outputs/worldpop_syria_2026_aggregated_approx_1km.tif` | Population raster aggregated to approximately 1 km | Excluded; reproducible |
| 04 | `outputs/worldpop_syria_2026_reprojected_3857.tif` | Population raster reprojected to EPSG:3857 | Excluded; reproducible |
| 05 | `outputs/euphrates_flood_affected_locations_validated.gpkg` | Validated flood-affected locations | Included |
| 06 | `outputs/iom_hotosm_location_matching_audit.csv` | Matching candidate, score, decision and reason for all 8,394 IOM records | Included |
| 06 | `outputs/iom_displacement_return_locations_validated.gpkg` | 2,455 accepted IOM records with HOTOSM geometries | Included |

## Repository and Reproduction Notes

- `02_DATA/` is excluded through `.gitignore` and is not published to GitHub.
- Source files must retain the local names and directory structure documented above unless the Notebook paths are updated.
- Selected small derived outputs are included to support review and auditing.
- Large derived outputs are excluded because they can be regenerated from the corresponding Notebook.
- Provider metadata, licences and download conditions should be checked again before redistributing any source dataset.
- Acquisition dates and original download URLs that are currently not recorded should be added when they can be verified.
