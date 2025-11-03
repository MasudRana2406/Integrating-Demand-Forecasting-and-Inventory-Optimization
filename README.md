# Retail Demand Forecasting & Inventory Optimization (LSTM Model)

**Author:** Masud Rana
**Website:** [Data4Fashion.com](https://data4fashion.com)
**GitHub:** [MasudRana2406](https://github.com/MasudRana2406)

---

## Project Overview

This project predicts future product sales using deep learning (LSTM) on the M5 Forecasting – Walmart Sales dataset.
The model helps retailers plan inventory, reduce stockouts, and improve service levels — transforming sales history into actionable insights.

---

## Dataset Information

**Source:** [Kaggle – M5 Forecasting Accuracy](https://www.kaggle.com/competitions/m5-forecasting-accuracy)

**Files used:**

* `sales_train_validation.csv` → Historical daily sales for each item and store
* `calendar.csv` → Date mapping and events (used for aligning sales timeline)

**Data size:**

* 30,490 products × 1,913 days of daily sales
* Period: January 2011 – May 2016

---

## Business Objective

To forecast future daily sales for any product or store and assist decision-makers in:

* Determining optimal inventory levels
* Planning production or replenishment
* Reducing holding costs and lost-sales risk

---

## Methodology

| Step                           | Description                                                                                         |
| ------------------------------ | --------------------------------------------------------------------------------------------------- |
| **1. Data Loading & Cleaning** | Read `sales_train_validation.csv` and `calendar.csv`, align 1913 daily records with calendar dates. |
| **2. Product Selection**       | Dynamically identify product and store (e.g., `HOBBIES_1_001_CA_1`).                                |
| **3. Data Preprocessing**      | Scale sales data to [0,1] range and create rolling time windows (past 30 days → next day).          |
| **4. Model Building**          | Two-layer LSTM network with dropout for regularization.                                             |
| **5. Evaluation**              | Compare actual vs predicted sales on the last 20% of data.                                          |
| **6. Forecasting**             | Predict next 30 days and visualize the future trend.                                                |

---

## Model Architecture

```text
Input (30 timesteps)
   ↓
LSTM(64, return_sequences=True)
   ↓
Dropout(0.2)
   ↓
LSTM(32)
   ↓
Dense(1)
```

**Loss Function:** Mean Squared Error (MSE)
**Optimizer:** Adam
**Epochs:** 25 with early stopping

---

## Results

### Sample Product Forecast

![LSTM Forecast](results/sample_forecast.png)

**Observation:**

* The model effectively captures seasonal and weekly patterns.
* Forecasted sales follow realistic retail fluctuations — useful for inventory and supply-chain decisions.

---

## Next 30-Day Forecast (Example)

| Date       | Predicted Sales |
| ---------- | --------------: |
| 2016-05-23 |           212.7 |
| 2016-05-24 |           219.4 |
| 2016-05-25 |           225.8 |
| ...        |             ... |

*(Saved automatically as `forecast_next_30_days.csv`)*

---

## Key Learnings

* Proper date alignment between `calendar.csv` and sales columns (`d_1`–`d_1913`) is crucial.
* LSTM models can generalize sales patterns from raw transactional data without explicit time features.
* A small change (window size, dropout, learning rate) can significantly impact forecasting stability.

---

## Future Improvements

| Enhancement                   | Goal                                             |
| ----------------------------- | ------------------------------------------------ |
| Add `sell_prices.csv`         | Include price sensitivity and promotion effects. |
| Integrate event/holiday flags | Capture spikes during promotions or holidays.    |
| Compare with classical models | Evaluate ARIMA, Prophet, and XGBoost baselines.  |
| Build Streamlit dashboard     | Enable interactive forecast visualization.       |

---

## Tech Stack

**Languages:** Python
**Libraries:** Pandas, NumPy, Matplotlib, Scikit-Learn, TensorFlow/Keras
**IDE:** Google Colab
**Version Control:** Git & GitHub

---

## Author’s Note

> “I built this project to bridge my retail merchandising experience with data science — using machine learning to drive better forecasting and inventory decisions. This is part of my Data4Fashion portfolio.”

**Connect with me:** [LinkedIn – Masud Rana](https://linkedin.com/in/masudranads)

