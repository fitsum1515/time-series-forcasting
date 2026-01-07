# Hybrid Time Series Forecasting and Anomaly Detection

This repository implements a **hybrid framework** for **time series forecasting and anomaly detection**, combining **STL decomposition, SARIMA, and LSTM models**. The pipeline not only predicts future values but also detects **behavioral drifts, shocks, and anomalies**, providing an **early warning scoring system**.

---

## 📊 Project Overview

The workflow follows this procedure:
``` text
Raw Time Series
       │
       ▼
  STL Decomposition
       │
       ├── Trend Component
       ├── Seasonal Component ──► Behavioral Drift Detection
       └── Residual Component ──► Shock / Outlier Detection
                                   │
                                   ▼
                           Anomaly Scoring Engine
                                   │
                     ┌─────────────┴─────────────┐
                     ▼                             ▼
             Anomaly-Cleaned Signal        Early-Warning Risk Scores
                     │
                     ▼
              SARIMA Forecasting Layer
                     │
                     ▼
              LSTM Neural Forecast Layer
                     │
                     ▼
              Future Value + Risk Forecast
```


---

## 🔬 Methodology

1. **STL Decomposition**
   - Decompose time series into:
     - Trend component
     - Seasonal component
     - Residual component
   - Detect **behavioral drifts** (seasonal anomalies) and **shocks/outliers** (residual anomalies) using **control bands**.

   Example anomaly detection equations:

   - Seasonal anomalies:  
     *x<sub>t</sub> > UCL* or *x<sub>t</sub> < LCL*

   - Residual anomalies:  
     *x<sub>t</sub> > UCL* or *x<sub>t</sub> < LCL*

2. **Anomaly Scoring**
   - Combine seasonal and residual deviations into a **total score**.
   - Classify anomalies into levels: `NORMAL`, `LOW`, `MEDIUM`, `HIGH`, `CRITICAL`.

3. **SARIMA Forecasting**
   - Fit SARIMA model on **anomaly-cleaned time series**.
   - Capture **seasonal trends** and predict future values.

   Notation:

     $$
SARIMA(p,d,q)(P,D,Q)_s
$$


4. **LSTM Neural Forecasting**
- Feed **anomaly-cleaned residuals** into LSTM network.
- Model **non-linear dependencies** in the residual component.

Forecasting formula:

$$
\hat{y}_t = \hat{\text{TREND}}_t + \hat{\text{SEASONAL}}_t + (\hat{\text{RESIDUAL}}_t)^{\text{LSTM}}
$$


- All variables have **hats (^)** to indicate predicted components.
- `t` is the time index.
- LSTM is applied **only to the residual** component.

  

5. **Future Forecast and Risk Detection**
- Combine SARIMA and LSTM outputs to produce **future value predictions**.
- Generate **early warning risk scores** for potential anomalies.

---

## 🛠 Features

- **STL Decomposition:** Trend, seasonal, residual extraction  
- **Anomaly Detection:** Residual shocks and behavioral drift detection  
- **Hybrid Forecasting:** SARIMA + LSTM for accurate predictions  
- **Alarm Scoring:** Critical, high, medium, low anomaly levels  
- **Visualization:** Time series plots, STL decomposition, control charts, and forecast graphs  

---

# 📂 Dataset
- **Alcohol_Sales.csv: Monthly alcohol sales data**
- **Columns:**
   1. DATE - timestamp
   2. Sales - monthly sales amount
     
  



