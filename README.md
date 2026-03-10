# Causal Impact of Temperature on Walmart Weekly Sales

## Project Overview

This project investigates whether changes in temperature have a **causal impact on Walmart's weekly sales**. The analysis uses panel data from **45 Walmart stores between February 2010 and October 2012** to examine how temperature variations influence consumer purchasing behavior.

The goal is to determine whether temperature affects sales directly or whether observed correlations are driven by seasonal patterns or other confounding factors.

---

## Research Question

Does temperature have a **causal effect** on Walmart's weekly sales?

Key considerations:

- Sales and temperature both vary seasonally
- Store characteristics differ across locations
- Macroeconomic factors may influence purchasing behavior

To address these issues, the analysis applies **panel data econometric methods with fixed effects**.

---

## Dataset

The dataset contains **6,435 weekly observations** across **45 Walmart stores**.

| Variable | Description |
|--------|-------------|
| Store | Store identifier |
| Date | Week of observation |
| Weekly_Sales | Total weekly store sales |
| Temperature | Average weekly temperature |
| Fuel_Price | Fuel price during the week |
| CPI | Consumer Price Index |
| Unemployment | Regional unemployment rate |
| Holiday_Flag | Indicator for holiday weeks |

---
log_sales = log(Weekly_Sales)
## Data Preparation

Key preprocessing steps included:

- Converting date fields to proper date format
- Creating year and month features
- Log-transforming sales to stabilize variance

Weekly sales were **right-skewed**, so using the logarithm allows coefficients to be interpreted as **percentage changes in sales**.

The dataset was also verified to be a **balanced panel**, meaning each store has observations across the same time period.

---

## Exploratory Data Analysis

Exploratory analysis revealed:

- Strong **seasonality patterns** in both temperature and sales
- Potential **spurious correlations** due to time trends
- Evidence of a **nonlinear relationship** between temperature and sales

A LOESS smoothing curve suggested an **inverted U-shaped relationship**, motivating the inclusion of a quadratic temperature term in the regression model. :contentReference[oaicite:2]{index=2}

---

## Causal Framework

A causal diagram was used to identify potential **confounding paths**.

Main backdoor paths:
Temperature ← Location → Sales
Temperature ← Date → Sales


To block these confounders:

- **Store Fixed Effects** control for time-invariant store characteristics such as location, size, and customer demographics.
- **Date Fixed Effects** control for seasonal and macroeconomic shocks.

This identification strategy isolates the effect of **within-store temperature variation over time**. :contentReference

---

## Econometric Model

The primary model estimated is a panel fixed effects regression**:


Controls included:

- Fuel Price
- CPI
- Unemployment

Standard errors are **clustered at the store level** to account for serial correlation.

---

## Results

### Model 1: Full Model with Controls

Key findings:

| Variable | Effect |
|------|------|
| Temperature | Positive and statistically significant |
| Temperature² | Negative and significant |
| Unemployment | Negative effect on sales |
| Fuel Price | Small negative effect |
| CPI | Not statistically significant |

The results indicate a **nonlinear relationship** between temperature and sales.

A 1°F increase in temperature increases weekly sales by approximately 0.5%**, holding other factors constant.

However, the negative quadratic term suggests **diminishing returns**.

Sales peak at approximately:
76°F


Beyond this temperature, further increases in heat begin to **reduce sales**.

---

### Model 2: Robustness Check

A second model excludes macroeconomic controls.

Findings remain consistent:

- Temperature coefficient remains stable
- Quadratic term remains negative
- Turning point shifts slightly to ~84°F

This suggests the **temperature effect is not driven by macroeconomic variables**.

---

## Key Insights

The analysis reveals three important findings:

1. **Temperature has a causal impact on sales**, after controlling for seasonal patterns and store characteristics.
2. The relationship is **nonlinear**.
3. **Moderate temperatures increase sales**, but extreme heat reduces consumer activity.

---

## Business Implications

These findings can inform retail planning strategies:

- Inventory planning based on temperature forecasts
- Seasonal marketing campaigns
- Staffing adjustments during warmer periods

Moderate warming may **increase demand**, while extreme heat could reduce store traffic.

---

## Tools Used

- R
- tidyverse
- fixest
- ggplot2
- Panel data econometrics

## Author
Yasmeen Karachiwala  
MS Business Analytics  
Seattle University

