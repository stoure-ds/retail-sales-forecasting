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

## Author
**Seydou Toure**  
Data Scientist | Product & Business Analytics | Python, SQL, Forecasting
