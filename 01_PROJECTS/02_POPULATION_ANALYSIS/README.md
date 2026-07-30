# Syria Population Analysis Collection

## Overview

This folder contains four population analyses of Syria created using the WorldPop 2026 population raster. Each Jupyter Notebook applies a different method: national population-distribution visualisation, windowed reading of a selected area, zonal statistics by governorate, or polygon-based raster masking.

This collection implements a sequence of spatial analysis methods for reading, processing, aggregating, extracting and visualising population raster data according to different analytical objectives.

## Analysis Collection

- Four population analyses included
- WorldPop 2026 estimated population raster used
- Each analysis exported as an interactive HTML file
- A derived GeoTIFF also exported for the Idleb analysis

| No. | Interactive map | Jupyter Notebook | Analysis method | Analysis area |
|---:|---|---|---|---|
| 01 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/01_syria_population_distribution_map.html) | [Notebook](01_Syria_Population_Distribution_Map.ipynb) | Downsampling and raster visualisation | All of Syria |
| 02 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/02_syria_windowed_reading.html) | [Notebook](02_Syria_WindowedReading.ipynb) | Windowed reading | Mainly northwestern Syria |
| 03 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/03_syria_zonal_statistics.html) | [Notebook](03_Syria_NW3_ZonalStatistics.ipynb) | Zonal statistics and proportional circles | Aleppo, Idleb and Lattakia governorates |
| 04 | [View map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/04_syria_idleb_mask.html) | [Notebook](04_Syria_Idleb_Mask.ipynb) | Raster masking | Idleb Governorate |

## 01 — Syria Population Distribution Map

This analysis uses the WorldPop 2026 population raster to visualise estimated population distribution across Syria. The raster is downsampled using average resampling for web-map display, styled with a custom colour map, and displayed on a dark basemap with administrative boundaries and governorate labels.

Main processes:

- Read and downsample the population raster
- Preserve NoData areas as transparent pixels
- Apply a custom colour map
- Add administrative boundaries, governorate labels, a colour legend and an information panel
- Export the interactive HTML file

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/01_syria_population_distribution_map.html)

## 02 — Syria Population Windowed Reading Map

This analysis uses the WorldPop 2026 population raster to read a 3,000 × 3,000 pixel window from the upper-left section without loading the complete raster. The selected window mainly covers northwestern Syria and displays estimated population per source grid cell on a white basemap with administrative boundaries and labels.

Main processes:

- Define a 3,000 × 3,000 pixel reading window
- Read a selected area without loading the complete raster
- Preserve NoData areas as transparent pixels
- Display the population raster without aggregation or resampling
- Add administrative boundaries, labels, a colour legend and an information panel
- Export the interactive HTML file

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/02_syria_windowed_reading.html)

## 03 — Northwestern Syria Three-Governorate Population Zonal Statistics Map

This analysis uses the WorldPop 2026 population raster to calculate the estimated population of Aleppo, Idleb and Lattakia governorates using zonal statistics. Population values are calculated by summing source raster cells whose centres fall within each governorate boundary, and the results are displayed on a dark basemap using circles whose areas are proportional to population.

Main processes:

- Validate the administrative boundaries, population raster, coordinate reference systems and NoData value
- Select Aleppo, Idleb and Lattakia governorates
- Apply the cell-centre rule using `all_touched=False`
- Calculate estimated population by governorate using zonal statistics
- Create representative points within the governorate polygons
- Add area-proportional circles, a numeric legend and an information panel
- Export the interactive HTML file

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/03_syria_zonal_statistics.html)

## 04 — Idleb Governorate Population Raster Masking Map

This analysis uses the WorldPop 2026 population raster to mask the national population raster with the Idleb Governorate administrative boundary. The extracted population raster is saved as a derived GeoTIFF that retains the source resolution, coordinate reference system and NoData definition, and is displayed on an interactive map using logarithmic colour scaling.

Main processes:

- Validate the administrative boundary, population raster, coordinate reference systems and NoData value
- Select Idleb Governorate and validate its geometry
- Mask the population raster using the cell-centre rule
- Save a derived GeoTIFF while preserving spatial metadata
- Validate the derived GeoTIFF
- Apply logarithmic colour scaling
- Add the Idleb boundary, label, legend and source information
- Export the interactive HTML file

Derived raster:

- `outputs/worldpop_idleb_2026.tif`

[View interactive map](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/02_POPULATION_ANALYSIS/04_syria_idleb_mask.html)

## Shared Specifications

- WorldPop 2026 estimated population raster used
- Syrian administrative boundary data used
- NoData areas considered during analysis and display
- Interactive maps created with Folium
- Legends and analysis information displayed
- Saved in HTML format and displayed in Jupyter Notebook

## Data

Population raster data:

- `worldpop_syria_2026.tif`

Source: WorldPop, 2026 estimated population dataset

Administrative boundary data:

- `syr_admin0.geojson`
- `syr_admin1.geojson`

Source: HDX OCHA, Syria subnational administrative boundaries

## Technologies

- Python
- Rasterio
- GeoPandas
- NumPy
- rasterstats
- Folium
- Matplotlib
- Branca
- pathlib

## How to Run

Run each Jupyter Notebook from top to bottom. The corresponding analysis and visualisation will be completed, and the interactive map will be saved as an HTML file and displayed in Jupyter Notebook.

In addition to the interactive HTML file, `04_Syria_Idleb_Mask.ipynb` saves the masked population raster as `outputs/worldpop_idleb_2026.tif`.

## Notes

- Population values are estimates rather than census counts.
- The source raster resolution is 3 arc seconds, approximately 100 metres.
- The downsampled display layer in 01 should not be used to calculate population totals.
- Analysis 02 displays only a 3,000 × 3,000 pixel window from the upper-left section of the source raster and does not represent all of Syria.
- Analysis 03 is limited to Aleppo, Idleb and Lattakia governorates.
- Analysis 03 includes cells whose centres fall within each governorate boundary and excludes boundary cells whose centres fall outside it.
- The circles in 03 are placed at representative points within the governorate polygons and do not indicate governorate capitals.
- In 03, circle areas, rather than circle radii, are proportional to estimated population.
- The derived GeoTIFF in 04 retains the source raster resolution, coordinate reference system and NoData definition.
- Results depend on the source raster, administrative boundaries, processing extent, resampling method and boundary-cell rule.
- An internet connection is required to load the background tiles.
- The terms of use and attribution requirements of the respective providers apply to the background maps, population raster and administrative boundary data.
- This collection presents maps and estimates for analysis and does not represent the legal status of administrative boundaries.
