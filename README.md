# 📈 Enterprise Monthly Price Forecasting & MLOps Dashboard

An end-to-end time-series forecasting and machine learning operations (MLOps) platform designed for commercial commodity and procurement price planning. 

The system leverages historical pricing data to deliver **12-month forward price projections** with statistical confidence intervals, served through a decoupled microservices architecture and visualized via an interactive dashboard with continuous production drift monitoring.

---

## 🚀 Key Dashboard Features

### 1. Forecast & Business Intelligence Dashboard
- **Interactive Price Trajectory:** Visualizes multi-year historical actuals alongside the 12-month future forecast path.
- **Uncertainty Quantification:** Displays dynamic 95% confidence interval bands to assist procurement teams in downside risk management.
- **Executive KPI Summary:** Real-time KPI metric cards highlighting:
  - Latest observed unit price
  - 12-month projected average price
  - Projected net percentage change
  - Upper and lower exposure limits

### 2. Production MLOps & Drift Monitoring
- **Automated Data Hygiene Engine:** Verifies incoming data for schema regularity, missing records, negative price values, and temporal continuity.
- **Statistical Data Drift Detection:** Tracks distribution changes over historical windows using the **Kolmogorov-Smirnov (KS) two-sample test** and **Population Stability Index (PSI)**.
- **Forecast Degradation Auditing:** Evaluates realized actuals against predictions to calculate rolling **Mean Absolute Percentage Error (MAPE)** and residual tracking errors.
- **Automated Retraining Protocol:** Predefined rule triggers that flag the model for re-calibration if rolling MAPE exceeds 10% or PSI exceeds 0.25.

---

## 🏗️ System Architecture

The application is built on a modern, decoupled three-tier microservice architecture:

```
[ Next.js React Dashboard ]
            │  (REST / JSON)
            ▼
[ Django API Gateway & Core App ]  ──► Authentication, RBAC, Business Logic
            │  (Internal HTTP / ASGI)
            ▼
[ FastAPI Inference Microservice ] ──► Low-Latency ML Prediction Engine (ARIMA)
            │
    [ Model Artifacts & Data Layer ]
```

- **Frontend (Next.js / React):** Responsive web interface utilizing modern data visualization libraries (`Recharts` / `Chart.js`) for price paths, KPI panels, and error distributions.
- **Backend Gateway (Django):** Manages user authentication, request throttling, business workflows, and API routing.
- **ML Inference Service (FastAPI):** High-throughput, asynchronous inference service delivering sub-5ms prediction responses with Pydantic schema validation.
- **Forecasting Core (Statsmodels / Scikit-Learn):** Automated stationarity analysis via Augmented Dickey-Fuller (ADF) testing, first-order differencing ($d=1$), and ARIMA modeling.

---

## 📊 Technical Stack

| Layer | Technologies |
| :--- | :--- |
| **Machine Learning / Statistics** | Python, `statsmodels` (ARIMA), `scikit-learn`, `scipy` (KS-Test, PSI), `pandas`, `numpy` |
| **Inference Service** | FastAPI, Uvicorn, Pydantic |
| **Backend API Gateway** | Django, Django REST Framework |
| **Frontend Dashboard** | Next.js, React, Tailwind CSS, Recharts |
| **Visualization & Reporting** | Matplotlib, Seaborn |

---

## 📈 Model Performance & Evaluation

- **Baseline Comparison:** Evaluated against Naive Random Walk and 3-Month Moving Average benchmarks on a 12-month holdout test set.
- **Out-of-Sample Accuracy:** Achieved **9.07% Mean Absolute Percentage Error (MAPE)** and **$417.38 Mean Absolute Error (MAE)**.
- **Forecast Horizon:** 12-Month forward projection with calibrated prediction intervals.

---

## 📂 Project Structure

```
├── price_data.csv                    # Historical monthly price dataset (2005 - 2025)
├── price_forecasting_internship.ipynb # Core notebook with analysis, models & visualizations
├── forecast_model_params.json         # Serialized model parameters & baseline forecast artifact
├── .gitignore                         # Git exclusion rules
└── README.md                          # Project documentation
```

---

## 💻 Getting Started

### 1. Prerequisites
- Python 3.10+
- Jupyter Notebook or JupyterLab

### 2. Installation
```bash
git clone https://github.com/VanitaCSE/Price-Forecasting-Dashboard.git
cd Price-Forecasting-Dashboard
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn scipy
```

### 3. Run the Notebook
```bash
jupyter notebook price_forecasting_internship.ipynb
```
