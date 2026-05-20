# GeoAI Flood Risk Assessment & Digital-Twin-Style Replay

## Overview

This project demonstrates a GeoAI workflow for urban flood **risk assessment**, situational awareness, and emergency decision support. It combines a physics-grounded flood model with a trained machine-learning classifier and an interactive, time-stepped replay of a historic storm.

The notebook integrates:

- Real elevation and terrain analysis
- Historical weather retrieval
- Hydrology-based runoff and flood modeling
- A trained flood-classification model (Random Forest)
- Road-network routing and accessibility analysis
- Interactive visualization and a storm-replay slider

The workflow is a research and educational prototype showing how geospatial AI and digital-twin concepts can support urban flood management and disaster response. The demonstration uses **Orlando, Florida** and **Hurricane Ian (2022)** as the example scenario, replaying actual storm-period weather over the study area.

---

## Features

### Physics-Grounded Flood Model
- SCS Curve Number (NRCS TR-55) runoff estimation per land-use class
- Topographic Wetness Index (Beven & Kirkby, 1979)
- D8 flow accumulation over a real digital elevation model
- Dynamic flood-surface estimation driven by cumulative rainfall, wind, and drainage impairment

### GeoAI Flood Classification
- A `RandomForestClassifier` trained to classify flood severity from terrain, hydrology, land-use, population, and storm features
- `KMeans` clustering to identify high-risk hotspots
- Note on training data: the classifier learns from labels produced by the physics model rather than from observed flood extents (see Limitations)

### Weather & Rainfall Analysis
- Historical Hurricane Ian weather via the Open-Meteo archive API (Sept 27 – Oct 2, 2022)
- Rainfall trend and cumulative-rainfall visualization
- Synthetic fallback if the API is unavailable

### Geospatial Analysis
Built with GeoPandas, OSMnx, NetworkX, Shapely, and Folium. Capabilities include real road-network extraction, a spatial analysis grid, terrain-derived layers, and infrastructure mapping.

### Routing & Accessibility
- Real OpenStreetMap drive-network routing via OSMnx and NetworkX
- Shelter and evacuation-exit analysis with flood-aware accessibility screening
- Straight-line fallback when the OSM network is unavailable

### Interactive Visualization
The notebook generates interactive Folium flood maps, a Hurricane Ian replay slider, rainfall plots, risk and classification layers, and infrastructure overlays.

### Emergency Decision Support Concepts
Illustrates flood monitoring, high-risk hotspot identification, shelter and safe-zone screening, and evacuation-route awareness.

---

## Technologies Used

| Category | Tools / Libraries |
|---|---|
| Programming | Python |
| Geospatial Analysis | GeoPandas, OSMnx, Shapely, py3dep |
| Mapping | Folium, branca |
| Data Processing | Pandas, NumPy, SciPy |
| Visualization | Matplotlib |
| Network Analysis | NetworkX |
| Weather Data | Open-Meteo Archive API |
| Machine Learning | Scikit-learn (Random Forest, KMeans) |
| Elevation Data | USGS 3DEP (via py3dep) |
| Interactive Widgets | ipywidgets |

---

## Project Workflow

1. **Environment setup** — install dependencies and configure the notebook.
2. **Define study area** — select a city (Orlando is the default example).
3. **Retrieve weather data** — pull historical Hurricane Ian rainfall and wind from Open-Meteo.
4. **Build geospatial context** — load USGS elevation, derive slope and wetness, build the analysis grid, land-use, and population layers.
5. **Model flood conditions** — apply SCS-CN runoff and topographic wetness to estimate flood surfaces.
6. **Train the GeoAI classifier** — fit a Random Forest on physics-model-labeled samples and identify hotspots.
7. **Visualize risk** — generate interactive maps comparing the physics model and the ML classification.
8. **Routing & accessibility** — extract the OSM road network and screen evacuation routes against flood conditions.
9. **Replay & decision support** — step through the storm with an interactive slider and export the model state.

---

## Installation

### Clone Repository
```bash
git clone <repository-url>
cd <repository-folder>
```

### Install Dependencies
```bash
pip install folium scikit-learn shapely geopandas branca ipywidgets osmnx networkx openmeteo-requests requests-cache retry-requests py3dep xarray rioxarray rasterio scipy
```

---

## Running the Notebook

Launch Jupyter and open `Flood_Detection_Demo.ipynb`, then run the cells sequentially.
```bash
jupyter notebook
```

---

## Running in Google Colab

The notebook also runs in Google Colab. Install dependencies with:
```python
!pip install folium scikit-learn shapely geopandas branca ipywidgets osmnx networkx openmeteo-requests requests-cache retry-requests py3dep xarray rioxarray rasterio scipy
```

### Notes
- Geospatial libraries may take a few minutes to install.
- An internet connection is required for OpenStreetMap, Open-Meteo, and USGS elevation queries.
- Interactive Folium maps and ipywidgets are supported in Colab.

---

## Example Outputs

- Hurricane Ian rainfall trend and cumulative-rainfall plots
- Physics-model flood-depth surface vs. GeoAI flood classification
- Interactive flood and risk maps with infrastructure overlays
- High-risk hotspot clusters and shelter/evacuation routing
- An exported model-state CSV (`geoai_flood_dt_state.csv`)

---

## Research & Educational Context

Developed as a GeoAI and urban flood intelligence demonstration, intended for educational demonstrations, workshops, research prototypes, and GeoAI learning activities.

---

## Limitations

This is a demonstration prototype and should not be treated as a production-grade flood forecasting system.

- **The ML classifier is trained on labels generated by the physics model, not on observed flood extents.** It therefore learns to approximate the simulator and has not been validated against real flood-event data. Reported accuracy reflects agreement with the simulator, not real-world predictive skill.
- The flood model uses a simplified runoff-and-wetness formulation rather than full hydrodynamic (e.g., shallow-water) simulation.
- Land-use and population layers are schematic approximations rather than authoritative datasets.
- Risk scoring uses fixed heuristic weights.
- The "digital twin" here is a replay of a single historic storm, not a live, continuously synchronized model.
- Results depend on the availability and resolution of public datasets and APIs.

---

## Future Improvements

- Validation against observed flood extents and gauge data
- Satellite-based flood segmentation and sensor integration
- Full hydrodynamic modeling
- LLM-assisted emergency briefings
- Dynamic, traffic-aware evacuation optimization
- Live data feeds for closer-to-real-time operation

---

## Acknowledgments

This project uses OpenStreetMap, Open-Meteo weather services, USGS 3DEP elevation data, and the Python open-source geospatial ecosystem. Thanks to the GeoAI and digital-twin research and educational communities.

---

## License

Intended for educational and research demonstration purposes. Please verify external dataset and API licenses before redistribution or commercial deployment.

---

## Contact

**Phani Raja Bharath Balijepalli**
bharathbalijepalli@gmail.com
M.S. Modeling & Simulation
University of Central Florida
