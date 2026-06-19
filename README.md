# Advertising Sales Prediction — Multiple Linear Regression

A data analytics project that builds a multiple linear regression model to predict product sales from advertising spend across three channels: TV, Radio, and Social Media. The project covers the full analytical pipeline from exploratory data analysis through model evaluation, assumption diagnostics, and business interpretation.

---

## Dataset Description

**File:** `Advert.csv`  
**Rows:** 572 observations  
**Columns:** 5

| Column | Type | Description |
|---|---|---|
| TV | Categorical (Low / Medium / High) | TV advertising spend tier |
| Radio | Float | Radio advertising spend (continuous) |
| Social Media | Float | Social media advertising spend (continuous) |
| Influencer | Categorical | Influencer type used in campaign |
| Sales | Float | Product sales figures (target variable) |

**Note:** TV is a spend tier rather than a raw monetary figure. It was encoded ordinally (Low=1, Medium=2, High=3) for use in the regression model, since the categories represent a natural order of investment levels.

---

## Analysis Goals

This project answers three business questions:

1. **Which advertising channels have a statistically significant effect on Sales?**
2. **How well can the model predict Sales from these three channels combined?**
3. **Are there any channels where increasing spend does not produce a meaningful return?**

To answer these, the project follows this analytical sequence:

- Exploratory Data Analysis (EDA): shape, data types, missing values, distributions, and summary statistics
- Multicollinearity check: correlation matrix and Variance Inflation Factor (VIF) to ensure predictors are not redundant
- Multiple Linear Regression model using statsmodels OLS
- Model evaluation using Adjusted R-squared and individual predictor p-values
- Assumption diagnostics: Linearity, Normality, and Homoscedasticity checks via residual plots
- Coefficient interpretation and business recommendation

---

## Project Structure

```
advertising-sales-regression/
│
├── Advert.csv                         # Raw dataset
├── advertising_sales_regression.ipynb # Main Jupyter notebook (full analysis)
├── sales_regression_model.py          # Clean Python script version
├── diagnostic_plots.png               # Residual diagnostic plots
└── README.md                          # This file
```

---

## Environment Setup

This project runs in Python 3. Install the required libraries using pip:

```bash
pip install pandas seaborn statsmodels scipy matplotlib
```

If you are running in **Google Colab**, all libraries except statsmodels are pre-installed. Run this at the top of your notebook:

```python
!pip install statsmodels
```

Then upload your dataset:

```python
from google.colab import files
uploaded = files.upload()  # Select Advert.csv from your local machine
```

### Library versions used

| Library | Purpose |
|---|---|
| pandas | Data loading, cleaning, and manipulation |
| numpy | Numerical operations |
| matplotlib | Base plotting library |
| seaborn | Statistical visualizations (heatmap) |
| statsmodels | OLS regression model and VIF calculation |
| scipy | Shapiro-Wilk normality test |

---

## Key Findings

- The model explains **90.3% of the variance in Sales** (Adjusted R² = 0.903), indicating a strong fit.
- **TV spend tier** is the most powerful predictor: moving up one tier (e.g., Low to Medium) is associated with a **77.32-unit increase in Sales**, holding other channels constant.
- **Radio spend** is a statistically significant predictor: each one-unit increase in Radio spend is associated with a **2.98-unit increase in Sales**, holding other channels constant.
- **Social Media spend** is **not statistically significant** (p-value = 0.815), meaning the current data provides no reliable evidence that Social Media independently drives Sales once TV and Radio are accounted for.

---

## Business Recommendation

Prioritize TV and Radio budget allocation, as both channels show strong, statistically reliable relationships with Sales. Social Media spend shows no significant independent effect in this model, though this should be investigated further (e.g., checking whether social media spend is concentrated in a narrow range, or whether its effect is captured indirectly through TV and Radio activity) before budget decisions are made based on this finding alone.

---


