# Evaluation of Velocity Potential Simulation Performance During ENSO Periods Using Seasonal Reforecast Data
# By Jenny Jung


## Introduction
El Niño and La Niña are significant climate phenomena characterized by changes in sea surface temperatures in the equatorial Pacific. During these periods, tropical Pacific convection differs significantly compared to average conditions. Convection activity can be analyzed using variables such as precipitation, outgoing longwave radiation (OLR), and velocity potential.

In this study, I focus on the upper-level velocity potential to examine whether convection patterns during El Niño and La Niña are theoretically well represented. The velocity potential is a variable associated with strong convection. A positive Laplacian of Chi (the velocity potential) indicates upper-level convergence, while a negative Laplacian represents upper-level divergence. This variable allows for a straightforward analysis of the spatial distribution of convergence and divergence over large-scale horizontal fields.

## Data
### 1. Niño 3.4 index
The Nino3.4 index was obtained from the NOAA Physical Sciences Laboratory's "Climate Indices: Monthly Atmospheric and Ocean Time Series" pages. This index represents the SST anomalies in the East-Central Tropical Pacific (5°N-5°S, 170°W-120°W), calculated using NOAA ERSST V5 anomalies by CPC (Climate Prediction Center). The data can be downloaded from the following link: https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii.

### 2. Model Data
The model data used in this study is the Ensemble Seasonal Reforecasts dataset, as described in Huang et al. (2017). The key characteristics of this dataset are as follows:
- Model: NCEP CFSv2 (coupled system including GFS for atmosphere, LSM for land, and MOM4 for ocean).
- Forecast: Initialized in January, April, July, and October with 91-day predictions.
For more details about the model, please refer to [Huang et al., 2017](https://doi.org/10.1175/JCLI-D-16-0642.1).

This study focuses only on the data initialized in January to minimize model errors associated with forecast lead times. The dataset spans from 1980 to 2014.

The primary variables used in this study are 200 hPa u and v wind components, from which velocity potential was calculated.

### 3. ERA5 Reanalysis
To evaluate the performance of the model, the ERA5 reanalysis dataset was used as the reference. This dataset was obtained from CPC, and the variables used were 200 hPa u and v wind components. Since the ERA5 data is provided at an hourly resolution, it was converted to daily averages to align with the model data. Using these variables, the velocity potential was calculated for comparison with the model outputs.

## Methods
### 1. Data Preprocessing
The ERA5 data, originally in hourly resolution, was converted to daily resolution.

[Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/convert2daily_era5.ipynb)

(Daily averages should use all 24-hour data points, but for simplicity, the average was calculated using only the 00, 06, 12, and 18 UTC time steps.)

### 2. Calculating Velocity Potential
Velocity potential was calculated using the u and v wind components with the **windspharm** package.

For more details about the windspharm package, refer to the following link: https://ajdawson.github.io/windspharm/.

To run this package, the following Conda environment configuration is required: **env_windspharm.yml**

  - ERA5 : [Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/calculation_vp200_era5.ipynb)

  - Model : [Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/calculation_vp200_model.ipynb)

### 3. Analysis of Nino3.4 Index and Model Data
The Conda environment required for the analysis is **env_all.yml**
  - Calculating the Correlation Coefficient
: Assess the relationship between the Nino3.4 index and the model's velocity potential.
  - Composites of Velocity Potential Anomalies for ENSO Phases
: Generate composite maps to identify the characteristic anomaly patterns during different ENSO phases.

## Results
### 1. Time Series of the Nino3.4 Index
The figure below shows the time series of the Niño3.4 index during the analysis period from 1980 to 2014. The index clearly highlights periods of El Niño and La Niña events, which are characterized by positive and negative anomalies, respectively.

Observed ENSO Events:
  - El Niño years (red dots): 1983, 1987, 1992, 1995, 1998, 2010
  - La Niña years (blue dots): 1985, 1989, 1999, 2000, 2008, 2011

![Time series of the Nino3.4 index](figures/plot_ts_nino34.png)

[Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/plt_xy_ts_nina34.ipynb)


### 2. Correlation between Niño3.4 and Velocity Potential Anomalies
This analysis was conducted to understand the relationship between the Niño3.4 index and the velocity potential. Specifically, we computed the correlation between the interannual variability of the Niño3.4 index and the interannual variability of velocity potential from both the model and ERA5 data.

The figure below illustrates the correlation results. Significant positive correlations were observed near the Maritime Continent, while significant negative correlations appeared over the central and eastern tropical Pacific.

During El Niño events (when the Niño3.4 index is strongly positive):
  - The upper-level velocity potential over the western Pacific and the Maritime Continent tends to have positive values, indicating upper-level convergence, descending air, and drier conditions near the surface.
  - Over the central and eastern Pacific, the upper-level velocity potential exhibits negative values, indicating upper-level divergence, ascending air, and enhanced precipitation.

Model Performance: These patterns were well captured by the model, demonstrating its ability to simulate the spatial characteristics of velocity potential anomalies associated with ENSO phases.

![Correlation between Niño3.4 and Velocity Potential Anomalies](figures/plot_map_corr_bw_nino34_models.png)

[Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/plt_map_corr_bw_model.ipynb)


### 3. Composite Analysis of Velocity Potential Anomalies for ENSO Phases
The velocity potential anomalies were composited for each ENSO phase: El Niño, La Niña, and Neutral. As expected based on theoretical understanding:
  - During El Niño phases, descending air dominates over the Maritime Continent, indicated by upper-level convergence (positive velocity potential anomalies). In contrast, ascending air dominates over the central Pacific, represented by upper-level divergence (negative velocity potential anomalies).
  - During La Niña phases, the convection system shifts westward, resulting in ascending motion (upper-level divergence) over the Maritime Continent and descending motion (upper-level convergence) along the central Pacific coastline.
  - In Neutral conditions, these patterns are less pronounced and show no significant trends.

**Comparison between ERA5 and Model**
  - El Niño: The model shows stronger upper-level divergence over the central Pacific compared to ERA5.
  - La Niña: The model exhibits more pronounced upper-level convergence (positive anomalies) around the central Pacific near 180° longitude, indicating stronger descending motion during La Niña phases.

![Composite of Velocity Potential Anomalies for Each ENSO Phase](figures/plot_map_comp_anom_each_ph.png)



![Composite Differences in Velocity Potential Anomalies during ENSO](figures/plot_map_comp_diff_anom.png)

[Jupyter notebook link](https://github.com/jyjung907/clim680_project/blob/main/plt_map_comp_anom_model.ipynb)



## Summary
