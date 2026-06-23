GFM Notebooks – Global Flood Monitoring (Copernicus CEMS)
==========================================================

This repository contains three Jupyter notebooks for analyzing and visualizing
flood data from the Copernicus Emergency Management Service (CEMS) Global Flood
Monitoring (GFM) system, which provides near-real-time flood information derived
from Sentinel-1 radar imagery.


Notebooks
---------

1. 3D_visualization_of_observed_floods_GFM/
   - Loads GFM ensemble flood extent rasters via STAC API (EODC)
   - Aggregates flood observations over time per pixel
   - Polygonizes flooded areas and exports GeoJSON
   - Visualizes flood frequency as interactive 3D extruded map (leafmap/maplibregl)

2. Flood_and_infrastructure_analyzer_GFM/
   - Loads GFM flood extent, exclusion mask, and likelihood layers
   - Computes maximum flood extent, exclusion, and likelihood rasters
   - Overlays flood data with OpenStreetMap infrastructure (hospitals, schools, etc.)
   - Exports impact analysis as CSV and interactive Folium maps

3. Global_flood_monitoring_time_series/
   - Loads GFM flood extent time series via STAC API
   - Exports per-day flood PNG overlays with cumulative fading effect
   - Renders animated GIF with OSM basemap and flooded-area bar chart
   - Embeds interactive HTML5 frame-by-frame player in the notebook


Data Source
-----------
- STAC API: https://stac.eodc.eu/api/v1
- Collection: GFM (Global Flood Monitoring)
- Band: ensemble_flood_extent (uint8, 0=no flood, 1-100=flood, 255=nodata)
- Resolution: 20m (Azimuthal Equidistant projection, reprojected to EPSG:4326)


Environment Setup
-----------------

Prerequisites: pixi (https://pixi.sh)

    # Install the environment
    pixi install

    # Launch JupyterLab (recommended for interactive widgets)
    pixi run lab

    # Or launch classic Notebook
    pixi run notebook

The environment is defined in pixi.toml and includes all dependencies
(geospatial, visualization, STAC access, Jupyter).


Binder
------
This repository is Binder-compatible. The binder/ directory contains:
- environment.yml  – conda environment for repo2docker
- postBuild       – post-install script

Launch on mybinder.org by pointing it at this repository.


Key Dependencies
----------------
- pystac-client, odc-stac  – STAC catalog search and lazy data loading
- xarray, rioxarray        – raster data handling and reprojection
- geopandas, shapely       – vector geometry operations
- rasterio                 – raster I/O and polygonization
- numpy, pandas            – numerical and tabular data
- matplotlib, folium       – static and interactive maps
- leafmap, ipyleaflet      – interactive map widgets (3D, drawing)
- ipywidgets               – notebook UI controls (date pickers, etc.)
- imageio, pillow          – image/video frame generation


Usage Notes
-----------
- All notebooks include interactive map widgets (ipyleaflet) for drawing an AOI.
  These require JupyterLab in a browser (pixi run lab).
- Default bounding boxes are provided so notebooks can run without drawing.
- The Overpass API (OpenStreetMap) may rate-limit; if 406 errors occur, wait a
  minute or switch to an alternative endpoint (see notebook comments).


License
-------
Notebooks: provided as-is for educational and research purposes.
GFM data: Copernicus Emergency Management Service (CEMS), EU.
OSM data: OpenStreetMap contributors, ODbL license.
