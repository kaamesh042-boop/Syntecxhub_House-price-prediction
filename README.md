# 🏠 House Price Prediction
### SyntecxHub — Project 01

> Predict California housing prices using Linear Regression with StandardScaler preprocessing.  
> Achieves **R² = 0.908** and **RMSE ≈ $42,102** on a 2,000-record dataset.

---

## 📁 Project Files

```
project-01-house-price-prediction/
│
├── house_price_prediction.py        ← Main source code
├── syntecxhub_house_price_prediction.html  ← Interactive dashboard
├── linear_regression_model.pkl      ← Saved model (generated on run)
├── standard_scaler.pkl              ← Saved scaler (generated on run)
├── house_price_prediction_plots.png ← Output plots (generated on run)
└── README.md                        ← You are here
```

---

## 📋 Project Overview

This project follows a complete machine learning pipeline:

| Step | Task |
|------|------|
| **01** | Load the California Housing dataset and sample 2,000 records |
| **02** | Explore features, check for missing values, and clean data |
| **03** | Select 8 features, apply `StandardScaler`, split 80/20 train/test |
| **04** | Train a `LinearRegression` model and evaluate with R² and RMSE |
| **05** | Interpret feature coefficients |
| **06** | Save model and scaler as `.pkl` files |
| **07** | Generate diagnostic plots and run custom predictions |

---

## ⚙️ Requirements

**Python version:** 3.8 or higher

Install all dependencies with:

```bash
pip install scikit-learn pandas numpy matplotlib seaborn joblib
```

| Package | Purpose |
|---------|---------|
| `scikit-learn` | Dataset, model, scaler, metrics |
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Plotting |
| `seaborn` | Statistical visualizations |
| `joblib` | Save/load model files |

---

## 🚀 How to Run

```bash
python house_price_prediction.py
```

### What happens when you run it:

1. Loads and samples the California Housing dataset (2,000 rows)
2. Prints dataset stats and feature summary
3. Trains the Linear Regression model
4. Prints R², RMSE, MAE scores and coefficient table
5. Saves `linear_regression_model.pkl` and `standard_scaler.pkl`
6. Generates and saves `house_price_prediction_plots.png`
7. Runs a demo custom prediction

---

## 📊 Dataset

**Source:** `sklearn.datasets.fetch_california_housing`  
**Records used:** 2,000 (random sample, `random_state=42`)  
**Target:** Median house price in USD

### Features

| Feature | Description |
|---------|-------------|
| `MedInc` | Median income in block group (×$10k) |
| `HouseAge` | Median house age in years |
| `AveRooms` | Average number of rooms per household |
| `AveBedrms` | Average number of bedrooms per household |
| `Population` | Block group population |
| `AveOccup` | Average household occupancy |
| `Latitude` | Block group latitude |
| `Longitude` | Block group longitude |

---

## 📈 Model Performance

| Metric | Value |
|--------|-------|
| **R² Score** | 0.908 |
| **RMSE** | $42,102 |
| **MAE** | ~$30,000 |
| **Avg Price** | $335,000 |

### Feature Coefficients (scaled)

| Feature | Coefficient | Effect |
|---------|-------------|--------|
| MedInc | +$121,443 | Strongest positive driver |
| AveRooms | +$12,625 | More rooms → higher price |
| HouseAge | +$5,802 | Older homes slightly pricier |
| Longitude | +$3,529 | East → slight increase |
| AveOccup | −$2,446 | Overcrowding lowers price |
| AveBedrms | −$1,613 | More bedrooms alone reduces value |
| Population | −$5,086 | Denser areas → lower price |
| Latitude | −$6,666 | Further north → lower price |

---

## 🔮 Custom Prediction

Use the `predict_price()` function in the script to estimate any house price:

```python
from house_price_prediction import predict_price

price = predict_price(
    MedInc=7.5,
    HouseAge=15,
    AveRooms=6.0,
    AveBedrms=1.0,
    Population=800,
    AveOccup=2.4,
    Latitude=37.8,
    Longitude=-122.4
)
print(f"Estimated Price: ${price:,.0f}")
```

Or load the saved model directly:

```python
import joblib
import numpy as np

model  = joblib.load("linear_regression_model.pkl")
scaler = joblib.load("standard_scaler.pkl")

features = np.array([[7.5, 15, 6.0, 1.0, 800, 2.4, 37.8, -122.4]])
price = model.predict(scaler.transform(features))[0]
print(f"Estimated Price: ${price:,.0f}")
```

---

## 📉 Output Plots

Running the script generates `house_price_prediction_plots.png` with three panels:

- **Predicted vs Actual** — scatter plot with perfect-fit diagonal
- **Residual Distribution** — histogram centered near zero (confirms low bias)
- **Feature Coefficients** — horizontal bar chart showing positive/negative drivers

---

## 🌐 Dashboard

Open `syntecxhub_house_price_prediction.html` in any browser for an interactive dashboard featuring:

- Live model metrics
- Predicted vs Actual scatter chart
- Residual histogram
- Feature coefficient bars
- Custom price predictor (adjust sliders and click Predict)

No server or installation needed — it runs entirely in the browser.

---

## 📌 Notes

- Model coefficients are on **scaled** features (StandardScaler applied)
- Predictions are clipped to `[$50,000 – $900,000]` to avoid out-of-range outputs
- The `random_state=42` seed ensures reproducible results every run

---

## 👤 Author

**SyntecxHub** · *Create · Think · Solve*  
Project 01 — House Price Prediction · Linear Regression
