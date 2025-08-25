# simultaneous forecasting of multiple time-series variables
Forecasting electricity demand, supply, and market price using TFT-multi and quantile regression
## Overview
This project focuses on **simultaneous forecasting of multiple time-series variables** in the electricity market using Temporal Fusion Transformer-multi (TFT-multi).  
We predict **electricity demand, supply, and market price** for the Shikoku and Chugoku regions in Japan. By forecasting multiple variables together, the model can capture interdependencies among variables, improving both accuracy and consistency.

## Data
- **Target variables**: demand, supply, price (hourly data)  
- **Dynamic covariates**: interconnection flow, pumped storage, batteries, temperature, weather, wind speed, precipitation, nuclear, thermal, hydro, geothermal, biomass, solar generation  
- **Static covariates**: region (Shikoku/Chugoku), population, day of week, hour, month, day  

- Dataset: 1-year hourly data, 90% training / 10% test split  
- Forecast horizon: 36-hour input → 12-hour output

## Model
- **Temporal Fusion Transformer-multi (TFT-multi)**  
- Multi-horizon probabilistic forecasting using quantile regression (0.1, 0.5, 0.9)  
- Captures temporal dependencies and inter-series correlations  
- Handles missing values via masked loss function  

- **Optimization**: Adam optimizer, learning rate 1e-3  
- **Evaluation metric**: MAE (normalized by region)

## Results
- TFT-multi successfully forecasts demand, supply, and price while maintaining inter-series consistency  

### MAE Results

| Region | Variable | Mean MAE | Median MAE | n |
|--------|----------|----------|------------|---|
| Chugoku | Demand  | 0.012    | 0.012      | 35 |
| Chugoku | Supply  | 0.017    | 0.015      | 35 |
| Chugoku | Price   | 0.019    | 0.018      | 35 |
| Shikoku | Demand  | 0.009    | 0.004      | 35 |
| Shikoku | Supply  | 0.014    | 0.005      | 35 |
| Shikoku | Price   | 0.019    | 0.018      | 35 |

## Example Visualizations

### Shikoku Region
![Shikoku Demand](results/shikoku_demand.png)
*Shikoku electricity demand: actual vs predicted*

![Shikoku Supply](results/shikoku_supply.png)
*Shikoku electricity supply: actual vs predicted*

![Shikoku Price](results/shikoku_price.png)
*Shikoku electricity market price: actual vs predicted*

### Chugoku Region
![Chugoku Demand](results/chugoku_demand.png)
*Chugoku electricity demand: actual vs predicted*

![Chugoku Supply](results/chugoku_supply.png)
*Chugoku electricity supply: actual vs predicted*

![Chugoku Price](results/chugoku_price.png)
*Chugoku electricity market price: actual vs predicted*


## How to Run
1. Install dependencies via `requirements.txt`  
2. Run `notebooks/train_model.ipynb` for data preprocessing and model training  
3. Run `notebooks/predict.ipynb` for forecasting and visualization

## References
1. Bryan Lim et al., Temporal Fusion Transformers for Interpretable Multi-Horizon Time Series Forecasting, 2021  
2. He & Chiang, TFT-multi: Simultaneous Forecasting of Vital Sign Trajectories in the ICU, 2024  
3. Shikoku Electric Power Network, https://www.yonden.co.jp  
4. Chugoku Electric Power Network, https://www.energia.co.jp  
5. JEPX, https://www.jepx.jp  
6. Japan Meteorological Agency, https://www.jma.go.jp
