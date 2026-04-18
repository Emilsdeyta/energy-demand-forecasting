# Energy Demand Forecasting — PJM Regions

Time series forecasting of hourly electricity consumption across 12 PJM regions using XGBoost with lag-based feature engineering.

## Results

| Metric | Value |
|--------|-------|
| MAE    | 537.45 MW |
| MAPE   | 3.38% |
| R²     | 0.99 |

> Achieved **3.38% MAPE** across all 12 regions — well within the 2–5% industry benchmark for energy demand forecasting.

## Dataset

Source: [PJM Hourly Energy Consumption](https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption) via Kaggle

Covers hourly load data from **1998 to 2018** across 12 regional transmission zones:
`PJM_Load` `PJME` `PJMW` `NI` `AEP` `DAYTON` `DUQ` `DOM` `COMED` `FE` `DEOK` `EKPC`

## Methodology

### 1. Preprocessing
- Parsed datetime index and converted to column
- Sorted by region and timestamp

### 2. Feature Engineering
| Feature | Description |
|---------|-------------|
| `hour` | Hour of day (0–23) |
| `dayofweek` | Day of week (0=Mon, 6=Sun) |
| `month` | Month of year |
| `is_weekend` | Binary flag for Saturday/Sunday |
| `lag_24` | Load 24 hours prior (same hour yesterday) |
| `lag_168` | Load 168 hours prior (same hour last week) |
| `rolling_mean_24` | 24-hour rolling average load |

### 3. Model
- **Algorithm:** XGBoost Regressor
- **Split:** 80% train / 20% test (time-based)
- **Target:** Hourly load (MW)
- All 12 regions trained in a single model using `region` as an encoded feature

### 4. Evaluation
- Mean Absolute Error (MAE)
- Mean Absolute Percentage Error (MAPE)
- R² Score

