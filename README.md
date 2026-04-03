# Life Expectancy Prediction Using Supervised Learning

A supervised machine learning project that predicts life expectancy using health and socioeconomic indicators from WHO data. Two regression models — Ridge Regression and Random Forest — are implemented, tuned, and compared.

---

## Project Overview

This project uses the WHO Life Expectancy Fixed dataset to predict a country's life expectancy in years. The goal was to identify which model better captures the complexity of real-world health data and determine which factors most strongly drive life expectancy across countries.

---

## Dataset

- **Source:** [WHO Life Expectancy Fixed — Kaggle](https://www.kaggle.com/datasets/lashagoch/life-expectancy-who-updated)
- **Rows:** 2,864
- **Features:** 17 health and socioeconomic indicators
- **Target Variable:** Life Expectancy (years)
- **Countries:** 179
- **Years covered:** 2000–2015

### Key Features
- Adult Mortality
- Under-five Deaths
- HIV/AIDS incidents
- Immunization rates (Hepatitis B, Polio, Diphtheria)
- GDP per capita
- Schooling
- BMI
- Alcohol consumption
- Economy status (Developed / Developing)

---

## Requirements

Install the required libraries before running the notebook:

```bash
pip install pandas scikit-learn matplotlib
```

---

## How to Run

1. Download the dataset from Kaggle and save it as `Life-Expectancy-Data-Updated.csv` in the same folder as the notebook
2. Open the notebook in Google Colab or any Python environment
3. Run all cells in order from top to bottom

---

## Project Steps

1. Load the dataset and inspect its shape and columns
2. Drop non-predictive columns: `Country`, `Region`, `Year`
3. Define features (`X`) and target variable (`y`)
4. Split data into 80% training and 20% test sets
5. Apply `StandardScaler` to normalize feature scales
6. Train and tune Ridge Regression using `GridSearchCV`
7. Train and tune Random Forest using `RandomizedSearchCV`
8. Evaluate both models using R², MSE, and MAE
9. Visualize results with scatter plots, bar charts, and feature importance

---

## Models

### Ridge Regression
- Regularized linear regression with L2 penalty
- Hyperparameter tuned: `alpha` — tested values: 0.01, 0.1, 1, 10, 100
- Tuning method: `GridSearchCV` with `cv=5`
- Best alpha: **1**

### Random Forest
- Ensemble model that builds multiple decision trees and averages predictions
- Hyperparameters tuned: `n_estimators`, `max_depth`, `min_samples_split`
- Tuning method: `RandomizedSearchCV` with `n_iter=10`, `cv=5`
- Best parameters: `n_estimators=100`, `max_depth=10`, `min_samples_split=5`

---

## Results

| Metric | Ridge Regression | Random Forest |
|--------|-----------------|---------------|
| R² Score | 0.9777 | 0.9960 |
| MSE | 1.853 | 0.333 |
| MAE | 1.09 years | 0.444 years |

Random Forest outperformed Ridge on every metric. The performance gap indicates that the relationship between health indicators and life expectancy is non-linear, which Ridge's straight-line assumption cannot fully capture.

---

## Key Finding

Feature importance from Random Forest revealed that **under-five deaths (0.75)** and **adult mortality (0.25)** completely dominate all other features. GDP, schooling, immunization rates, and all other features contribute very little in comparison.

---

## Technologies Used

- Python
- Pandas
- Scikit-learn
- Matplotlib
- Google Colab
