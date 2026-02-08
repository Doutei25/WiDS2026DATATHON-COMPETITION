# WiDS 2026 Datathon – Time-to-Event Risk Prediction

**Survival Analysis | Probabilistic Forecasting | Model Calibration**

## Overview

This repository contains the solution to the **WiDS Worldwide Datathon 2026**, where the goal was to predict the **probability of an event occurring within specific time horizons** rather than a single binary outcome.

Using survival analysis, the project estimates **calibrated probabilities** of events at **12h, 24h, 48h, and 72h**, enabling actionable, time-aware decision-making for emergency management and resource allocation.

**Final Public Leaderboard Score:** **0.90793**

---

## Problem Framing

Traditional classification ignores *when* an event will occur. This project reframes the challenge as a **time-to-event prediction problem**, which allows:

* Prioritization of high-risk events earlier
* Efficient allocation of emergency resources
* Interpretability of risk over time

---

## Methodology

### 1. Data Preparation

* Load and validate train and test datasets
* Handle missing values and confirm data types
* Ensure no target leakage from train to test

### 2. Feature Engineering

* Quantile-based outlier handling (1%-99%)
* Log transformations for skewed distributions
* Robust scaling for continuous variables
* Encode circular features (sine/cosine) and binary flags
* Preserve monotonicity in risk ranking

### 3. Baseline Survival Modeling

* Kaplan–Meier analysis for overall survival distribution
* Cox Proportional Hazards model for baseline hazard ratios
* Weibull Accelerated Failure Time (AFT) model for parametric baseline

### 4. Horizon-Based Probability Estimation

* Extract survival functions from CoxPH and Weibull AFT
* Convert survival curves to cumulative probabilities for horizons:

  * `prob_12h`
  * `prob_24h`
  * `prob_48h`
  * `prob_72h`
* Apply monotonicity enforcement

### 5. Advanced Models & Ensembling

* Evaluated non-linear and interaction models (Random Survival Forests)
* Weighted ensemble of CoxPH + Weibull AFT models
* Optimized weights based on **weighted Brier score**

### 6. Evaluation & Calibration

* Concordance Index (C-index) for rank accuracy
* Time-dependent Brier Score for horizon-specific accuracy
* Probability calibration using isotonic regression
* Operational validation to ensure actionable insights

---

## Repository Structure

```
WiDS2026DATATHON-COMPETITION/
├── data/                # Raw datasets (train.csv, test.csv)
├── notebooks/           # Step-by-step analysis notebooks
├── src/                 # Modular modeling code
├── submissions/         # Final CSV submissions
├── reports/             # Post-mortem and documentation
├── requirements.txt     # Python environment
└── README.md            # This file
```

---

## Results

| Metric           | Value                       |
| ---------------- | --------------------------- |
| Public Score     | 0.90793                     |
| Model Type       | Survival Analysis           |
| Prediction Type  | Multi-horizon probabilities |
| Interpretability | High                        |

---

## Tools & Libraries

* Python 3.12+
* pandas, numpy
* scikit-learn
* lifelines
* matplotlib, seaborn

---

## Key Learnings

* Survival analysis provides **superior insight** for time-sensitive problems
* **Probability calibration** is critical in competitive settings
* Submission validation ensures both accuracy and compliance
* Clear feature engineering improves **robustness and interpretability**

---

## Author

**Albert Better Ikiyoudoutei**
Data Scientist | Risk Modeling | Survival Analysis
GitHub: [https://github.com/Doutei25](https://github.com/Doutei25)

---

## Status

**Completed, validated, and competition-ready.**
