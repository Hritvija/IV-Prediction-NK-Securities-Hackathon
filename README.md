# Volatility Curve Prediction — NK Securities Hackathon 2025

### Predicting Implied Volatility for NIFTY50 Index Options

This repository contains my submission for the **NK Securities Research Hackathon 2025**, focused on **Volatility Curve Prediction** — a quantitative modeling challenge that required developing a model to reconstruct missing implied volatilities from high-frequency NIFTY50 index option data.

---

## Overview

Implied volatility (IV) reflects the market’s expectation of future movement and plays a critical role in **option pricing** and **risk management**.  
In this competition, the goal was to:

> **Predict missing implied volatilities across strike–maturity combinations** using anonymized, per-second trading data from real markets.

The task involved understanding the *volatility smile* — the characteristic non-linear relationship between strike price and implied volatility — and building a robust model that could accurately reconstruct this curve.

---

## Approach

The solution combines **parametric modeling** (SVI) with **machine learning (LightGBM)** to capture both the structural and statistical properties of volatility surfaces.

### Data Understanding & Preprocessing
- Parsed anonymized per-second trading data for NIFTY50 options.
- Cleaned and normalized inputs (strike, moneyness, expiry, IVs).
- Created engineered features such as:
  - Moneyness = `strike / underlying_price`
  - Time to maturity
  - Cross-sectional features (ATM spread, skewness indicators).

### Volatility Surface Modeling (SVI)
Implemented the **Stochastic Volatility Inspired (SVI)** parametrization:
\[
\sigma(k) = a + b \left[ \rho (k - m) + \sqrt{(k - m)^2 + \sigma^2} \right]
\]
- Calibrated parameters *(a, b, ρ, m, σ)* for each maturity slice.
- Used curve-fitting optimization to extract interpretable smile shapes.

### Machine Learning Enhancement (LightGBM)
- Trained a **LightGBM Regressor** to learn residuals and correct systematic deviations from the parametric model.
- Input features included:
  - SVI parameters
  - Strike, expiry, moneyness, and underlying price signals
- Output target: Predicted implied volatility

### Model Evaluation
- Evaluation Metric: **Mean Squared Error (MSE)**
- Achieved stable generalization across validation folds
- Optimized inference pipeline for efficiency and interpretability

---

## Tech Stack

| Category | Tools Used |
|-----------|-------------|
| Programming | Python 3 |
| Modeling | LightGBM, SciPy, NumPy, Pandas |
| Visualization | Matplotlib, Seaborn |
| Optimization | Least Squares Curve Fitting, Cross-validation |
| Core Theory | Black-Scholes Model, SVI Parameterization |

---

## Results

- **Leaderboard Rank:** 200 (out of 735 teams)  
- **Improvement:** +17 rank positions  
- **Evaluation Metric (MSE):** 0.000156825  
- **Competition Timeline:** May 31 – June 8, 2025  
- **Host:** NK Securities Research  

---

## Key Insights

- The **SVI + LightGBM hybrid approach** effectively balances *financial interpretability* with *data-driven flexibility*.
- SVI captures smile curvature efficiently, while LightGBM learns complex residual patterns not modeled parametrically.
- Future improvements could include:
  - Incorporating **temporal volatility clustering** via recurrent architectures.
  - Testing **neural spline flows** for non-parametric smile fitting.

---

## Acknowledgements

- Hosted by **NK Securities Research**
- Dataset: High-frequency NIFTY50 options market data
- Evaluation Metric: Mean Squared Error (MSE)
- Duration: **May 31 – June 8, 2025**

---

## Author

**Hritvija Singh (Team: Solo Submission)**  
Ranked **200 / 735 Teams** in the *NK Securities Hackathon 2025*  
📈 Focus: Quantitative Modeling | Machine Learning | Financial Analytics  
