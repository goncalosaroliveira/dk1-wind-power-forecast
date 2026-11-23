# DK1 Wind Power Forecast

This is my first project in power markets, focusing on Denmark's DK1 bidding zone and the relationship between weather forecasts and wind power generation.

## Project Overview

The project analyses the relationship between weather conditions and hourly wind power generation in Denmark's DK1 bidding zone.

The main objectives are to:
- Understand how weather conditions affect wind generation.
- Develop and compare machine learning models.
- Forecast wind generation using weather forecasts available 24 hours ahead.
- Evaluate model performance through testing and walk-forward backtesting.

The analysis covers 2025 and includes both onshore and offshore wind generation.

## Data Sources

Two main sources were used:

- **Open-Meteo:** Historical weather data and archived weather forecasts.
- **Energinet:** Actual wind generation data from the `GenerationProdTypeExchange` dataset, filtered for DK1.

Weather data was collected from six locations across Denmark and averaged into one hourly series representing DK1.

The main weather variables were wind speed at 100m, temperature at 2m and shortwave radiation.

Total wind generation was calculated as the sum of onshore and offshore production.

## Methodology

The project follows these steps:

1. Data collection and preparation.
2. Exploratory Data Analysis.
3. Model training and comparison.
4. Hyperparameter tuning.
5. Final model evaluation.
6. Day-Ahead forecasting.
7. Walk-Forward backtesting.

Five models were tested: Linear Regression, Multiple Linear Regression, Polynomial Regression, Random Forest and Gradient Boosting.

Gradient Boosting achieved the best validation results. The final configuration used 200 trees, a learning rate of 0.05 and a maximum tree depth of 2.

## Results

### Model Evaluation

The tuned Gradient Boosting model was trained on the first 80% of the dataset and evaluated on the remaining 20%.

**Test results:**
- MAE: 347.373
- RMSE: 454.965
- R²: 0.879

### Day-Ahead Forecast

The model was also tested using weather forecasts from Open-Meteo's Previous Runs API, using the `previous_day1` variables to simulate a 24-hour forecast horizon.

**Test results:**
- MAE: 385.110
- RMSE: 509.651
- R²: 0.848

Using forecast weather resulted in higher prediction errors than using observed weather, as expected. However, the model maintained a good level of predictive performance.

### Walk-Forward Backtesting

An expanding-window backtest was conducted from October to December 2025. The model was retrained at the beginning of each month using the data available up to that point.

**Overall results:**
- MAE: 383.105
- RMSE: 506.773
- R²: 0.850

October covers only the period from 20 to 31 October, while November and December cover the full months.

## Limitations

The project uses one year of historical data and only three weather variables. Other factors affecting wind generation, such as turbine availability, outages, curtailment and grid constraints, were not included.

The archived weather forecasts also do not fully reproduce the exact forecast information available at the Day-Ahead market deadline. Further testing with additional years and operational data would improve the analysis.

## Conclusion

The results show that weather forecasts can provide useful information for predicting wind power generation ahead of delivery. The Day-Ahead model achieved an R² of 0.848 on the test dataset, while the walk-forward backtest produced an overall R² of 0.850.

This project provides a foundation for further work on European power price forecasting and energy trading strategies.

## Project Files

- `DK1_Wind_Power_Forecast.ipynb` - Full analysis, model development and results.
- `dk1_wind_power_forecast.py` - Python code export.

## Data Sources

- [Open-Meteo](https://open-meteo.com/)
- [Energinet — Energi Data Service](https://www.energidataservice.dk/)
