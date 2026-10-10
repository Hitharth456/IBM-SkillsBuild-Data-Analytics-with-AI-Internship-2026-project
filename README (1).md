# Used Car Price Analytics and Price Prediction

**AICTE | IBM SkillsBuild Data Analytics with AI Internship 2026**  
Conducted by BharatCares in association with AICTE  
**Student:** Hitharth Dasari

---

## Project Overview

A complete end-to-end **Data Analytics and Artificial Intelligence** project that analyses real web-scraped used car listing data and builds a machine learning model to predict used car prices. The project covers the full data science lifecycle — from raw data cleaning through to an interactive web prediction interface and a REST API backend.

**All Python code is contained in a single Jupyter notebook**: `HitharthDasari_UsedCarPriceAnalytics.ipynb`.

The backend (`backend_api.py`) and frontend (`streamlit_app.py`) source code are written **directly inside notebook cells** using Jupyter's `%%writefile` magic. An evaluator reading the notebook sees the complete, readable source code for every component — no separate source file needs to be opened.

---

## Problem Statement

Buyers and sellers in the used car market often lack objective, data-driven pricing tools. Vehicle prices depend on many interacting factors — brand, model year, mileage, accident history, number of previous owners, and colour. This project uses machine learning to provide accurate, data-driven price estimates based on these characteristics.

---

## Objectives

- Analyse real web-scraped used car market data
- Clean and preprocess the raw dataset
- Identify key factors that influence used car prices
- Perform thorough exploratory data analysis (EDA)
- Create meaningful, presentation-quality visualisations
- Train and compare multiple regression ML models
- Select and interpret the best-performing model
- Build a working price prediction system
- Provide an interactive Streamlit frontend and a FastAPI backend
- Demonstrate a full end-to-end Data Analytics + AI solution

---

## Dataset

| Property | Value |
|---|---|
| Filename | `car_web_scraped_dataset.csv` |
| Source | Kaggle (web-scraped used car listings) |
| Total rows (raw) | 2,840 |
| Rows after cleaning | 2,312 (528 duplicates removed) |
| Columns (raw) | 6: `name`, `year`, `miles`, `color`, `condition`, `price` |
| Target column | `price_usd` (cleaned from `price`) |
| Price range | $5,995 – $97,998 (after 1st–99th percentile capping) |
| Unique brands | 42 |
| Year range | 2000 – 2024 |
| Missing values | 0 |

**Kaggle Dataset Link:** https://www.kaggle.com/datasets (search: "car web scraped dataset")

---

## Technologies Used

| Library | Version | Purpose |
|---|---|---|
| pandas | 3.0.0 | Data loading and manipulation |
| numpy | 2.4.1 | Numerical operations |
| matplotlib | 3.10.8 | Data visualisation |
| seaborn | 0.13.2 | Statistical visualisation |
| scikit-learn | 1.9.1 | ML models, preprocessing, evaluation |
| joblib | 1.6.0 | Model persistence |
| streamlit | 1.64.0 | Interactive web frontend |
| fastapi | 0.141.1 | REST API backend |
| uvicorn | 0.53.0 | ASGI server for FastAPI |
| ipywidgets | 8.1.9 | Jupyter notebook widgets |

---

## Project Workflow

```
Raw CSV Dataset
      ↓
Data Loading (pandas)
      ↓
Data Cleaning
  - Remove duplicates (528 removed)
  - Convert price, miles to numeric
  - Parse color, condition columns
  - Extract brand from car name
  - Cap price outliers (1st–99th percentile)
      ↓
Exploratory Data Analysis
  - Price distribution, mileage, brand, year, owners, accidents
  - 10 visualisation plots
  - Statistical analysis
      ↓
Feature Engineering
  - vehicle_age, miles_per_year, has_accident, brand, exterior_color
      ↓
Preprocessing Pipeline
  - StandardScaler (numerical) + OneHotEncoder (categorical)
  - ColumnTransformer → scikit-learn Pipeline (no data leakage)
      ↓
Train/Test Split (80/20, random_state=42)
      ↓
Model Training & Comparison
  - Linear Regression
  - Decision Tree Regressor
  - **Linear Regression  ← BEST (highest Test R²)**
  - Decision Tree Regressor
  - Random Forest Regressor
  - Gradient Boosting Regressor
      ↓
Model Evaluation (MAE, MSE, RMSE, R²)
      ↓
Best Model: Linear Regression  |  Test R² = 0.2935  |  Test MAE = $6,636
Note: Train R² = 0.5936. Gap indicates overfitting — tuning recommended.
      ↓
Model Saving (joblib → best_model_pipeline.pkl)
      ↓
Prediction System
  ┌────────────────────────────────────────────┐
  │  Python predict_price()  ← notebook §18   │
  │  FastAPI POST /predict   ← notebook §20   │  backend_api.py
  │  Streamlit → FastAPI     ← notebook §21   │  streamlit_app.py
  └────────────────────────────────────────────┘
```

---

## Project Structure

```
used_car_price_project/
│
├── RishwanthReddyD_UsedCarPriceAnalytics.ipynb   ← SINGLE SOURCE OF ALL CODE
├── car_web_scraped_dataset.csv                    ← Dataset (provided, never modified)
├── requirements.txt                               ← All dependencies with exact versions
├── README.md                                      ← This file
├── RishwanthReddyD_UsedCarPriceAnalytics_ProjectReport.docx  ← Project report
│
│   ── Generated automatically when the notebook runs ──
├── best_model_pipeline.pkl                        ← Saved ML pipeline (joblib)
├── model_metadata.pkl                             ← Model metadata (brands, colors, metrics)
├── backend_api.py                    ← FastAPI backend  (%%writefile cell in notebook §20)
├── streamlit_app.py                  ← Streamlit frontend (%%writefile cell in notebook §19)
│
│   ── Visualisation plots (created by notebook) ──
├── plot_price_distribution.png
├── plot_price_vs_miles.png
├── plot_price_vs_age.png
├── plot_avg_price_by_brand.png
├── plot_price_by_owners.png
├── plot_price_by_accidents.png
├── plot_correlation_heatmap.png
├── plot_avg_price_by_year.png
├── plot_top_colors.png
├── plot_brand_volume.png
├── plot_model_comparison.png
├── plot_feature_importance.png
└── plot_actual_vs_predicted.png
```

