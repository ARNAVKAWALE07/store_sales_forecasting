# 📈 Retail Sales Forecasting

A time-series forecasting system that predicts future sales across multiple store locations, helping managers make smarter inventory and stocking decisions ahead of time.

---

## 🔍 Problem Statement

Retail stores lose significant revenue every year through two problems: **overstocking** (cash tied up in unsold inventory) and **understocking** (lost sales due to empty shelves). This project builds location-level sales forecasts that automatically account for seasonality, trends, and holidays — so store managers can plan proactively instead of reactively.

---

## 🎯 Results

| Metric | Score |
|--------|-------|
| Forecast Accuracy Improvement | +20% over naive baseline |
| Models Evaluated | ARIMA, Facebook Prophet |
| Stores Covered | Multiple locations |
| Forecast Horizon | 30-day ahead prediction |

---

## 🗂️ Project Structure

```
store_sales_forecasting/
│
├── data/
│   ├── raw/                    # Original sales data
│   └── processed/              # Cleaned & resampled time series
│
├── notebooks/
│   ├── 01_EDA.ipynb            # Trend, seasonality & holiday analysis
│   ├── 02_preprocessing.ipynb  # Resampling, missing dates, outliers
│   ├── 03_arima.ipynb          # ARIMA modelling & stationarity tests
│   ├── 04_prophet.ipynb        # Facebook Prophet modelling
│   └── 05_evaluation.ipynb     # Model comparison & final results
│
├── src/
│   ├── preprocess.py           # Time series pipeline functions
│   ├── arima_model.py          # ARIMA training & forecasting
│   └── prophet_model.py        # Prophet training & forecasting
│
├── dashboards/
│   ├── sales_forecast.pbix     # Power BI dashboard
│   └── sales_forecast.twbx    # Tableau workbook
│
├── requirements.txt
└── README.md
```

---

## ⚙️ Workflow

```
Raw Sales Data → EDA → Stationarity Testing → Model Selection → Forecasting → Dashboard
```

### 1. Exploratory Data Analysis
- Decomposed time series into **trend, seasonality, and residual** components
- Identified weekly and monthly sales cycles across store locations
- Detected holiday spikes (Diwali, Christmas, year-end) that significantly impacted demand
- Visualised store-by-store performance variation

### 2. Data Preprocessing
- Resampled daily transaction data to weekly aggregates for stable modelling
- Filled missing dates with forward-fill and interpolation
- Removed outliers caused by data entry errors using IQR-based filtering
- Created holiday indicator features for Prophet

### 3. Stationarity Testing
- Applied **Augmented Dickey-Fuller (ADF) Test** to check stationarity per store
- Applied differencing where required for non-stationary series
- Selected model per store based on ADF results and ACF/PACF plots

### 4. Model Training & Comparison

| Model | RMSE | MAE | Best For |
|-------|------|-----|----------|
| Naive Baseline | High | High | Benchmark only |
| ARIMA | Medium | Medium | Stationary series |
| **Facebook Prophet** | **Low** | **Low** | Seasonal + holiday data |

- Prophet outperformed ARIMA on stores with strong seasonal patterns and holiday effects
- ARIMA was competitive on stores with more stable, stationary sales trends
- Final model selected per store based on cross-validated RMSE

### 5. Forecasting
- Generated **30-day ahead forecasts** with confidence intervals per store
- Outputs include upper/lower bounds for risk-aware inventory planning

---

## 📊 Interactive Dashboards

Built in both **Power BI** and **Tableau**:
- Store-level forecast vs. actual comparison
- Drill-down by location, time period, and product category
- Holiday impact visualisation
- Inventory risk flags (predicted demand vs. current stock)

---

## 🛠️ Tech Stack

- **Language:** Python 3.10
- **Data:** Pandas, NumPy
- **Time Series Models:** Facebook Prophet, Statsmodels (ARIMA)
- **Visualisation:** Matplotlib, Seaborn, Power BI, Tableau
- **Statistical Testing:** ADF Test, ACF/PACF Analysis
- **Environment:** Jupyter Notebook, VS Code

---

## 🚀 How to Run Locally

```bash
# 1. Clone the repo
git clone https://github.com/ARNAVKAWALE07/store_sales_forecasting.git
cd store_sales_forecasting

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run EDA notebook
jupyter notebook notebooks/01_EDA.ipynb

# 4. Run forecasting
jupyter notebook notebooks/04_prophet.ipynb
```

---

## 📊 Dataset

- **Source:** [Store Sales — Time Series Forecasting, Kaggle](https://www.kaggle.com/competitions/store-sales-time-series-forecasting)
- **Size:** Multi-store, multi-year daily sales transactions
- **Target:** `sales` (daily revenue per store)

---

## 📌 Key Learnings

- Prophet significantly outperforms ARIMA when holidays and seasonality dominate the signal
- Stationarity testing is essential before model selection — skipping this step leads to misleading ARIMA results
- Store-level modelling beats a single global model: each location has a unique demand pattern
- Confidence intervals are as important as point forecasts for practical inventory decisions

---

## 👤 Author

**Arnav Kawale**
- 📧 arnav.kawale@gmail.com
- 🔗 [LinkedIn](https://www.linkedin.com/in/arnav-kawale-a23934235/)
- 💻 [GitHub](https://github.com/ARNAVKAWALE07)

