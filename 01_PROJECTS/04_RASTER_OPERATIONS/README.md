# Syria Raster Analysis Collection

## Overview

This folder contains two raster analyses created using the WorldPop 2026 population raster. Each Jupyter Notebook applies a different operation: population-raster aggregation from approximately 100 m to approximately 1 km, or population-raster reprojection from WGS 84 to Web Mercator.

This collection implements a sequence of raster analysis methods for sum resampling, destination-grid calculation, metadata updates and validation of population totals before and after processing according to different analytical objectives.

## Analysis Collection

- Two raster analyses included
- WorldPop 2026 estimated population raster used
- Sum resampling used to preserve estimated population totals
- Analysis results saved as derived GeoTIFFs
- Each analysis exported as an interactive HTML file

| No. | Interactive map | Jupyter Notebook | Analysis method | Processing change |
|---:|---|---|---|---|
| 01 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/04_RASTER_OPERATIONS/01_syria_raster_resample.html) | [Notebook](01_Syria_Raster_Resample.ipynb) | Aggregation with sum resampling | Approximately 100 m to approximately 1 km |
| 02 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/04_RASTER_OPERATIONS/02_syria_raster_reprojection.html) | [Notebook](02_Syria_Raster_Reprojection.ipynb) | Reprojection with sum resampling | EPSG:4326 to EPSG:3857 |

## 01 — Syria Population Raster Aggregation Map at Approximately 1 km

This analysis uses the WorldPop 2026 population raster to aggregate the source resolution of approximately 100 m to an output resolution of approximately 1 km. Sum resampling is used so that each output cell contains the estimated population from its contributing source cells, and the results are validated by comparing population totals before and after processing.

Main processes:

- Validate the source raster CRS, dimensions, transform, NoData value and data type
- Set the output dimensions to one tenth of the source width and height
- Calculate the destination grid and transform
- Aggregate the population raster using sum resampling
- Compare valid cell counts and population totals before and after aggregation
- Save the aggregated result as a derived GeoTIFF
- Read back and validate the saved GeoTIFF
- Add administrative boundaries, a legend and an information panel
- Export the interactive HTML file

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/04_RASTER_OPERATIONS/01_syria_raster_resample.html)

![Syria Population Raster Aggregation Map at Approximately 1 km](images/01_syria_raster_resample.png)

## 02 — Syria Population Raster Reprojection Map to Web Mercator

This analysis uses the WorldPop 2026 population raster to reproject the data from WGS 84 (EPSG:4326) to Web Mercator (EPSG:3857). Sum resampling is used to retain the estimated population represented by the contributing source cells, and the results are validated by comparing population totals before and after processing.

Main processes:

- Validate the source raster CRS, dimensions, transform, bounds and NoData value
- Calculate the EPSG:3857 destination grid
- Reproject the population raster using sum resampling
- Compare population totals before and after reprojection
- Save the reprojected result as a derived GeoTIFF
- Read back and validate the saved GeoTIFF
- Transform the output bounds for Folium display
- Add administrative boundaries, a legend and an information panel
- Export the interactive HTML file

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/04_RASTER_OPERATIONS/02_syria_raster_reprojection.html)

![Syria Population Raster Reprojection Map to Web Mercator](images/02_syria_raster_reprojection.png)

## Shared Specifications

- WorldPop 2026 estimated population raster used
- Source raster metadata and values validated
- NoData areas considered during analysis and display
- Sum resampling used to preserve estimated population totals
- Population totals compared before and after processing
- Analysis results saved as derived GeoTIFFs and validated after being read back
- Interactive maps created with Folium
- Saved in HTML format and displayed in Jupyter Notebook

## Data

Population raster data:

- `worldpop_syria_2026.tif`

Source: WorldPop, open population data

Administrative boundary data:

- `syr_admin0.geojson`
- `syr_admin1.geojson`

Source: HDX OCHA, Syria subnational administrative boundaries

## Technologies

- Python
- Rasterio
- NumPy
- GeoPandas
- Folium
- Matplotlib
- GeoTIFF

## How to Run

Run each Jupyter Notebook from top to bottom. The corresponding raster analysis and visualisation will be completed, the derived GeoTIFF and interactive HTML file will be saved, and the map will be displayed in Jupyter Notebook.

Analysis 01 saves the population raster aggregated to approximately 1 km, while 02 saves the population raster reprojected to Web Mercator. Each result is saved as a derived GeoTIFF.

## Notes

- Population values are estimates per source grid cell rather than census counts.
- Analysis 01 reduces the source width and height to one tenth, aggregating the raster from approximately 100 m to approximately 1 km.
- Analysis 01 sums the population values of the source cells contributing to each output cell.
- The output of 02 is intended for alignment with web-map tiles that use Web Mercator.
- Analysis 02 does not use EPSG:3857 for distance or area measurement.
- Both analyses use sum resampling and compare population totals before and after processing.
- Results depend on the source raster, destination grid, resampling method and handling of NoData areas.
- An internet connection is required to load the background tiles.
- The terms of use and attribution requirements of the respective providers apply to the background maps, population raster and administrative boundary data.
- This collection presents maps and estimates for analysis and does not represent the legal status of administrative boundaries.