---

## Installation

**Prerequisites:** Python 3.9 or higher, pip

```bash
# Clone or download the project folder
# Navigate to the project directory

# Install all required dependencies
pip install -r requirements.txt
```

---

## How to Run the Notebook

```bash
# Option 1: JupyterLab
jupyter lab RishwanthReddyD_UsedCarPriceAnalytics.ipynb

# Option 2: Classic Jupyter Notebook
jupyter notebook RishwanthReddyD_UsedCarPriceAnalytics.ipynb

# Option 3: VS Code
# Open the .ipynb file directly in VS Code with the Jupyter extension

# Run all cells: Kernel → Restart & Run All
```

The notebook will automatically:
1. Load and clean the dataset
2. Generate all 13 visualisation plots
3. Train and compare all 4 regression models
4. Save `best_model_pipeline.pkl` and `model_metadata.pkl`
5. Write `backend_api.py` via `%%writefile` cell (Section 20 — full source visible in notebook)
6. Write `streamlit_app.py` via `%%writefile` cell (Section 19 — full source visible in notebook)
7. Launch the FastAPI server in a background thread

---

## How to Launch the Frontend (Streamlit)

After running the notebook:

```bash
streamlit run streamlit_app.py
```

Then open **http://localhost:8501** in your browser.

The app has two pages:
- **Dashboard** — dataset statistics and analytics charts
- **Price Prediction** — input form with Predict Price button

---

## How the Backend Works (FastAPI)

After running the notebook, the backend can be started with:

```bash
python backend_api.py
```

Or directly with uvicorn:

```bash
uvicorn backend_api:app --host 0.0.0.0 --port 8000
```

API endpoints:
- `GET /` — API status and model info
- `GET /health` — health check
- `POST /predict` — predict used car price

**Example request:**
```json
POST http://localhost:8000/predict
{
  "brand": "Toyota",
  "year": 2020,
  "miles": 35000,
  "exterior_color": "Black",
  "accidents": 0,
  "owners": 1
}
```

**Example response:**
```json
{
  "predicted_price_usd": 22450.00,
  "model_used": "Random Forest"
}
```

Interactive API docs: **http://localhost:8000/docs**

---

## Machine Learning Models

| Model | Description |
|---|---|
| **Linear Regression** | **Baseline linear model — BEST MODEL (highest Test R²)** |
| Decision Tree Regressor | max_depth=10 to prevent overfitting |
| Random Forest Regressor | 200 estimators |
| Gradient Boosting Regressor | 200 estimators, learning_rate=0.1 |

**Preprocessing pipeline:** `StandardScaler` for numerical features + `OneHotEncoder` for categorical features, wrapped in a `ColumnTransformer` — no data leakage.

---

## Evaluation Metrics

Regression metrics used (no classification metrics):

| Metric | Description |
|---|---|
| MAE | Mean Absolute Error — average dollar error |
| MSE | Mean Squared Error |
| RMSE | Root Mean Squared Error |
| R² | Coefficient of determination (proportion of variance explained) |

---

## Actual Results (Best Model — Linear Regression)

| Metric | Value |
|---|---|
| Test R² | **0.2935** |
| Train R² | **0.5936** (gap indicates overfitting) |
| Test MAE | **$6,636** |
| Test RMSE | **$13,460** |

Note: Price outlier clipping was removed to avoid data leakage. The full comparison table is in the executed notebook (Section 15).

---

## Key Insights

1. **Mileage** shows a moderate-to-strong negative association with price (r≈-0.52) in this dataset
2. **Vehicle age** is negatively associated with price (r≈-0.44). Older vehicles tend to be listed at lower prices
3. **Premium brands** (BMW, Mercedes-Benz, Audi) have an observed average price ~$7,157 (~30%) higher than standard brands — an observed difference, not a causal claim
4. **Accident history** is negatively associated with price (r≈-0.18). Vehicles without accidents have higher average prices
5. **Single-owner vehicles** have a higher observed average price than multi-owner vehicles
6. Black, White, Gray, and Silver are the most common exterior colours

---

## Future Scope

- Add fuel type, transmission, engine size, and trim level features
- Use XGBoost, LightGBM, or CatBoost for potentially higher accuracy
- Hyperparameter tuning with GridSearchCV or Optuna
- SHAP values for per-prediction explainability (Explainable AI)
- Cloud deployment on IBM Cloud, AWS, or Azure
- Mobile application consuming the FastAPI backend
- Real-time scraping to retrain on fresh market data

---

## References

- Dataset: [Kaggle — Car Web Scraped Dataset](https://www.kaggle.com)
- [scikit-learn documentation](https://scikit-learn.org)
- [pandas documentation](https://pandas.pydata.org)
- [Streamlit documentation](https://docs.streamlit.io)
- [FastAPI documentation](https://fastapi.tiangolo.com)
- [IBM SkillsBuild](https://skillsbuild.org)

---

*AICTE | IBM SkillsBuild Data Analytics with AI Internship 2026 — Rishwanth Reddy D*
