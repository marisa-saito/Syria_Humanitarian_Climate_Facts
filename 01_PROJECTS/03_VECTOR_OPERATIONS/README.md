# Syria Vector Analysis Collection

## Overview

This folder contains four spatial analyses created using vector data for Syria. Each Jupyter Notebook applies a different method: river buffering, administrative-boundary dissolve, spatial join between administrative points and governorate boundaries, or coordinate reference system alignment for river and water-body data.

This collection implements a sequence of vector analysis methods for distance analysis, boundary aggregation, point-in-polygon operations, attribute validation, reprojection and data simplification according to different analytical objectives.

## Analysis Collection

- Four vector analyses included
- Attributes, geometries and coordinate reference systems validated in each analysis
- Analysis results saved as derived GeoPackages
- Each analysis exported as an interactive HTML file

| No. | Interactive map | Jupyter Notebook | Analysis method | Analysis area |
|---:|---|---|---|---|
| 01 | [View map](PUBLIC_URL) | [Notebook](01_Syria_Vector_Buffer.ipynb) | Reprojection and 10 km buffering | Rivers in Syria |
| 02 | [View map](PUBLIC_URL) | [Notebook](02_Syria_Vector_Dissolve.ipynb) | Attribute aggregation and dissolve | Four custom regions created from 14 governorates |
| 03 | [View map](PUBLIC_URL) | [Notebook](03_Syria_Vector_SpatialJoin.ipynb) | Point-in-polygon spatial join | 348 administrative points |
| 04 | [View map](PUBLIC_URL) | [Notebook](04_Syria_Vector_CRS_Alignment.ipynb) | Reprojection and CRS alignment | Rivers and water bodies |

## 01 — Syria 10 km River Buffer Map

This analysis uses vector data for Syria to create 10 km buffers around mapped river features. The river data is reprojected from Web Mercator to WGS 84 / UTM zone 37N so that distances can be calculated in metres, and the resulting buffers are displayed on an interactive map with the source rivers and administrative boundaries.

Main processes:

- Validate the river and administrative boundary data
- Reproject the river data to WGS 84 / UTM zone 37N
- Create 10 km buffers around the river features
- Save a derived GeoPackage while preserving the source river attributes
- Create simplified copies for web-map display
- Display the rivers, buffers and administrative boundaries
- Export the interactive HTML file

Derived data:

- `outputs/syr_river_buffer_10km.gpkg`

[View interactive map](PUBLIC_URL)

## 02 — Syria Governorate Dissolve Map by Custom Analytical Region

This analysis uses vector data for Syria to classify the 14 governorates into four custom analytical regions and dissolve the internal governorate boundaries within each region. The dissolved regions retain the names, Pcodes and number of their constituent governorates, and their areas are calculated in a projected coordinate system.

Main processes:

- Validate the national and governorate boundary data
- Classify the 14 governorates into four custom regions
- Validate the classification and regional membership of every governorate
- Aggregate governorate names, Pcodes and feature counts
- Dissolve the governorate boundaries by analytical region
- Calculate regional areas using WGS 84 / UTM zone 37N
- Save and validate the derived GeoPackage
- Export the interactive HTML file

Derived data:

- `syr_custom_analytical_regions.gpkg`

[View interactive map](PUBLIC_URL)

## 03 — Syria Administrative Point Spatial Join Map

This analysis uses vector data for Syria to assign governorate attributes to administrative points through a point-in-polygon spatial join. A left join using the `within` predicate is applied to 348 points after excluding the national-level reference point, and the results are checked for unmatched points, points assigned to multiple governorates and consistency with the source governorate attributes.

Main processes:

- Validate the administrative point and boundary data
- Exclude the national-level reference point
- Perform a left spatial join using the `within` predicate
- Detect unmatched points and points assigned to multiple governorates
- Compare the spatially assigned governorate attributes with the source attributes
- Save the verified results as a derived GeoPackage
- Create point layers by administrative level
- Add administrative boundaries, labels, a legend, information panels and layer controls
- Export the interactive HTML file

[View interactive map](PUBLIC_URL)

## 04 — Syria River and Water-Body CRS Alignment Map

This analysis uses vector data for Syria to align river and water-body datasets that originally use different coordinate reference systems. The river data is reprojected from Web Mercator (EPSG:3857) to WGS 84 (EPSG:4326), the full-resolution datasets are saved in a GeoPackage, and simplified copies are displayed on an interactive map.

Main processes:

- Validate the river, water-body and administrative boundary data
- Confirm the coordinate reference system of each input dataset
- Reproject the river data from EPSG:3857 to EPSG:4326
- Validate the feature count and geometry types after reprojection
- Save the full-resolution CRS-aligned data in a GeoPackage
- Read back and validate the saved GeoPackage layers
- Create simplified copies for web-map display
- Add the river, water-body, administrative boundary, label, legend, information panel and layer-control elements
- Export the interactive HTML file

[View interactive map](PUBLIC_URL)

## Shared Specifications

- Vector data attributes, geometries and coordinate reference systems validated
- Vector analysis performed with GeoPandas
- Analysis results saved as derived GeoPackages
- Interactive maps created with Folium
- Administrative boundaries, labels, legends and analysis information displayed
- Saved in HTML format and displayed in Jupyter Notebook

## Data

River and water-body data:

- `syr_rivers_3857.geojson`
- `syr_lakes_4326.geojson`

Source: OpenStreetMap contributors

Administrative point data:

- `syr_adminpoints.geojson`

Administrative boundary data:

- `syr_admin0.geojson`
- `syr_admin1.geojson`

Source: HDX OCHA, Syria subnational administrative boundaries

## Technologies

- Python
- GeoPandas
- Folium
- Shapely
- PyProj
- GeoPackage

## How to Run

Run each Jupyter Notebook from top to bottom. The corresponding vector analysis and visualisation will be completed, the derived data and interactive HTML file will be saved, and the map will be displayed in Jupyter Notebook.

`01_Syria_Vector_Buffer.ipynb` saves the 10 km river buffers as `outputs/syr_river_buffer_10km.gpkg`.

`02_Syria_Vector_Dissolve.ipynb` saves the dissolved custom analytical regions as `syr_custom_analytical_regions.gpkg`.

## Notes

- Analysis 01 reprojects the river data to WGS 84 / UTM zone 37N so that distances can be calculated in metres.
- The buffers in 01 are not clipped to the Syrian national boundary and may extend into neighbouring countries.
- The four regions in 02 were defined for this analysis and do not represent an official humanitarian, administrative or operational regional framework.
- The dissolved regions in 02 retain the names, Pcodes and number of their constituent governorates.
- Analysis 03 excludes the national-level reference point because it does not belong to a single governorate.
- Analysis 03 uses a left join with the `within` predicate to preserve every analytical point.
- Analysis 04 saves the full-resolution data in a GeoPackage and uses simplified copies for the interactive map.
- Simplified copies are used for web-map visualisation and should be distinguished from the full-resolution derived data.
- An internet connection is required to load the background tiles.
- The terms of use and attribution requirements of the respective providers apply to the background maps, administrative boundaries, river data and water-body data.
- This collection includes analytical maps and custom classifications and does not represent the legal or official status of administrative boundaries or regional groupings.
