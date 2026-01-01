# Integrating Retail Demand Forecasting and Inventory Optimization

## Project Overview
This project delivers an end-to-end retail analytics pipeline combining demand forecasting with inventory optimization to improve service levels and reduce operational costs. Using the M5 Forecasting dataset, it benchmarks traditional statistical methods against machine learning and deep learning models, showing how forecast-driven inventory policies outperform classical replenishment strategies. The study aligns forecasting accuracy with inventory KPIs, including fill rate, stockout rate, total cost, and inventory turnover.

## Objectives
- Conduct exploratory data analysis (EDA) to understand sales patterns  
- Develop and compare multiple demand forecasting models  
- Identify the best-performing forecasting approach  
- Integrate forecasts into inventory decision-making  
- Evaluate traditional (s, Q) inventory policies versus ML-driven dynamic replenishment  
- Quantify improvements in service levels and cost efficiency  

## Dataset
**M5 Forecasting – Accuracy Dataset**  
Key files used:  
- `sales_train_validation.csv` – Daily unit sales per item–store  
- `calendar.csv` – Date attributes (events, SNAP, weekdays, seasonality)  
- `sell_prices.csv` – Historical selling prices  

**Subset for demonstration:**  
- State: WI | Store: WI_3 | Category: FOODS | Department: FOODS_2  

## Exploratory Data Analysis (EDA)
- Sales distribution and zero-sales patterns  
- Trend and seasonality (daily, weekly, monthly)  
- Price elasticity and promotional impact  
- Event and SNAP influence  
- Correlation analysis with numerical features  

## Feature Engineering
- Lag features: 1, 7, 14, 28 days  
- Rolling means: 7-day, 28-day  
- Calendar-based features  
- Event and promotion indicators  

## Demand Forecasting Models
- **Statistical:** Holt–Winters, SARIMA  
- **Machine Learning:** XGBoost, LightGBM, CatBoost (best-performing)  
- **Deep Learning:** LSTM  

**Evaluation Metrics:** RMSE, MAE, MAPE, sMAPE  
> CatBoost achieved the lowest RMSE and was used for inventory optimization. Hyperparameter tuning was performed with Optuna.

## Inventory Optimization
- **Baseline Policy:** Traditional (s, Q) continuous-review policy  
- **ML-Driven Policy:** Forecast-driven replenishment (Dynamic ROP = Forecast Demand × Lead Time)  

**Inventory KPIs:**  
- Fill Rate (Service Level)  
- Stockout Rate  
- Total Cost  
- Holding and Ordering Costs  
- Inventory Turnover  

**Results:** Forecast-driven inventory decisions significantly improve service levels, reduce stockouts, lower total costs, and increase turnover.

## Tech Stack
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM, CatBoost, TensorFlow/Keras, Statsmodels, Optuna, Google Colab

## Usage
1. Clone the repository  
```bash
git clone <repo-url>

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) – free for personal, academic, or commercial use, with attribution.
