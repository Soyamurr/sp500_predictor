# S&P 500 Market Prediction

A machine learning project that predicts whether the S&P 500 index will go up or down the next trading day, using a Random Forest classifier and historical price data.

---

## Overview

This project uses historical S&P 500 data going back to 1990 to train a binary classifier. The model predicts whether tomorrow's closing price will be higher than today's — outputting `1` (up) or `0` (down).

The project also implements a backtesting system to simulate how the model would have performed over time, and uses rolling average features to improve prediction accuracy.

---

## Stack

| Tool | Purpose |
|---|---|
| Python 3.8+ | Core language |
| yfinance | Download S&P 500 historical data |
| pandas | Data manipulation |
| scikit-learn | Random Forest model & evaluation |
| matplotlib | Visualizing predictions |

---

## how to run
### BEFORE RUNNING YOU NEED TO HAVE VS Code Jupyter Extension, Python 3.8+

### 1. clone or create the project folder
```bash
mkdir sp500_predictor
cd sp500_predictor
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install yfinance scikit-learn matplotlib pandas
```

### 4. Open in VS Code
```bash
code .
```

Open `market_prediction.ipynb` and run cells top to bottom.

---

## how it works

### Data
- Downloaded directly from Yahoo Finance via `yfinance` (no CSV needed)
- Covers S&P 500 daily prices from 1990 to present
- Features used: `Open`, `High`, `Low`, `Close`, `Volume`

### Target
- `1` → Tomorrow's close is higher than today's
- `0` → Tomorrow's close is lower than today's

### Features (Rolling Averages)
To improve the model, rolling ratio and trend features are engineered over multiple time horizons:

| Horizon | Meaning |
|---|---|
| 2 days | Very short-term momentum |
| 5 days | Weekly trend |
| 60 days | Quarterly trend |
| 250 days | Annual trend |
| 1000 days | Multi-year trend |

### Model
- Random Forest Classifier (`n_estimators=200`, `min_samples_split=50`)
- Prediction threshold set to 0.6 (only predicts "up" when confidence ≥ 60%)
- Evaluated using precision score

### Backtesting
A custom backtesting function simulates real-world usage by training only on past data and predicting forward in steps of 250 trading days (~1 year).

---

## Results

The model is evaluated using precision score — measuring how often the "up" predictions were actually correct. A score above 0.55 meaningfully outperforms random guessing in market prediction.

---

## based on

Based on the Dataquest project walkthrough by [Dataquest](https://www.youtube.com/c/Dataquestio).
