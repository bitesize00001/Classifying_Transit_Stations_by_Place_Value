# Classifying_Transit_Stations_by_Place_Value

This project analyzes and classifies transit stations in Hamburg, Germany based on their **Place Value** within a **Transit-Oriented Development (TOD)** framework. Using open spatial data and network science, it derives 11 urban indicators from OpenStreetMap (OSM) data and clusters stations using **Affinity Propagation** to identify typologies of walkability, accessibility, and urban form.

---

## Objective

To systematically evaluate the **TOD potential** of station neighborhoods by combining:
- **Street network design** (connectivity, centrality, entropy)
- **Point-of-Interest (POI)** patterns (density, diversity, accessibility)

This analysis supports better planning, equitable transit investment, and the design of walkable, vibrant communities.

---

## Study Area

- **Location**: Metropolitan Hamburg, Germany  
- **Units of Analysis**: 1500×1500m² catchment areas around 136 railway public transport (RPT) stations

---

## Methodology

### Step 1: Street Network Extraction
- Retrieve 1500m catchment around each station using `osmnx.graph_from_point()`
- Compute:
  - Number of nodes / links
  - Average segment length
  - Average node degree
  - Street bearing entropy

### Step 2: POI Feature Extraction
- Download POIs (amenity, shop, leisure) via `osmnx.geometries_from_point()`
- Compute:
  - **Density**: number of POIs
  - **Diversity**: number of unique POI tags
  - **Accessibility**: average POIs within 750m per node (`pandana`)

### Step 3: Centrality Metrics
- Compute average **closeness** and **betweenness** centrality per station using `osmnx.extended_stats()`

### Step 4: Clustering Analysis
- Use `AffinityPropagation` from `sklearn` to group stations with similar Place Values
- Identify **exemplar** stations for each sub-cluster

---

## Indicators Used

| Category            | Indicator                        | Description                            |
|---------------------|----------------------------------|----------------------------------------|
| Diversity           | Number of POI categories         | More diversity = higher TOD potential  |
| Density             | Total POI count                  | More POIs = more amenities             |
| Accessibility       | POIs within 750m per node        | Proximity to destinations              |
| Design              | # of Nodes / Links               | Network complexity                     |
| Design              | Avg Segment Length               | Shorter = better walkability           |
| Design              | Entropy of Street Bearing        | Order/disorder of grid orientation     |
| Topology            | Avg Node Degree                  | Interconnectedness                     |
| Topology            | Clustering Coefficient           | Local clustering of paths              |
| Centrality          | Closeness Centrality             | Reachability from any node             |
| Centrality          | Betweenness Centrality           | Influence as connector                 |

---

## Repository Structure

```bash
├── 0_6_0_Code_for_github_Ch6.ipynb    # Main notebook (Chapter 6 workflow)
├── 0_6_0_input_station_list.csv       # Station coordinates and pre-clustered Node Values
├── results/
│   ├── tod_indicators.csv             # Calculated 11 indicators for each station
│   ├── station_clusters.csv           # Cluster assignments and exemplars
│   └── plots/                         # POI distribution and network plots
├── README.md

## Key Results
- 3-level clustering of 136 stations into sub-clusters (e.g., Cluster 0-0, 0-1, 0-2)
- Assignment of each station to a TOD typology based on its Place Value
- Identification of exemplar stations for in-depth spatial analysis
- Mapping of Hamburg’s TOD landscape on the Node-Place model

---

## Dependencies
- osmnx
- networkx
- pandas, numpy, scipy
- pandana
- scikit-learn
- matplotlib, seaborn

Install via:
pip install osmnx pandana scikit-learn matplotlib

##  Citation
If using this code or analysis, please cite the corresponding academic publication:

Chen, H.-H., Mumm, N., & Carlow, V. (2024).
A computational approach for categorizing street segments in urban street networks based on topological properties. Frontiers in Built Environment.

##　Author
Hsiao-Hui (Helen) Chen, Dr.-Ing.
Urban Data Scientist | Health Informatics | Spatial Network An
