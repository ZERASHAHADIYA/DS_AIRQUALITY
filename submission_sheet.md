# Air Quality Insight - Submission Sheet

## Round 1 - Data Understanding, Preparation & EDA

**Problem statement:** Analyze how measured pollutants, weather, and time relate to air quality. Identify periods with higher AQI and provide evidence-based monitoring recommendations.

**Dataset details:** UCI Machine Learning Repository Air Quality dataset, with the AQI label from the provided prepared file. The analyzed dataset contains **8,991 hourly records and 25 attributes**, including timestamp, sensor measurements, AQI, and engineered features; coverage is 10 March 2004 to 4 April 2005.

**Data preprocessing:** Restored timestamps after validating sensor-row alignment; decoded `-200` sensor sentinels as missing values. Removed 366 rows with missing instrument readings and found 0 duplicate timestamps. Remaining missing readings were retained in the dataset and median-imputed within the training pipeline only. IQR extremes were flagged for review, not automatically removed, to preserve possible pollution peaks.

**EDA findings:**
- Mean AQI peaked at **19:00 (164.31)** and was lowest at **05:00 (83.45)**.
- **Winter** had the highest seasonal mean AQI (**155.37**); **summer** had the lowest (**115.05**).

## Round 2 - Feature Engineering & Machine Learning

**Selected features:** Pollutant and sensor readings (`CO`, `NMHC`, `C6H6`, `NOx`, `NO2`, and PT08 sensors), temperature, relative/absolute humidity, and engineered hour, weekday, month, weekend, season, cyclical-hour, and temperature-humidity interaction features. **Target:** AQI.

**Algorithm and justification:** Random Forest Regressor. It can model nonlinear relationships and interactions in sensor data without requiring feature scaling; missing numeric inputs and the seasonal category are handled in a training pipeline.

**Model performance:** Chronological 80/20 split; **1,799 test rows**. MAE **0.4844**, RMSE **2.8547**, R² **0.9969**. MAE baseline (training-set mean) **49.1510**. This is same-period AQI-label estimation, not a future forecast; the AQI label formula is undocumented.

## Round 3 - Intelligence Layer, Visualization & Prototype

**Visualizations:** Mean AQI by hour (line chart); mean AQI by season (bar chart); pollutant/AQI correlation chart; Excel summary charts and native PivotTables/PivotCharts by hour, season, and weekday.

**Key insights:**
- AQI rose during the evening, reaching its hourly mean peak at 19:00.
- Winter AQI averaged about **40.32 points higher** than summer in this dataset.

**Prototype / intelligence layer:** Executable EDA notebook, Excel analysis workbook with formulas and PivotCharts, and an AQI-estimation model evaluated on a chronological holdout; the findings are summarized in a five-slide business pitch.

**Recommendations:**
- Prioritize enhanced monitoring around evening hours, especially near 19:00, and during winter; confirm with current measurements.
- Collect station identifiers, PM2.5, wind, traffic, rainfall, and holiday data before ranking locations or attributing causes.

## Final Submission

**GitHub repository:** https://github.com/ZERASHAHADIYA/DS_AIRQUALITY

**Overall result / conclusion:** The analysis identifies clear hourly and seasonal AQI patterns, and the Random Forest closely estimates the provided AQI label on a chronological holdout. Results are limited to one historical monitoring site; the available data cannot answer the requested station, PM2.5, wind, traffic, or rain comparisons.