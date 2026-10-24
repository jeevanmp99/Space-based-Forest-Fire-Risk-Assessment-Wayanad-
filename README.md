# Space-Based Forest Fire Risk Assessment and Mapping: A Case Study of Wayanad District, Kerala

A geospatial modeling study assessing forest fire susceptibility across the ecologically sensitive terrain of Wayanad District in the Western Ghats of Kerala, India. The project employs multi-source satellite observations, topographic parameters, human proximity metrics, and meteorological records within a **Frequency Ratio (FR)** bivariate statistical framework, validated via **Receiver Operating Characteristic (ROC)** curve analysis.

---

## 📌 Overview

Wildfires represent a major driver of forest degradation, biodiversity loss, and atmospheric pollution across tropical montane ecosystems. In the Western Ghats, seasonal dry spells combined with steep topography and anthropogenic pressure significantly escalate wildfire vulnerability. 

This study leverages remote sensing and GIS geoprocessing to:
- Establish a multi-decadal historical wildfire inventory (2005–2024).
- Statistically evaluate spatial relationships between historical ignitions and geo-environmental conditioning factors.
- Quantify susceptibility tiers across Wayanad District to support forest management, fire patrol planning, and disaster mitigation.

```text
             [ Multi-Source Spatial Data Ingestion ]
  (Fire Inventory, CartoDEM, Sentinel-2, OpenStreetMap, NASA Giovanni)
                                │
                                ▼
                 [ Conditioning Factor Conditioning ]
  (Elevation, Slope, TWI, Dist. to Roads/Settlements, Rain, Temp, Wind)
                                │
                                ▼
               [ Bivariate Frequency Ratio (FR) Modeling ]
           • FR = (N_fire / N_total_fire) / (N_class / N_total)
           • Relative Frequency (RF) & Predictive Ratio (PR)
                                │
                                ▼
            [ Forest Fire Susceptibility Index (FFSI) ]
                 Low  |  Moderate  |  High Susceptibility
                                │
                                ▼
                [ Model Accuracy & Verification ]
                     AUC-ROC Curve (AUC = 0.74)
```

---

## 🗺️ Study Area

**Wayanad District** is situated in the northeastern upland plateau of Kerala, nested within the biodiversity hotspot of the Western Ghats.

- **Geographic Extent:** Approximately $2,132\text{ km}^2$
- **Elevation Range:** 700 m to 2,100 m above mean sea level (MSL)
- **Administrative Boundaries:** Bordered by the Nilgiris district of Tamil Nadu, the Mysore and Kodagu districts of Karnataka to the north and east, Malappuram district to the south, and Kozhikode and Kannur districts to the west.
- **Ecological Context:** Characterized by rugged ridgelines, moist deciduous forests, semi-evergreen tracts, shola-grassland mosaics, and extensive commercial plantations (tea, coffee, and rubber).

<p align="center">
  <img src="assets/Fig%202.Study%20area%20of%20the%20Wayanad%20district.jpg" alt="Fig 2. Study area of the Wayanad district" width="90%">
</p>

---

## 🛠️ Data Sources & Conditioning Factors

The analysis integrates three categories of spatial conditioning parameters:

| Category | Factor / Layer | Resolution / Source | Description |
| :--- | :--- | :--- | :--- |
| **Historical Fire Inventory** | 345 Fire Incident Hotspots | FSI / MODIS & S-NPP (2005–2024) | Primary ground-truth dependent variable |
| **Topographic Factors** | Elevation (DEM)<br>Slope Gradient<br>Topographic Wetness Index (TWI) | ISRO Bhoonidhi Hub (CartoDEM) | Terrain steepness, moisture retention, and aspect control fuel dryness and fire spread velocity |
| **Anthropogenic Factors** | Distance to Roads<br>Proximity to Settlements | OpenStreetMap (OSM)<br>Sentinel-2 LULC Derivations | Proxies for human ingress, slash-and-burn practices, and incidental ignition sources |
| **Meteorological Factors** | Mean Annual Rainfall<br>Surface Temperature<br>Wind Speed | NASA Giovanni Data Portal | Climatic triggers influencing fuel flammability and fire propagation |

