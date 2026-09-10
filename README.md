# 🇮🇹 Italy Natural Hazard Intelligence

## Project 01 – Flash Flood Intelligence in Liguria

### Overview

This project investigates extreme rainfall and flash-flood hazard indicators in Liguria, Italy, with a focus on the Genoa area and the 9–10 October 2014 extreme rainfall event.

The project combines environmental data analysis, statistical assessment, geospatial analysis, and GIS visualization to demonstrate a reproducible workflow for natural hazard intelligence and decision support.

The main workflow is:

**Raw Data → Data Cleaning → Statistical Analysis → Spatial Analysis → GIS Visualization → Hazard Interpretation**

---

## Objectives

- Identify extreme rainfall events from historical observations
- Analyze rainfall intensity and temporal accumulation
- Compare ground-based rainfall observations with gridded precipitation estimates
- Evaluate data completeness and temporal gaps
- Provide spatial context around the rainfall observation station
- Produce GIS-based hazard context maps
- Interpret rainfall characteristics from a natural hazard and engineering perspective

---

## Study Area

The analysis focuses on **Liguria, Italy**, with particular attention to the Genoa area and the **GENOVA - GEIRATO** rainfall station.

The station is located at approximately:

- Latitude: **44.45966° N**
- Longitude: **8.97959° E**
- Elevation: **58 m**

A **10 km spatial buffer** around the station was used to identify nearby municipal areas potentially relevant to the observed rainfall event.

The spatial analysis identified **13 municipalities** intersecting the 10 km station-based context.

Because rainfall observations are available from a single station, the spatial analysis should be interpreted as a **station-based hazard context**, not as a rainfall distribution map for the whole Liguria region.

---

## Key Event

The main case study is the extreme rainfall event of **9–10 October 2014**.

Analysis of the cleaned ARPA station dataset identified:

| Indicator | Result |
|---|---:|
| Event rainfall at station | **559.0 mm** |
| Maximum hourly rainfall | **135.0 mm** |
| Maximum 3-hour accumulation | **215.0 mm** |
| Maximum 6-hour accumulation | **256.6 mm** |
| Maximum 12-hour accumulation | **265.8 mm** |
| Maximum 24-hour accumulation | **438.4 mm** |

The results demonstrate substantial rainfall intensity across both short and longer temporal scales, highlighting the potential severity of the event for flash-flood and urban-flood hazard assessment.

---

## ARPA vs Open-Meteo Comparison

Ground-based ARPA observations were compared with hourly precipitation estimates from Open-Meteo.

For the 9–10 October 2014 event:

| Metric | Result |
|---|---:|
| ARPA event precipitation | **559.0 mm** |
| Open-Meteo event precipitation | **68.0 mm** |
| Difference | **491.0 mm** |
| Event Mean Absolute Error | **10.23 mm** |
| ARPA maximum hourly precipitation | **135.0 mm** |
| Open-Meteo maximum hourly precipitation | **3.8 mm** |

Across the full comparison dataset:

| Metric | Result |
|---|---:|
| Mean Absolute Error | **6.64 mm** |
| Maximum Absolute Error | **133.70 mm** |
| Mean Difference (ARPA − Open-Meteo) | **5.55 mm** |
| MAE excluding maximum discrepancy | **5.44 mm** |

The largest discrepancy occurred during the extreme rainfall period, where the station observation recorded **135.0 mm** while the corresponding Open-Meteo estimate was **1.3 mm**, producing an absolute difference of **133.7 mm**.

These results highlight the difficulty of representing highly localized extreme precipitation using gridded precipitation estimates. The comparison should be interpreted as an evaluation of differences between station observations and gridded estimates, rather than as a determination that one dataset is universally more accurate.

---

## Data Quality Assessment

Temporal consistency was evaluated before calculating rainfall accumulation.

During the 9–10 October event period:

- Expected hourly records: **48**
- Observed records: **46**
- Missing hourly records: **2**
- Number of gaps larger than one hour: **8** in the wider cleaned dataset

The rainfall accumulation analysis therefore used **time-based rolling windows** and excluded windows with insufficient valid observations.

This approach avoids treating missing observations as zero rainfall and provides a more conservative representation of rainfall accumulation.

---

## Spatial Analysis

The spatial component of the project was developed using **GeoPandas** and **QGIS**.

The analysis includes:

- Official Liguria regional boundaries
- Official municipal boundary data
- GENOVA - GEIRATO station location
- A 10 km station-based spatial buffer
- Identification of municipalities within the spatial context
- GIS visualization of the rainfall observation location and surrounding administrative areas

The station and buffer were transformed to **WGS 84 / UTM zone 32N (EPSG:32632)** for metric spatial operations.

---

## GIS Outputs

A dedicated QGIS project was created to visualize the spatial hazard context.

The GIS workflow includes:

- Municipal boundaries
- Liguria regional boundary
- GENOVA - GEIRATO rainfall station
- 10 km station buffer
- Metric station layer
- Saved GeoPackage spatial data

The final GIS project is stored in the `qgis/` directory.

---

## Technologies and Tools

### Programming & Data Analysis

- Python
- Pandas
- NumPy
- Matplotlib

### Geospatial Analysis

- GeoPandas
- Shapely
- Coordinate Reference Systems (CRS)
- Spatial buffering
- Spatial intersection

### GIS

- QGIS
- GeoPackage
- Shapefile
- EPSG:4326
- EPSG:32632

### Development & Reproducibility

- Jupyter Notebook
- Visual Studio Code
- Git
- GitHub

---

## Repository Structure

```text
Italy-Natural-Hazard-Intelligence/
│
├── data/
│   ├── raw/
│   │   ├── ARPA rainfall data
│   │   ├── Open-Meteo data
│   │   ├── municipal boundaries
│   │   ├── Liguria regional boundaries
│   │   └── station metadata
│   │
│   └── processed/
│       ├── extreme_rainfall_events.csv
│       ├── precipitation_comparison.csv
│       ├── severity_summary.csv
│       └── final_hazard_summary.csv
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   └── 02_spatial_analysis.ipynb
│
├── outputs/
│   └── spatial_hazard_context.png
│
├── qgis/
│   ├── flash_flood_hazard.qgz
│   ├── station_genova_metric.gpkg
│   └── station_buffer_10km.gpkg
│
├── .gitignore
├── LICENSE
└── README.md