# Forecasting water treatment membrane's performance degradation with LSTM and time-series data.

## Overview
This project implements a **hybrid approach** for predicting membrane performance degradation and estimating **Remaining Useful Life (RUL)**. It combines **Deep Learning (LSTM)** for short-term trend learning with **Physics-based Curve Fitting (Power Law)** for long-term extrapolation.

## Key Features

### 1. Data Preprocessing Pipeline
- **Loading & Cleaning:** Automated loading of sensor CSVs, column renaming, and outlier removal using **IQR**.
- **Resampling:** Standardizes data to **30-second intervals** with interpolation for minor gaps.
- **Rejection Calculation:** Computes membrane rejection rates based on temperature-corrected conductivity.

### 2. Intelligent Cycle Segmentation
- Automatically detects **operational cycles** based on time gaps and performance jumps.
- Removes unstable "stabilization" periods at the start of each cycle to ensure clean training data.

### 3. Deep Learning Model (LSTM)
- Uses a **Long Short-Term Memory (LSTM)** network to learn temporal degradation patterns from historical cycles.
- Features include `Time_in_Cycle` and `Total_Cumulative_Hours` to capture aging effects.

### 4. Hybrid Forecasting & RUL Estimation
- **Multi-step Forecasting:** Uses the trained LSTM to predict future rejection trends.
- **Physics-based Extrapolation:** Fits a Power Law model to the LSTM predictions:

  $$y = a - b \cdot t^c$$

- **Uncertainty Quantification:** Generates **95% Confidence Intervals (CI)** for the failure prediction.
- **RUL Calculation:** Estimates the exact time until the rejection rate drops below a critical threshold (e.g., **99.0%**).

## Dependencies

This project requires **Python 3.x** and the following libraries:

- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`, `scipy`
- `torch` (PyTorch)

You can install the dependencies using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy torch
