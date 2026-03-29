## README: The Epidemic Forest in Jakarta

This repository contains the implementation of the algorithms and data processing steps described in the paper:  
**"The epidemic forest reveals the spatial pattern of the spread of acute respiratory infections in Jakarta, Indonesia"** ([Nature Scientific Reports, 2024](https://www.nature.com/articles/s41598-024-58390-3)).

---

## Overview
The project reconstructs the transmission pathways of Acute Respiratory Infections (ARIs) across Jakarta using an algorithm called **Epidemic Forest**. By analyzing spatiotemporal surveillance data, the code identifies how outbreaks shift between regions and identifies the primary "roots" of infection.

## Data Availability
* **Included:** Jakarta's population data and GeoJSON files for geographical area definition, centroid mapping, and visualization.
* **Excluded:** The specific ARI disease data is not provided in this repository due to privacy and public health data restrictions.

---

## Methodology & Notebook Structure

The Jupyter Notebook is organized into the following core stages:

### 1. Infectious Period Identification
Uses **Hierarchical Clustering** to group temporal data and define specific windows of time where the infection is most active across different administrative districts.

### 2. Outbreak Shift Identification
Applying **Hierarchical Clustering** again to detect significant shifts in case clusters over time. This helps in understanding the movement of the disease from one temporal cluster to another.

### 3. Onset Time Determination
Uses **Richard’s Curve** (a generalized logistic function) to model the growth of cases in each area and precisely determine the "onset time"—the exact moment an outbreak begins in a specific location.

### 4. Spatial Data Processing
Maps complex geographical areas into discrete points using **Centroid Mapping**:
* **Geographical Coordinates:** Calculated for each administrative area from the provided GeoJSON.
* **Neighbor Analysis:** Connectivity is determined based on the distance between these centroids to simplify spatial transmission analysis.

### 5. Epidemic Forest Algorithm
The core algorithm that links individual outbreaks into a "forest" of transmission trees. It calculates the likelihood of transmission between areas based on spatial proximity and the timing of case onsets.

---

## Technical Stack

The implementation utilizes the following Python libraries:

* **Data Handling:** `pandas`, `numpy`, `json`
* **Spatial Analysis:** `geopandas`, `contextily` (for basemaps)
* **Mathematical Optimization:** `scipy.optimize` (for Richard's Curve fitting)
* **Network/Graph Theory:** `networkx` (to build the epidemic forest)
* **Visualization:** `matplotlib`, `seaborn`
* **Time Utilities:** `datetime`, `dateutil`
