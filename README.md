# Integrating Retail Demand Forecasting and Inventory Optimization  
*A Forecast-Driven Supply Chain Analytics Framework Using the M5 Dataset*

---

## 1. Project Overview

This project presents an end-to-end analytical framework that integrates **retail demand forecasting** with **inventory optimization** to enhance supply chain efficiency. Rather than evaluating forecasting models in isolation, the study explicitly links forecast accuracy to downstream **inventory performance**, demonstrating how improved predictions translate into operational and financial benefits.

Using the **M5 Forecasting – Accuracy dataset**, multiple statistical, machine learning, and deep learning models are evaluated. The best-performing model is then embedded into an inventory control policy and compared against a traditional baseline approach using key inventory KPIs.

The project emphasizes **practical decision impact**, not only predictive performance.

---

## 2. Objectives

The main objectives of this project are:

- To explore and understand retail sales patterns through exploratory data analysis (EDA)
- To compare classical time-series models with modern machine learning and deep learning approaches for demand forecasting
- To identify the best-performing forecasting model using multiple accuracy metrics
- To integrate demand forecasts into inventory replenishment decisions
- To compare traditional inventory control policies with forecast-driven strategies
- To quantify supply chain improvements using service and cost-related KPIs

---

## 3. Dataset Description

### M5 Forecasting – Accuracy Dataset

The project uses the **M5 Forecasting – Accuracy** dataset released by Walmart, which contains daily sales data at the item–store level.

**Files used:**
- `sales_train_validation.csv` – Historical daily unit sales  
- `calendar.csv` – Calendar features (events, SNAP indicators, weekdays, seasonality)  
- `sell_prices.csv` – Historical selling prices  

Evaluation files are not used, as the focus is on model comparison and inventory simulation rather than competition submission.

### Data Subset

To ensure computational tractability while preserving real-world complexity, a focused subset is selected:

- **State:** Wisconsin (WI)  
- **Store:** WI_3  
- **Category:** FOODS  
- **Department:** FOODS_2  

This subset reflects high-frequency retail demand with strong seasonality and promotional effects.

---

## 4. Exploratory Data Analysis (EDA)

EDA is conducted to understand:

- Demand trends and seasonality  
- Intermittency and volatility across items  
- Effects of promotions and calendar events  
- Price variation over time  

Visualizations include:
- Time-series demand plots
- Distribution analysis
- Seasonality and event impact exploration

Insights from EDA guide feature engineering and model selection.

---

## 5. Feature Engineering

A rich feature set is constructed to capture temporal, price, and calendar effects:

- **Lagged demand features:** 1, 7, 14, 28 days  
- **Rolling statistics:** 7-day and 28-day rolling means  
- **Calendar features:** weekday, month, year  
- **Event features:** event name and event type  
- **Promotional indicators:** SNAP features  
- **Price features:** historical sell prices  

Categorical variables are handled differently depending on the model:
- **CatBoost:** native categorical handling
- **XGBoost / LightGBM:** label encoding

---

## 6. Demand Forecasting Models

### 6.1 Statistical Models
- **Holt–Winters Exponential Smoothing**
- **SARIMA**

These models serve as classical benchmarks and capture trend and seasonality.

---

### 6.2 Machine Learning Models
- **XGBoost**
- **LightGBM**
- **CatBoost**

Tree-based models leverage engineered features and nonlinear interactions.  
**CatBoost**, with native categorical support, consistently outperforms other models.

Hyperparameter tuning for CatBoost is performed using **Optuna** to further improve accuracy.

---

### 6.3 Deep Learning Model (Benchmark)
- **LSTM (Long Short-Term Memory)**

An item-level LSTM model is implemented as a benchmark:
- 28-day sliding window
- Log-transformed demand
- MinMax scaling
- Single LSTM layer with 64 units
- MSE loss function

LSTM performance is evaluated per item and averaged across the subset. While effective, it underperforms tuned tree-based models in this setting.

---

## 7. Model Evaluation

Forecasting performance is assessed using multiple metrics to ensure robustness:

- **RMSE (Root Mean Squared Error)**
- **MAE (Mean Absolute Error)**
- **MAPE (Mean Absolute Percentage Error)**
- **sMAPE (Symmetric MAPE)**

All models are evaluated on a consistent train–test split.  
**Tuned CatBoost achieves the lowest RMSE and MAE**, and is selected for inventory integration.

---

## 8. Inventory Optimization Framework

### 8.1 Baseline Policy
A traditional **continuous-review (s, Q)** inventory policy is implemented using historical average demand.

---

### 8.2 Forecast-Driven Policy
A deterministic forecast-based policy is constructed using CatBoost predictions:

- **Reorder Point (ROP)**  
  \[
  ROP = \text{Forecasted Daily Demand} \times \text{Lead Time}
  \]

- **Order Quantity (Q)**  
  \[
  Q = \text{Forecasted Daily Demand} \times \text{Lead Time}
  \]

No explicit safety stock is included to isolate the impact of improved demand forecasting.

Inventory simulation is conducted for a representative SKU (`FOODS_2_233`).

---

## 9. Inventory Performance Metrics

Inventory policies are evaluated using the following KPIs:

- **Fill Rate (Service Level)**
- **Stockout Rate**
- **Total Cost** (holding + ordering)
- **Inventory Turnover**

Results demonstrate that the forecast-driven policy consistently:
- Improves service levels
- Reduces stockouts
- Lowers total inventory costs
- Increases inventory turnover

---

## 10. Results Summary

Key findings include:

- Machine learning models outperform classical time-series methods
- Tuned CatBoost delivers the most accurate forecasts
- Forecast accuracy improvements translate directly into better inventory performance
- Forecast-driven inventory control outperforms traditional baseline policies across all KPIs

---

## 11. Technology Stack

- **Programming Language:** Python  
- **Data Handling:** Pandas, NumPy  
- **Visualization:** Matplotlib, Seaborn  
- **Statistical Models:** Statsmodels  
- **Machine Learning:** Scikit-learn, XGBoost, LightGBM, CatBoost  
- **Deep Learning:** TensorFlow / Keras  
- **Optimization:** Optuna  
- **Environment:** Google Colab  

---

## 12. How to Run the Project

This project is designed to run in **Google Colab**.

Steps:
1. Clone the repository:
   ```bash
   git clone https://github.com/MasudRana2406/Integrating-Demand-Forecasting-and-Inventory-Optimization.git
   ```bash
1. Open the notebook in **Google Colab**
2. Mount **Google Drive** when prompted
3. Ensure dataset paths match your Drive directory structure
4. Run the notebook sequentially from top to bottom

---

## License

This project is released under the **[MIT License](https://opensource.org/licenses/MIT)** and is free for academic, personal, and commercial use with attribution.