---

## ⚙️ Analytical Methodology

<p align="center">
  <img src="assets/Fig%201.Flow%20Chart%20of%20Methodology.jpg" alt="Fig 1. Flow Chart of Methodology" width="90%">
</p>

The spatial probability of fire occurrence was modeled using the **Frequency Ratio (FR)** bivariate probabilistic approach:

1. **Spatial Discretization:** Conditioning raster layers were classified into discrete thematic intervals.
2. **Frequency Ratio Formulation:**
   $$\text{FR} = \frac{N_{fire}(L_i) / N_{fire\_total}}{N_{area}(L_i) / N_{area\_total}}$$
   Where $N_{fire}(L_i)$ is the number of fire ignition points in class $L_i$, and $N_{area}(L_i)$ is the total area of class $L_i$.
3. **Relative Frequency (RF) & Predictive Ratio (PR):**
   $$\text{RF} = \frac{\text{FR}_i}{\sum \text{FR}}$$
   $$\text{PR} = \frac{\text{Max(RF)} - \text{Min(RF)}}{\text{Min(RF)}}$$
4. **Susceptibility Zonation:** The cumulative Forest Fire Susceptibility Index (FFSI) was synthesized by summing factor layers weighted by their predictive ratios:
   $$\text{FFSI} = \sum (\text{RF} \times \text{PR})$$

---

## 📊 Results & Susceptibility Distribution

The resulting continuous susceptibility index was reclassified into three discrete risk tiers:

| Susceptibility Class | Area ($\text{km}^2$) | Percentage of Total Area |
| :--- | :--- | :--- |
| **Low** | 822.000 $\text{km}^2$ | 38.92% |
| **Moderate** | 989.419 $\text{km}^2$ | 46.85% |
| **High** | 300.749 $\text{km}^2$ | 14.23% |
| **Total Analyzed** | **2,112.168 $\text{km}^2$** | **100.00%** |

<p align="center">
  <img src="assets/Fig%203.Fire%20Susceptibility%20Map.jpg" alt="Fig 3. Fire Susceptibility Map" width="90%">
</p>

### Parameter Sensitivity & Key Findings
- **High-Risk Acreage:** Approximately **$300.75\text{ km}^2$ (14.23%)** of Wayanad falls into the **High Susceptibility** tier, heavily concentrated along exposed ridge slopes, degraded forest fringes, and deciduous transition zones.
- **Primary Driving Factors:** **Slope gradient** and **proximity to roads** exhibited the strongest statistical correlation with fire occurrences, each scoring a maximum predictive weight of **$1.81$**. Steep slopes preheat upslope fuels and accelerate convective fire fronts, while road corridors facilitate human access.
- **Secondary & Influencing Factors:** **Elevation** and **Topographic Wetness Index (TWI)** significantly modulate microclimate and fuel moisture levels.
- **Least Influencing Factor:** **Wind speed** yielded the lowest predictive weight (**$1.00$**), as local topographic channeling dominates over regional wind patterns in dense canopies.

---

## 📈 Model Validation

Model performance was validated using the **Area Under the Curve - Receiver Operating Characteristic (AUC-ROC)** metric by evaluating True Positive Rates against False Positive Rates across classification thresholds:

<p align="center">
  <img src="assets/Fig%204.ROC%20Curve%20indicating%20Fair%20accuracy.png" alt="Fig 4. ROC Curve indicating Fair accuracy" width="70%">
</p>

- **Validation Metric:** $\text{AUC} = \mathbf{0.74}$
- **Classification Rating:** The model demonstrates **Fair Accuracy ($0.70 \le \text{AUC} < 0.80$)**, confirming that bivariate frequency ratios effectively capture historical fire ignition distributions for regional baseline planning.

---

## 📂 Repository Structure

```text
├── assets/
│   ├── Fig 1.Flow Chart of Methodology.jpg
│   ├── Fig 2.Study area of the Wayanad district.jpg
│   ├── Fig 3.Fire Susceptibility Map.jpg
│   └── Fig 4.ROC Curve indicating Fair accuracy.png
└── README.md
