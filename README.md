# STAT670---EDA---Delhi-Air-Pollution

# Delhi Air Pollution Analysis

> **Note on repository history:** This project was originally hosted on Indiana University's GitHub Enterprise repository. Because that repository could not be accessed publicly, the project has been copied here to my personal GitHub repository so it can be viewed and shared openly.

A statistical analysis of fine particulate matter (PM2.5) in Delhi, India, completed as the final project for **STAT-670**. The project explores what drives PM2.5 concentrations across six monitoring stations and builds a multiple linear regression model to predict daily pollution levels.

**Author:** Yashkumar Burnwal

---

## Overview

PM2.5 is the fine particulate matter that poses the greatest health risk in air quality monitoring. Using hourly readings from six stations across Delhi (June 2018 – October 2019), this analysis:

- Cleans and structures roughly 70,000 hourly observations across 21 variables
- Explores temporal patterns in PM2.5 (daily cycles, day-of-week effects, seasonal trends)
- Identifies the pollutants and meteorological factors most strongly associated with PM2.5
- Fits and evaluates a predictive regression model on a held-out test period

The full analysis is written in R Markdown, so all code, output, and figures are reproducible from a single source file.

---

## Repository Contents

| File | Description |
|------|-------------|
| `Delhi_AirPollution_Analysis.Rmd` | The R Markdown source — all code and narrative |
| `Delhi_AirPollution_Analysis.html` | The rendered report (open in a browser to view) |
| `Delhi_6Station_Hourly.csv` | The dataset: hourly readings from six Delhi stations |
| `README.md` | This file |

---

## The Data

- **Source:** Hourly air quality and meteorological readings from six monitoring stations in Delhi
- **Period:** June 1, 2018 – October 1, 2019
- **Size:** ~70,227 rows × 21 columns
- **Response variable:** `PM2.5` (μg/m³)

**Variable groups:**

- **Pollutants:** PM2.5, PM10, NO, NO2, NOx, SO2, Ozone, CO, Benzene, NH3
- **Meteorology:** Air temperature (AT), barometric pressure (BP), solar radiation (SR), relative humidity (RH), wind speed (WS), wind direction (WD)
- **Time/location:** year, month, day, hour, station (`loc`)

The dataset was clean on inspection — no missing PM2.5 values and only a single extreme outlier.

---

## Analysis Structure

The report is organized into five sections:

1. **Load and Inspect the Data** — Read the CSV, examine structure and summary statistics, classify variables.
2. **Construct Datetime and Clean Data** — Build a proper timestamp from the date components, derive features (hour of day, day of week, weekend flag), and run missing-value and outlier checks.
3. **Explore PM2.5 Over Time** — Distribution analysis, full time series, diurnal cycle, day-of-week patterns, and monthly/seasonal trends.
4. **Explore Relationships with Other Variables** — Correlation matrix, ranked predictors, scatterplots, and trivariate visualizations (e.g., PM2.5 vs NO2 by hour, PM2.5 vs humidity by season).
5. **Training/Testing Split and Modeling** — Time-based train/test split, aggregation to daily means, multiple linear regression, diagnostics, and test-set evaluation.

---

## Key Findings

- **Right-skewed distribution:** Mean PM2.5 is ~93 μg/m³ but the median is only 58 — most days are moderate, with a long tail of severe winter pollution episodes. Delhi sits well above the WHO 24-hour guideline of 35 μg/m³ for most of the year.
- **Daily cycle:** PM2.5 peaks late at night (~10 PM) and is lowest in the afternoon (~4 PM), driven by atmospheric mixing.
- **Weak weekend effect:** The weekday–weekend difference is modest, reflecting that Delhi's pollution comes from many sources rather than commuter traffic alone.
- **Top predictors:** PM10 (r ≈ 0.79) is the strongest correlate, followed by Benzene, CO, and NH3. Temperature is strongly *negatively* correlated — colder days mean worse air.
- **Model performance:** A multiple linear regression on daily means explains **~93% of the variance** (R² = 0.927). On the held-out test period, test RMSE (~13.4 μg/m³) was lower than training RMSE, indicating the model generalizes well without overfitting.

---

## Reproducing the Analysis

**Requirements:** R (4.x recommended) and RStudio.

Install the required packages:

```r
install.packages(c(
  "tidyverse", "lubridate", "corrplot", "viridis", "scales",
  "gridExtra", "knitr", "kableExtra", "reshape2", "broom"
))
```

Then knit the report:

1. Open `Delhi_AirPollution_Analysis.Rmd` in RStudio.
2. Make sure `Delhi_6Station_Hourly.csv` is in the same directory.
3. Click **Knit** to regenerate the HTML report.

Alternatively, open `Delhi_AirPollution_Analysis.html` directly in any web browser to view the rendered analysis without running any code.
