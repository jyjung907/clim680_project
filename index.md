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
  - Calculating the Correlation Coefficient
Assess the relationship between the Nino3.4 index and the model's velocity potential.
  - Composites of Velocity Potential Anomalies for ENSO Phases
Generate composite maps to identify the characteristic anomaly patterns during different ENSO phases.



## Results
### 1. ENSO 


### 2. 


### 3.

