# Integrating Retail Demand Forecasting and Inventory Optimization to Enhance Supply Chain Efficiency

## Project Overview

This project demonstrates an end-to-end retail analytics pipeline that integrates demand forecasting with inventory optimisation to improve service levels and reduce operational costs.
Using the M5 Forecasting dataset, the study compares traditional statistical methods with modern machine learning and deep learning models, and evaluates how forecast-driven inventory policies outperform classical replenishment strategies.

The project is designed from both an academic and industry perspective, aligning forecasting accuracy with downstream inventory KPIs such as fill rate, stockout rate, total cost, and inventory turnover.

## Objectives

- Analyze retail sales behavior using exploratory data analysis (EDA)

- Build and compare multiple demand forecasting models

- Identify the best-performing forecasting model

- Integrate forecasts into inventory decision-making

- Compare traditional (s, Q) inventory policy with ML-driven dynamic replenishment

- Quantify improvements in service level and cost efficiency

## Dataset

_M5 Forecasting – Accuracy Dataset_

Files used:

   01. sales_train_validation.csv → Daily unit sales per item–store
   
   02. calendar.csv → Date attributes (events, SNAP, weekdays, seasonality)
   
   03. sell_prices.csv → Historical selling prices

Subset used for demonstration:

- State: WI

- Store: WI_3

- Category: FOODS

- Department: FOODS_2

## Exploratory Data Analysis (EDA)

- Sales distribution and zero-sales analysis

- Trend and seasonality (daily, weekly, monthly)

- Price elasticity analysis

- Event and SNAP impact

- Correlation analysis with numerical features

## Feature Engineering

- Lag features: 1, 7, 14, 28 days

- Rolling means: 7-day, 28-day

- Calendar-based features

- Event and promotion indicators

## Demand Forecasting Models

### Statistical Models

- Holt–Winters Exponential Smoothing

- SARIMA

### Machine Learning Models

- XGBoost

- LightGBM

- CatBoost (best-performing model)

### Deep Learning

- LSTM

### Evaluation Metrics

RMSE, MAE, MAPE, sMAPE

CatBoost achieved the lowest RMSE and was selected for downstream inventory optimization.

Hyperparameter tuning was performed using Optuna.

## Inventory Optimisation
- Baseline Policy: Traditional (s, Q) inventory policy or  Continuous-review fixed reorder point based on historical mean demand

- ML-Driven Policy: Forecast-driven replenishment

   Dynamic reorder point: ROP=Forecast Demand×Lead Time

Demand generated from tuned CatBoost model

Inventory KPIs Evaluated

- Fill Rate (Service Level)

- Stockout Rate

- Total Cost

- Holding Cost

- Ordering Cost

### Inventory Turnover

Results clearly show that forecast-driven inventory decisions:

- Improve fill rate

- Reduce stockouts

- Lower total inventory cost

- Increase inventory turnover


### Tech Stack: 
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM, CatBoost, TensorFlow / Keras, Statsmodels, Optuna,  Google Colab

### How to Run

- Clone the repository

- Open the notebook in Google Colab

- Mount Google Drive

- Install required libraries:

_pip install catboost optuna_

Run the notebook sequentially
