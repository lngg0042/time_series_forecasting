# ETW3420 Time Series Forecasting


## Projects

| # | Project | Data | Key Methods |
|---|---|---|---|
| 1 | [Forecasting Fundamentals](#1-forecasting-fundamentals) | Drug sales, beer production, Google stock, electricity | Seasonal plots, benchmark methods, residual diagnostics, Box-Cox |
| 2 | [U.S. Transportation Energy After COVID-19](#2-us-transportation-energy-after-covid-19-group-project) *(group)* | U.S. EIA monthly energy data, 2010–2025 | ARIMA, ETS, stationarity tests, time series cross-validation |
| 3 | [Forecasting Global Gold Demand](#3-forecasting-global-gold-demand) | Quarterly gold demand and economic indicators, 2010–2025 | Regression with ARIMA errors, ensembles, bagging |

---

## 1. Forecasting Fundamentals

An introduction to the core forecasting workflow, using four classic datasets.

- **Seasonality:** found a strong January peak in Australian antidiabetic drug sales, linked to people stocking up before the yearly reset of the government's Pharmaceutical Benefits Scheme (PBS) Safety Net.
- **Benchmark forecasting:** compared the Mean, Naïve and Seasonal Naïve methods on Australian beer production. **Seasonal Naïve** was clearly best (MAPE 3.2% vs 8.3% and 14.2%).
- **Residual diagnostics:** used the ACF and a Ljung-Box test (p = 0.36) to confirm that a Naïve model's residuals on Google stock prices behave like white noise.
- **Transformations:** applied a Box-Cox transformation (λ ≈ 0.27) to steady the growing swings in Australian electricity production.

📄 [`A1-ETW3420.pdf`](A1-ETW3420.pdf)

---

## 2. U.S. Transportation Energy After COVID-19 *(Group Project)*

How did COVID-19 disrupt U.S. transportation energy use, and has it recovered?

We analysed **five U.S. Energy Information Administration (EIA) energy series** for the transportation sector. Models were trained on **pre-COVID data (2010 to Feb 2020)** and tested on the pandemic and recovery period, to see how well forecasting models cope with a major shock.

**Workflow:** data cleaning, then exploration (STL decomposition, seasonal and ACF plots), then stationarity checks (KPSS and ADF tests, differencing), then pure AR and MA models, then Auto ETS and Auto ARIMA. Finally we picked the best ("champion") model for each dataset using test accuracy and time series cross-validation, and forecast 2026–2027.

**Findings:**
- Transport energy use **fell about 37% in early 2020**, and recovery has been **incomplete**. Most series are still below pre-pandemic levels.
- **ETS** worked best for smoother seasonal series. **ARIMA-based** models worked better for more volatile series.
- All models lost accuracy during the COVID period, which shows the limits of historical models when a sudden structural break happens.

📄 [`Group_Project_Report.pdf`](Group_Project_Report.pdf)

---

## 3. Forecasting Global Gold Demand

Can economic indicators explain gold demand, and which approach forecasts it best?

Using quarterly data from 2010 to 2025, this project compares **causal** and **purely predictive** forecasting.

- **Causal model:** regression with ARIMA(1,0,0)(0,0,2)[4] errors, using gold price, inflation, interest rates and the USD index as predictors. Gold price, inflation and interest rates were significant. The model beat plain regression (AIC 807 vs 820), and its residuals passed the white noise checks.
- **Ensemble:** averaged Seasonal Naïve, ETS, ARIMA and STL forecasts.
- **Bagging:** bagged ETS fitted to 20 moving block bootstrap samples.
- **Evaluation:** holdout test set plus rolling time series cross-validation up to 12 quarters ahead.

**Findings:**
- **Bagged ETS** was the most accurate (CV RMSE 242), just ahead of the ensemble (248).
- The **causal model** was the easiest to interpret but the least accurate (CV RMSE 329), and its errors grew quickly at longer horizons. This shows a trade-off between **explaining** demand and **predicting** it.
- No model predicted the record **Q2 2025 spike** (about 2,084 tonnes).

📄 [`ETW3420_A3.pdf`](ETW3420_A3.pdf)

---

## Tools
**R**, using `forecast`, `fpp2`, `ggplot2`, `zoo`, `tidyr` and `knitr`.

## Academic Integrity
These projects are shared for portfolio and learning purposes. If you are currently taking ETW3420, please don't copy this work. Follow [Monash University's academic integrity policy](https://www.monash.edu/student-academic-success/maintaining-integrity).
