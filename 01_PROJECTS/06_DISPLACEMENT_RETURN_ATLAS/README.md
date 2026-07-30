# Syria Displacement and Return Atlas

## Overview

This folder contains English and Japanese versions of the Syria Displacement and Return Atlas, which integrates the 2026 displacement and return baseline data from the International Organization for Migration (IOM) with populated-place points from the Humanitarian OpenStreetMap Team (HOTOSM).

The IOM data contains population indicators by reported location but does not include point geometries. HOTOSM populated-place points within the same ADM3 Pcode are therefore treated as candidates and matched one-to-one using normalised settlement names and text-similarity scores. Only locations that satisfy the defined acceptance criteria are displayed on the map, while candidates, similarity scores, acceptance decisions and exclusion reasons are retained as audit data.

## Atlas Collection

- IOM population indicators integrated with HOTOSM point geometries
- Locations matched using ADM3 Pcodes and settlement-name similarity
- Only exact matches or similarity scores of 85% and above accepted automatically
- One-to-one matching prevents a HOTOSM point from being assigned to multiple IOM locations
- Five population indicators displayed using a shared proportional-circle scale
- English and Japanese interactive HTML files exported

| No. | Interactive map | Jupyter Notebook | Display language | Analysis |
|---:|---|---|---|---|
| 01 | [View map](PUBLIC_URL) | [Notebook](01_Syria_Displacement_and_Return_Atlas.ipynb) | English | IOM–HOTOSM location matching with displacement and return indicators |
| 02 | [View map](PUBLIC_URL) | [Notebook](02_Syria_Displacement_and_Return_Atlas_JP.ipynb) | Japanese | IOM–HOTOSM location matching with displacement and return indicators |

## Data Integration and Location Matching

This analysis uses IOM displacement and return data and integrates it with HOTOSM populated-place data that provides point geometries. The three highest-scoring candidates are generated within the same ADM3 Pcode, and spelling variations—including variations in English transliterations of Arabic place names—are evaluated using normalised names and text-similarity scores.

Main processes:

- Validate the columns, CRS and geometries of the IOM and HOTOSM data
- Standardise the IOM administrative and population-indicator columns
- Validate missing, non-numeric, non-finite and negative population values
- Confirm that 2026 values do not exceed the corresponding totals since December 2024
- Recalculate total population from its components and compare it with the reported value
- Retain only Point features from the HOTOSM dataset
- Normalise IOM and HOTOSM settlement names
- Generate the three highest-scoring candidates within the same ADM3 Pcode
- Calculate text similarity using direct comparison and token-order comparison
- Accept exact matches or candidates with similarity scores of 85% and above
- Apply deterministic one-to-one assignment without reusing HOTOSM points
- Classify records as accepted, review required, unresolved duplicate conflict or no candidate
- Save the audit CSV and validated GeoPackage
- Display five population indicators using a shared proportional-circle scale

[View English interactive map](PUBLIC_URL)

[View Japanese interactive map](PUBLIC_URL)

## Matching Results

| Item | Records | Percentage or composition |
|---|---:|---|
| IOM source data | 8,394 | 100% |
| HOTOSM candidate available | 8,391 | 99.96% |
| Automatically accepted | 2,455 | 29.25% |
| Exact matches | 1,260 | Included in accepted records |
| High-confidence matches | 1,195 | Similarity score of 85% and above |
| Review required | 5,922 | Retained in audit data |
| Unresolved duplicate conflicts | 14 | Retained in audit data |
| No candidate | 3 | Retained in audit data |

The 2,455 automatically accepted locations were validated to ensure that there were no duplicate IOM Location Pcodes, duplicate HOTOSM IDs, below-threshold matches or ADM3 Pcode mismatches.

## Displayed Indicators

| Population indicator | Displayed locations | Displayed population | Percentage of IOM source total |
|---|---:|---:|---:|
| Residents | 2,180 | 6,094,064 | 32.73% |
| Internally displaced persons (IDPs) | 809 | 2,568,776 | 43.76% |
| IDP returnees since December 2024 | 959 | 808,746 | 38.90% |
| IDP returnees in 2026 | 415 | 67,992 | 42.37% |
| Total population | 2,353 | 9,921,264 | 35.55% |

A shared proportional-circle scale is used for all five population indicators. Circle areas are proportional to population, while extremely large values are capped at a maximum symbol size based on the 99th percentile across all indicators to preserve cross-layer comparability and map readability.

## Derived Data

- `outputs/iom_hotosm_location_matching_audit.csv`
  - Stores the best candidate, similarity score, acceptance decision and exclusion reason for all 8,394 IOM records
- `outputs/iom_displacement_return_locations_validated.gpkg`
  - Stores IOM population indicators and HOTOSM geometries for the 2,455 automatically accepted locations

## Data

Displacement and return data:

- `iom_displacement_return_2026.xlsx`

Source: International Organization for Migration (IOM)

Populated-place data:

- `hotosm_populated_places.gpkg`

Source: Humanitarian OpenStreetMap Team (HOTOSM) / OpenStreetMap contributors

Administrative boundary data:

- `syr_admin0.geojson`
- `syr_admin1.geojson`

Source: HDX OCHA, Syria administrative boundaries

River and water-body data:

- `syr_rivers_3857.geojson`
- `syr_lakes_4326.geojson`

Source: OpenStreetMap contributors

## Technologies

- Python
- Pandas
- GeoPandas
- Folium
- difflib
- Branca
- GeoPackage

## How to Run

Run `01_Syria_Displacement_and_Return_Atlas.ipynb` from top to bottom. The workflow validates the data, matches locations, applies the acceptance criteria, saves the audit data and creates the population-indicator layers. The English atlas is saved as `01_syria_displacement_and_return_atlas.html` and displayed in Jupyter Notebook.

Run `02_Syria_Displacement_and_Return_Atlas_JP.ipynb` from top to bottom to create the Japanese atlas from the same analysis results. The Japanese atlas is saved as `02_syria_displacement_and_return_atlas_jp.html` and displayed in Jupyter Notebook.

## Notes

- IOM locations are displayed using the coordinates of their matched HOTOSM populated-place points.
- The mapped coordinates are reference locations derived from the matching process and are not original IOM coordinates.
- Name similarity alone does not prove that two records describe the same settlement.
- Matching candidates are restricted to locations sharing the same ADM3 Pcode.
- Only exact matches or similarity scores of 85% and above that also satisfy the uniqueness criteria are used in the primary population layers.
- Similarity scores from 70% to below 85% require review; scores below 70%, records with no candidate and unresolved duplicate conflicts remain in the audit output.
- Displayed population values and percentages cover only the 2,455 automatically accepted locations and do not represent the complete IOM source dataset.
- Population indicators follow the definitions and reporting period of the IOM source data.
- The atlas does not represent real-time displacement or return conditions.
- An internet connection is required to load the background tiles.
- The terms of use and attribution requirements of the respective providers apply to the background map, administrative boundaries, river data and water-body data.
- This atlas is intended for analysis and does not represent the legal status of administrative boundaries.
