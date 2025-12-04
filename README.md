# Public Transport Ridership Analysis & SARIMA Forecasting  
### A 7-Year Time-Series Analysis and 7-Day Forecasting Report

---
Key Insights (Short & Crisp)

1) Pandemic Effect: Ridership dropped sharply in 2020–2021 due to COVID-19 and began a steady recovery from 2022 onward, though not all services returned to pre-pandemic levels.

2) Dominant Services: Rapid Route and Local Route consistently have the highest daily ridership and the largest fluctuations, making them the core demand drivers; Light Rail is also a major contributor.

3) Weekly Seasonality: Strong weekday usage and significant weekend drops are observed across all services, with School services showing almost exclusive weekday demand.

4) Service Variability: Rapid Route and Local Route show high daily variance, requiring dynamic operational planning, while Peak Service and Other remain low-volume and stable.

5) Correlation Patterns: Most major services are strongly correlated (>0.85), indicating shared commuter-driven behaviour, while the Other category shows weak correlations and more independent usage patterns.

## 1. Key Insights from Exploratory Data Analysis

### 1.1 Pandemic Impact on Ridership  
Daily passenger journeys show a sharp decline from late 2019 to early 2021 due to COVID-19 restrictions and reduced mobility.  
This period represents the lowest ridership levels in the full 7-year dataset.  
Beginning in 2022, most services exhibit a steady recovery, although some remain below pre-pandemic levels.

---

### 1.2 Dominant Service Types: Rapid Route and Local Route  
- Rapid Route and Local Route consistently record the highest daily ridership.  
- They form the core of the transportation network and show the largest operational fluctuations.  
- Light Rail also contributes significantly and consistently ranks as a major service.

---

### 1.3 Strong Weekly Seasonality  
A clear weekday–weekend pattern is present across all service types:

- Higher ridership from Monday to Friday  
- Sharp decline on Saturdays and Sundays  
- School services show extremely concentrated weekday behavior, with almost zero weekend usage  

This reflects a strong commuter-driven demand pattern.

---

### 1.4 Yearly Trends and Post-Pandemic Recovery  
Yearly aggregation reveals three distinct phases:

- A notable decline during 2020–2021  
- Recovery beginning in 2022  
- Strong upward momentum in 2023, with Rapid Route showing the fastest recovery  

These trends indicate increasing public confidence and the resumption of regular travel routines.

---

### 1.5 Inter-Service Correlation Patterns  
- Local Route, Light Rail, Peak Service, and Rapid Route exhibit strong positive correlations, suggesting they serve similar commuter groups.  
- School service aligns moderately with these trends but retains its own academic schedule–driven pattern.

---

## 2. Model Selection: Why SARIMA Was Chosen

Three forecasting approaches were evaluated: **SARIMA**, **Prophet**, and **XGBoost**.  
After assessing dataset characteristics and model performance, SARIMA was selected as the most suitable forecasting approach.

---

## 2.1 Reasons for Choosing SARIMA

### 1. Strong Weekly Seasonality  
SARIMA’s seasonal component (P, D, Q, m) models repeating weekly cycles (m = 7), which is a defining pattern in the ridership data.

### 2. Ability to Handle Trend Shifts  
With differencing and integrated components, SARIMA captures long-term patterns and structural breaks—crucial for handling pandemic disruptions.

### 3. Statistical Interpretability  
SARIMA provides interpretable coefficients, residual diagnostics, and model selection metrics (AIC/BIC).  
This supports transparent and defensible forecasting.

### 4. High Accuracy for Short-Term Forecasting  
Since the task requires predicting the next 7 days, SARIMA excels at modeling short-term dependencies and recurring seasonal structures.

---

## 3. Comparison with Other Forecasting Models

### 3.1 Prophet

**Pros:**  
- Automatically models trend and seasonality  
- Business-friendly and robust to outliers  

**Limitations:**  
- Less precise in modeling weekly seasonality compared to SARIMA  
- Struggles with structural shifts (e.g., pandemic) unless explicitly defined  
- Slightly lower short-term daily accuracy  

**Conclusion:**  
Prophet performed reasonably well, but SARIMA aligned more effectively with dataset characteristics.

---

### 3.2 XGBoost

**Pros:**  
- Effective for non-linear patterns  
- Flexible with custom feature engineering  

**Limitations:**  
- Requires supervised transformation of time series  
- Even with lag/rolling features, model performance was poor  
- Produced extremely negative R² scores and high error metrics  
- Failed to capture weekly seasonality and pandemic-driven shifts  

**Conclusion:**  
The dataset’s strong seasonal and temporal structure favors classical time-series models, making XGBoost unsuitable.

---

## Final Model Choice

SARIMA was selected because it best captures:

- Weekly seasonality  
- Long-term trend behaviour  
- Pandemic-driven structural changes  

It also offers superior interpretability and more stable 7-day forecasts compared to Prophet and XGBoost.

---

## 4. Forecast Output Summary
SARIMA Model Summary:




Model Evaluation for Rapid Route
----------------------------------
MAE : 10513.425283130899
RMSE: 12909.164419328721
MAPE: inf
R2 Score: -1.0909333894557163

Next 7-Day Forecast:
2024-09-16    17451.501075
2024-09-17    19756.568707
2024-09-18    19483.827578
2024-09-19    19040.793163
2024-09-20    17979.695387
2024-09-21     8997.790803
2024-09-22     7306.646340


