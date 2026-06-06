Stochastic Interest Rate Modelling and Yield Curve Reconstruction using CIR & CIR++

Project Overview

This project implements the Cox-Ingersoll-Ross (CIR) short-rate model and its deterministic-shift extension CIR++ for zero-coupon yield curve reconstruction and prediction.

The objective is to use the 3-Month Zero-Coupon Yield as a proxy for the instantaneous short rate and reconstruct the complete yield curve across multiple maturities ranging from 3 Months to 30 Years.

The project includes:

* Exploratory Data Analysis (EDA)
* Missing value audit
* Outlier detection and treatment
* Time-series analysis
* CIR model calibration
* CIR++ extension
* In-sample model evaluation
* Train/Validation testing
* Out-of-sample yield curve prediction
* Export of predicted yield curves

⸻

Dataset Description

Training Dataset

Contains daily zero-coupon yields for the following maturities:

Tenor	Column
3M	ZC025YR
6M	ZC050YR
9M	ZC075YR
1Y	ZC100YR
2Y	ZC200YR
5Y	ZC500YR
10Y	ZC1000YR
20Y	ZC2000YR
30Y	ZC3000YR

Period Covered:

2016 – 2024

Test Dataset

Contains observed yields for:

* 3M
* 6M
* 9M
* 1Y
* 2Y

Test 3M Dataset

Contains only:

* 3-Month Yield

This acts as the model input for reconstructing the entire yield curve.

⸻

Project Workflow

1. Exploratory Data Analysis

Performed:

* Missing value audit
* Descriptive statistics
* Yield distribution analysis
* Correlation analysis
* Yield curve snapshots
* Time-series visualization

2. Outlier Detection

Three approaches were used:

Method A: IQR Rule

Observations outside:

Q1 − 3×IQR

Q3 + 3×IQR

were flagged.

Method B: Z-Score Analysis

Observations with:

|Z| > 3.5

were examined.

Method C: Percentage Change Spikes

Large day-to-day changes were identified.

⸻

3. Data Cleaning

The following preprocessing steps were applied:

* Missing value imputation
* Winsorization (0.5% – 99.5%)
* Correction of identified anomalies
* Positivity enforcement for interest rates
* Validation checks

⸻

4. Time-Series Analysis

Studied:

* Lag-1 autocorrelation
* Yield curve inversions
* Term spread behaviour
* Correlation structure between maturities

⸻

5. CIR Model Calibration

The CIR short-rate process is:

dr(t) = κ(θ − r(t))dt + σ√r(t)dW(t)

where:

* κ = Mean reversion speed
* θ = Long-run mean rate
* σ = Volatility parameter

Model parameters are estimated using the training dataset.

⸻

6. Yield Curve Reconstruction

The 3-Month yield is treated as a proxy for the instantaneous short rate.

For each observation:

* Input: 3M yield
* Output: Full yield curve (3M → 30Y)

using the calibrated CIR model.

⸻

7. CIR++ Extension

To improve curve fitting, a deterministic shift function is introduced:

r(t) = x(t) + φ(t)

where:

* x(t) follows the CIR process
* φ(t) is a deterministic shift calibrated from observed market yields

This allows the model to better match the market term structure.

⸻

8. Model Evaluation

Performance is measured using:

R² Score

Measures proportion of variance explained.

R² = 1 indicates perfect fit.

RMSE

Root Mean Squared Error measured in basis points (bps).

Lower RMSE indicates better predictions.

Bias

Average prediction error.

⸻

9. Train / Validation Testing

An 80/20 chronological split is used:

* 80% Training
* 20% Validation

This evaluates model generalization on unseen periods.

⸻

10. Out-of-Sample Prediction

Using only the 3M yield from test_data_3M.csv:

* CIR predicts the full yield curve.
* CIR++ predicts the full yield curve.

Predictions are generated for:

* 3M
* 6M
* 9M
* 1Y
* 2Y
* 5Y
* 10Y
* 20Y
* 30Y

⸻

Key Findings

* Yield series exhibit extremely high persistence.
* Strong positive correlations exist across all maturities.
* The COVID period introduced significant market shocks.
* CIR performs well for short maturities.
* CIR++ improves the fit to observed yield curves through deterministic shifts.
* Long-maturity yields are more difficult to model using a single-factor short-rate framework.

⸻

Output

The final output file contains CIR++ predicted yields for all maturities:

cir_predictions_test.csv

Columns:

* Date
* pred_CIRpp_3M
* pred_CIRpp_6M
* pred_CIRpp_9M
* pred_CIRpp_1Y
* pred_CIRpp_2Y
* pred_CIRpp_5Y
* pred_CIRpp_10Y
* pred_CIRpp_20Y
* pred_CIRpp_30Y

⸻

Technologies Used

* Python
* NumPy
* Pandas
* SciPy
* Matplotlib
* Seaborn
* Scikit-Learn

⸻

References

1. Cox, Ingersoll and Ross (1985), “A Theory of the Term Structure of Interest Rates”.
2. Brigo & Mercurio (2001), “A Deterministic-Shift Extension of Analytically Tractable Short-Rate Models”.
3. Hull, J. C. – Options, Futures and Other Derivatives.
