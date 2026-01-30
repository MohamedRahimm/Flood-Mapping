## Overview

This project demonstrates a complete geospatial workflow for generating terrain and building models from LiDAR data and visualizing a **simple flash flood scenario** in 3D using QGIS. The study area is **Apopka, Florida**, and the focus is on deriving terrain, building heights, and flood extents from publicly available data.

## Data Sources

### LiDAR Data

* Source: **USGS LiDAR Data (3DEP)**
* Accessed via: **[USGS Website](https://apps.nationalmap.gov/downloader/)**
### Building Footprints

* Source: **OpenStreetMap**
* Accessed via: **QuickOSM plugin in QGIS**


## Methodology

### 1. LiDAR Preprocessing (CloudCompare)

LiDAR point clouds were processed in **CloudCompare** to generate elevation surfaces:

* Ground points were classified and used to generate a **Digital Terrain Model (DTM)** and **Kriging interpolation** was applied to fill empty cells:
  ![Picture of DTM](https://github.com/MohamedRahimm/Flood-Mapping/blob/main/screenshots/Screenshot%202026-01-30%20015628.jpeg)
* Non-ground returns were used to generate a **Digital Surface Model (DSM)**:
![Picture of DSM](https://github.com/MohamedRahimm/Flood-Mapping/blob/main/screenshots/Screenshot%202026-01-30%20015737.jpeg)


### 3. Building Footprint Extraction (QuickOSM)

Building polygons were extracted using **QuickOSM** This produced a polygon layer representing all mapped buildings in the study area.

### 4. Building Height Calculation

Building heights were derived using zonal statistics applied to the building footprint polygons. The building polygons were used as the zone layer, with the DSM as the input raster. This process computed the mean elevation for each building, resulting in a building layer with associated height values suitable for 3D visualization.

### 5. Flash Flood Simulation

A **simple flash flood scenario** was simulated using the DTM:

* A high water level was applied to **low-lying terrain**
* Flooded areas were identified by thresholding elevation values
* Flood extents were visualized as a raster layer

### 6. 3D Visualization
The flood polygon was overlaid on a Google Satellite basemap to provide spatial context and improve visual interpretation of inundated areas.
![Picture of 3D Map](https://github.com/MohamedRahimm/Flood-Mapping/blob/main/screenshots/Screenshot%202026-01-30%20021822.jpeg)
![Picture of 3D Map](https://github.com/MohamedRahimm/Flood-Mapping/blob/main/screenshots/Screenshot%202026-01-30%20021849.jpeg) 

## Limitations

* Flood simulation is elevation-based only
* No hydraulic connectivity or flow modeling
* Accuracy depends on LiDAR resolution and OSM building completeness

Project created as a geospatial analysis and visualization exercise using open-source GIS tools.
