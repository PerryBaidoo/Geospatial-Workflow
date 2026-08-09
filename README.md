# Geospatial Workflow

A Python-based geospatial analysis workflow developed for spatial data processing, land parcel analysis, road-network analysis, and multispectral remote sensing analysis of Tarkwa.

## Project Overview

This project demonstrates the application of Python-based geospatial and remote sensing techniques to analyse spatial datasets within Tarkwa.

The workflow is divided into two main parts:

- **Part A:** Vector-based geospatial analysis using land parcels, roads, buildings, and water bodies.
- **Part B:** Multispectral raster analysis and land-cover classification using spectral indices.

## Objectives

The workflow was developed to:

- Inspect and process geospatial datasets using Python.
- Examine and transform coordinate reference systems.
- Analyse land parcels based on land use, area, value, and registration status.
- Perform spatial analysis involving roads, buildings, and land parcels.
- Generate road buffers and determine affected land parcels.
- Visualise land-use and land-value distributions.
- Calculate multispectral vegetation, water, built-up, soil, and burn-related indices.
- Produce true-colour and false-colour composites.
- Perform threshold-based land-cover classification.
- Evaluate classification performance using a confusion matrix and overall accuracy.
- Investigate potential mining/degraded land areas in Tarkwa.

## Technologies and Libraries

The project uses:

- Python
- Jupyter Notebook
- GeoPandas
- Pandas
- NumPy
- Matplotlib
- Matplotlib-Scalebar
- Scikit-learn
- GeoJSON
- NumPy `.npz` raster data

## Part A — Vector Geospatial Analysis

### 1. Land Parcel Analysis

The land parcel dataset is loaded and inspected to determine:

- Number of land parcels
- Attribute structure
- Geometry information
- Coordinate Reference System (CRS)
- Spatial extent

The parcel data is transformed to **UTM Zone 30N (EPSG:32630)** for projected spatial analysis.

### 2. Land Use Analysis

The workflow analyses land parcels based on:

- Land-use type
- Parcel area
- Land value
- Registration status
- Tenure type

The analysis includes filtering residential parcels greater than 500 m², calculating average land values, grouping parcels by land use, and identifying the most valuable parcels.

### 3. Road Buffer Analysis

Road data is transformed to UTM coordinates and a **50 m buffer** is generated around the road network.

The buffer is dissolved into a single geometry and its total area is calculated in hectares.

The workflow also identifies land parcels intersecting the 50 m road corridor.

### 4. Building and Parcel Spatial Analysis

A spatial join is performed between land parcels and building features to determine:

- Parcels containing/intersecting buildings
- Parcels without associated buildings

### 5. Geospatial Visualisation

Maps are produced to visualise:

- Land-use distribution and road networks
- Continuous distribution of land parcel values
- Water bodies

The maps include cartographic elements such as:

- North arrow
- Scale bar
- Legends
- Map titles

## Part B — Multispectral Remote Sensing Analysis

Multispectral data for Tarkwa is loaded from a NumPy `.npz` dataset.

The workflow uses:

- Blue
- Green
- Red
- Near Infrared (NIR)
- Short-Wave Infrared 1 (SWIR-1)
- Short-Wave Infrared 2 (SWIR-2)

### Spectral Indices

The following spectral indices are calculated:

| Index | Purpose |
|---|---|
| NDVI | Vegetation assessment |
| NDWI | Water-related feature assessment |
| NDBI | Built-up area assessment |
| SAVI | Vegetation analysis with soil adjustment |
| NBR | Burned/degraded area assessment |

For each index, the workflow calculates minimum, maximum, and mean values.

## Image Visualisation

The workflow produces:

- True Colour Composite (TCC)
- False Colour Composite (FCC)
- Spectral index visualisations

Histogram stretching using the 2nd and 98th percentiles is applied to improve image visualisation.

## Land Cover Classification

A threshold-based classification is implemented using spectral indices.

The classification includes:

1. Dense Vegetation
2. Sparse Vegetation
3. Urban / Built-up
4. Bare Soil
5. Water

The number and percentage of pixels assigned to each class are calculated.

## Accuracy Assessment

The classified land-cover image is compared with the available ground-truth land-cover mask.

The assessment includes:

- Overall classification accuracy
- Confusion matrix
- Visualisation of the confusion matrix

Mean NDVI values are also calculated for each land-cover class to assess whether the spectral behaviour is physically consistent with the assigned class.

## Mining / Degraded Land Analysis

Potential mining or degraded areas within Tarkwa are identified using a combination of NDVI and NDBI thresholds.

The workflow calculates:

- Number of identified pixels
- Total area in square metres
- Total area in hectares

## Project Structure

```text
Geospatial-Workflow/
│
├── Geospatial workflow.ipynb
├── README.md
├── .gitignore
│
└── Data/
    ├── land_parcels.geojson
    ├── roads.geojson
    ├── buildings.geojson
    ├── water_bodies.geojson
    └── tarkwa_multispectral.npz## How to Use

1. Clone or download this repository.
2. Install the required Python libraries.
3. Ensure the required datasets are available in the appropriate directories.
4. Open `Geospatial workflow.ipynb` in Jupyter Notebook or JupyterLab.
5. Run the notebook cells sequentially.
