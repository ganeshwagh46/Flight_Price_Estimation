# Flight_Price_Estimation
## 👤 Analyst: Ganesh Wagh
📅 Date: Feb 2024

## 📌 Executive Summary
This project builds an end-to-end pipeline to estimate flight ticket prices using journey-level data (dates, times, airlines, routes, stops, durations). Through systematic EDA, feature engineering, and robust modeling pipelines, I evaluated several machine-learning approaches — notably Random Forest and XGBoost — and compared their predictive performance using MAE, RMSE, and R². The goal is a reproducible workflow that supports accurate price prediction and simple deployment for inference.

## Key objectives:

Clean and standardize raw flight data for modelling.

Engineer interpretable features (departure/arrival times, duration in minutes, route encoding, stop counts).

Build reproducible preprocessing pipelines and evaluate tree-based models.

Compare model performance and provide an inference-ready pipeline for predictions.

## 📂 Data Overview
Source: Public/collected flight journey datasets (e.g., Kaggle datasets, airline timetables, scraped fare snapshots).

Typical columns expected:

Date_of_Journey

Dep_Time, Arrival_Time

Airline, Source, Destination

Route, Duration, Total_Stops

Price (target)

Period covered: Depends on the dataset uploaded to data/; the notebooks support multi-year data.

Transformations applied:

Parsed datetime fields and extracted day/month/hour features.

Converted duration text to total minutes.

One-hot or target encoding for categorical features; imputation for missing values.

Optional log-transform of Price during training to stabilize variance.

## 🛠 Methodology

### Exploratory Data Analysis (EDA)

Visual checks for missingness, outliers, and seasonal patterns by route and airline.

Summary statistics and pairwise comparisons.

### Preprocessing & Feature Engineering

ColumnTransformer pipelines for separate numeric and categorical flows.

Imputation, scaling (where appropriate), and encoding consolidated into a single Pipeline to prevent leakage.

Derived features: journey day-of-week, departure hour (cyclical encoding option), duration minutes, route popularity metrics.

### Modeling

Baseline: linear regression / simple mean predictor.

Primary models: Random Forest Regressor and XGBoost Regressor.

Hyperparameter tuning via RandomizedSearchCV and cross-validation; time-aware or grouped CV recommended for temporal data.

### Evaluation & Forecasting

Metrics: MAE (primary), RMSE, R².

Residual diagnostics and feature importance checks (permutation or SHAP recommended).

Save best pipeline with joblib for inference.

## 📑 Key Findings

Categorical route-related features (Source, Destination, Airline, Stops) are among the strongest predictors of price.

Duration and number of stops significantly influence price distribution and model predictions.

Tree-based models (Random Forest / XGBoost) outperform simple linear baselines in predictive accuracy and handle heterogeneous feature types effectively.

Consolidating preprocessing into a single Pipeline prevents leakage and makes inference straightforward.

## 📈 Recommendations

Use the saved pipeline (models/final_pipeline.joblib) for inference and prototyping; wrap it in a small API (Flask/FastAPI) for production.

Improve predictive power by adding exogenous features where available: booking lead time, seasonality flags, holiday indicators, or route-level demand metrics.

Consider ensembling the best tree models and calibrating prediction intervals for uncertainty quantification.

Implement rolling validation and automated retraining to handle non-stationarity in fares.
