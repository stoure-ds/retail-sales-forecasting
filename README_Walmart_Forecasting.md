# Walmart Weekly Sales Forecasting (Prophet)

Forecast total **weekly retail sales** using time-series modeling to support **demand planning**, **inventory decisions**, and **holiday staffing**.

---

## Business Objective
Retail demand has strong seasonality and sharp holiday spikes. This project builds a forecasting model that:
- captures trend + yearly seasonality
- explicitly models holiday effects
- provides a forward-looking forecast with uncertainty bounds

---

## Dataset
**File:** `Walmart.csv`  
**Rows:** 6,435 store-week records  
**Stores:** 45  
**Date range:** 2010-02-05 to 2012-10-26  
**Key columns:**
- `Store` (store ID)
- `Date` (week start date)
- `Weekly_Sales` (target)
- `Holiday_Flag` (1 = holiday week, 0 = non-holiday)
- `Temperature`, `Fuel_Price`, `CPI`, `Unemployment`

**Target series used for forecasting:** total weekly sales aggregated across all stores.

---

## Approach
1. **Load & clean data**
   - Parse `Date` to datetime
   - Validate schema and missing values

2. **Aggregate sales**
   - Group by `Date` and sum `Weekly_Sales` across stores
   - Create Prophet-ready frame: `ds` (date), `y` (sales)

3. **Modeling**
   - Train **Facebook Prophet** to model:
     - overall trend
     - yearly seasonality
     - holiday spikes (using `Holiday_Flag`)

4. **Evaluation**
   - Hold out the last 12 weeks for testing
   - Report RMSE and compare against a simple baseline (ARIMA used in notebook)

5. **Diagnostics**
   - Inspect decomposition plots (trend / yearly / holiday effects)
   - Review residual behavior to confirm the model captured most structure

---

## Results (from notebook)
- Prophet captures **annual retail seasonality** and **holiday-driven spikes** well.
- Forecasts preserve the repeating seasonal structure and provide useful uncertainty intervals.
- Reported test performance in the notebook: **RMSE ≈ $1.2M (~2–3% of average weekly sales)**.

> Note: Exact results can vary slightly depending on random splits and environment.

---

## Visualizations
### Forecast
![Forecast](forecast_plot.png)

### Model Components (Trend, Holidays, Yearly Seasonality)
![Components](forecast_components.png)

---

## How to Run
### 1) Create environment (recommended)
```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
```

### 2) Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels prophet
```

### 3) Open the notebook
```bash
jupyter notebook "Walmart Store Sales Forecasting.ipynb"
```

---

## Repository Structure
```
.
├── Walmart Store Sales Forecasting.ipynb
├── Walmart.csv
├── forecast_plot.png
├── forecast_components.png
└── README.md
```

---

## Tools Used
- Python: Pandas, NumPy
- Visualization: Matplotlib, Seaborn
- Forecasting: Prophet
- Evaluation: scikit-learn (RMSE), statsmodels (ARIMA baseline)

---

## Next Improvements
- Forecast **per store** (hierarchical forecasting)
- Add **regressors** (CPI, unemployment, fuel price, temperature)
- Add **weekly seasonality** (if intra-month patterns exist)
- Use **cross-validation** (Prophet CV) for more robust error estimates

---
# Walmart Weekly Sales Forecasting 📈

Forecasting large-scale retail demand using time-series modeling (Facebook Prophet) to support inventory planning and holiday staffing decisions.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Forecasting](https://img.shields.io/badge/Time%20Series-Forecasting-orange)
![Prophet](https://img.shields.io/badge/Model-Prophet-success)
![Status](https://img.shields.io/badge/Project-Complete-brightgreen)

---

## Business Problem

Retail demand shows strong seasonality and sharp holiday spikes.  
Accurate forecasting is critical for:

- inventory management
- staffing decisions
- revenue planning
- supply chain optimization

This project builds a forecasting pipeline that models trend, seasonality, and holiday effects in Walmart weekly sales.

---

## Dataset

- 6,400+ weekly store records
- 45 Walmart stores
- 2010–2012 retail period
- Aggregated to total weekly sales

Features include:

- weekly sales (target)
- holiday indicator
- CPI
- unemployment
- fuel price
- temperature

---

## Modeling Approach

1. Aggregate weekly sales across stores
2. Train Prophet model with yearly seasonality
3. Add holiday regressors
4. Evaluate forecast accuracy
5. Inspect trend + seasonal decomposition

The model captures repeating retail cycles and holiday-driven spikes.

---

## Results

| Metric | Value |
|-------|------|
| RMSE | ~$1.2M |
| Error Rate | ~2–3% |
| Seasonality Capture | Strong |
| Holiday Sensitivity | High |
| Forecast Stability | Consistent |

The model successfully reproduces annual retail structure and produces realistic future demand projections.

---

## Forecast Visualization

### Sales Forecast
![Forecast](forecast_plot.png)

### Model Components
![Components](forecast_components.png)

---

## Project Structure

```
walmart-sales-forecast/
│
├── Walmart Store Sales Forecasting.ipynb
├── Walmart.csv
├── forecast_plot.png
├── forecast_components.png
└── README.md
```

---

## Tools Used

- Python
- Pandas / NumPy
- Matplotlib / Seaborn
- Facebook Prophet
- Statsmodels
- Jupyter Notebook

---

## Key Insights

- Retail demand is dominated by yearly seasonal structure
- Holiday spikes drive extreme revenue volatility
- Trend remains stable across years
- Prophet handles non-linear seasonality effectively

---

## Future Improvements

- Store-level hierarchical forecasting
- External regressors (CPI, unemployment)
- Prophet cross-validation
- Ensemble models

---

## Author

**Seydou Toure**  
Data Scientist | Forecasting & Analytics  
Python • SQL • Machine Learning • Time Series

---

## LinkedIn Project Summary

Built a time-series forecasting model using Facebook Prophet to predict Walmart weekly retail sales. Captured strong yearly seasonality and holiday demand spikes, achieving ~2–3% forecasting error. Demonstrated how retail demand is driven more by cyclical structure than random noise, enabling realistic demand planning and operational decision support.

---

## Author
**Seydou Toure**  
Data Scientist | Product & Business Analytics | Python, SQL, Forecasting
