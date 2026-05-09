# Complete Project Plan According to Teacher Requirements

Your project will follow the SAME structure as the wildfire project PDF, but adapted for:

# “GIS and Machine Learning-Based Urban Growth Susceptibility Mapping System”

The teacher already gave the workflow in the PDF. 
You just replace wildfire concepts with urban-growth concepts.

---

# FINAL PROJECT STRUCTURE

| Teacher Wildfire Project | Your Urban Project          |
| ------------------------ | --------------------------- |
| Burned vs Unburned       | Urban vs Non-Urban          |
| Wildfire susceptibility  | Urban growth susceptibility |
| Fire factors             | Urbanization factors        |
| Fire risk map            | Urban growth map            |

---

# SOFTWARE YOU NEED

## Required Tools

| Tool                                                                                                         | Purpose              |
| ------------------------------------------------------------------------------------------------------------ | -------------------- |
| [Google Earth Engine](https://earthengine.google.com/?utm_source=chatgpt.com)                                | Satellite processing |
| [QGIS](https://qgis.org/?utm_source=chatgpt.com) or [ArcGIS](https://www.arcgis.com/?utm_source=chatgpt.com) | GIS visualization    |
| [Google Colab](https://colab.research.google.com/?utm_source=chatgpt.com)                                    | Python ML training   |
| [Leaflet.js](https://leafletjs.com/?utm_source=chatgpt.com)                                                  | Web GIS application  |

---

# STEP 1 — DEFINE STUDY AREA

## Recommended:

Karabük

Choose:

* city boundary
* district
* urban center + surrounding area

---

# STEP 2 — COLLECT SATELLITE IMAGES

## Use:

Sentinel-2 imagery from Google Earth Engine.

## Years:

* Before = 2015
* After = 2025

Goal:
Compare urban expansion over time.

---

# STEP 3 — VISUALIZE BEFORE & AFTER IMAGES

In GEE:

* Load 2015 RGB image
* Load 2025 RGB image
* Add dates

Exactly like wildfire before/after comparison.

Output:

* Before urbanization map
* After urbanization map

---

# STEP 4 — CREATE LABELED POINTS

This matches teacher requirement exactly. 

---

# YOUR LABELS

| Class     | Label |
| --------- | ----- |
| Urban     | 1     |
| Non-Urban | 0     |

---

# CREATE POINTS

Manually place:

| Type             | Amount |
| ---------------- | ------ |
| Urban points     | 500    |
| Non-Urban points | 500    |

Total:
1000 points

---

# WHERE TO PLACE POINTS

## Urban Points

Place on:

* buildings
* roads
* industrial areas
* residential zones

## Non-Urban Points

Place on:

* forest
* agriculture
* grassland
* water

---

# EXPORT SHAPEFILES

Save:

* UrbanPoints.shp
* NonUrbanPoints.shp

Merge:

* samplepoints.shp

Exactly same as wildfire workflow.

---

# STEP 5 — PREPARE FEATURES (VERY IMPORTANT)

Teacher asks for 15 features. 

You need raster layers affecting urban growth.

---

# RECOMMENDED 15 FEATURES

| Feature                  | Source         |
| ------------------------ | -------------- |
| NDVI                     | Sentinel-2     |
| NDBI                     | Sentinel-2     |
| Elevation                | SRTM DEM       |
| Slope                    | DEM            |
| Aspect                   | DEM            |
| Distance to roads        | OpenStreetMap  |
| Distance to city center  | GIS            |
| Land Surface Temperature | MODIS          |
| Population density       | WorldPop       |
| Night lights             | VIIRS          |
| Soil type                | FAO            |
| Rainfall                 | CHIRPS         |
| Temperature              | ERA5           |
| Distance to rivers       | GIS            |
| Existing land use        | ESA WorldCover |

---

# IMPORTANT INDICES

## NDVI

NDVI=\frac{NIR-Red}{NIR+Red}

Vegetation indicator.

---

## NDBI

NDBI=\frac{SWIR-NIR}{SWIR+NIR}

Urban/build-up indicator.

---

# STEP 6 — EXTRACT FEATURE VALUES

This creates your ML dataset.

For every point:
extract values from all 15 raster layers.

Result:

| Point | NDVI | NDBI | Elevation | Slope | Temp | Label |
| ----- | ---- | ---- | --------- | ----- | ---- | ----- |
| P1    | 0.2  | 0.6  | 350       | 5     | 31   | 1     |
| P2    | 0.8  | -0.4 | 500       | 18    | 22   | 0     |

---

# EXPORT DATASET

Save as:

* training.csv
  or:
* Inputs.txt
* Label.txt

Exactly matching teacher requirement. 

---

# STEP 7 — MACHINE LEARNING MODEL

Teacher requires 3 classifiers. 

---

# Recommended Models

| Model         | Difficulty      |
| ------------- | --------------- |
| Random Forest | Easy + accurate |
| SVM           | Medium          |
| Decision Tree | Easy            |

---

# TRAINING PROCESS

In Python:

1. Load CSV
2. Split train/test
3. Train models
4. Evaluate accuracy
5. Compare models

Metrics:

* Accuracy
* Precision
* Recall
* F1-score

---

# STEP 8 — GENERATE URBAN GROWTH SUSCEPTIBILITY MAP

Use best model.

Predict probability of urban expansion for every pixel.

Output classes:

* High urban growth
* Medium
* Low

This is your final susceptibility map.

---

# STEP 9 — VISUALIZATION IN GIS

Use:

* QGIS
  or
* ArcGIS

Create:

* before/after maps
* susceptibility heatmaps
* urban expansion visualization
* legend + scale + north arrow

---

# STEP 10 — WEB GIS APPLICATION

Teacher requires interactive system. 

---

# SIMPLE WEB APP IDEA

Use Leaflet.

Features:

* show urban growth map
* zoom/pan
* layer switch
* click to view risk
* compare years

---

# EASIEST WEB APP STACK

| Part     | Tool          |
| -------- | ------------- |
| Frontend | HTML/CSS/JS   |
| Map      | Leaflet       |
| Tiles    | OpenStreetMap |
| Overlay  | GeoJSON       |

---

# STEP 11 — FINAL REPORT

Your report should contain:

---

# REPORT STRUCTURE

## 1. Introduction

* urban growth problem
* GIS importance
* ML importance

---

## 2. Study Area

* Karabük description
* maps

---

## 3. Data Collection

* Sentinel-2
* DEM
* OpenStreetMap
* climate datasets

---

## 4. Methodology

Explain workflow:

1. image collection
2. preprocessing
3. point labeling
4. feature extraction
5. ML training
6. susceptibility mapping

---

## 5. Machine Learning

* models used
* hyperparameters
* evaluation

---

## 6. Results

* accuracy tables
* maps
* discussion

---

## 7. Web GIS System

* screenshots
* explanation

---

## 8. Conclusion

* findings
* limitations
* future work

---

# FINAL DELIVERABLES

## You Must Submit

### 1. Report PDF

### 2. Web GIS application

### 3. Training dataset

### 4. GIS maps

### 5. Source code

---

# IMPORTANT ADVICE

## DO NOT:

* choose huge Türkiye-wide study area
* use too many features initially
* overcomplicate deep learning

---

# DO:

* finish complete pipeline
* create good visuals
* keep workflow clean
* make interactive map

---

# SIMPLE SUCCESS STRATEGY

## Best Practical Setup

| Part     | Recommended               |
| -------- | ------------------------- |
| Area     | Karabük                   |
| Images   | Sentinel-2                |
| ML       | Random Forest             |
| GIS      | QGIS                      |
| Web app  | Leaflet                   |
| Features | 10–15                     |
| Labels   | 500 urban + 500 non-urban |

This is VERY achievable for your course project and matches teacher requirements closely.
