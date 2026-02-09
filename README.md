#  Customer Personality Analysis: Determinants of Spending Behavior

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![Model](https://img.shields.io/badge/Model-LASSO%20%2F%20Ridge-green) ![Status](https://img.shields.io/badge/Status-Completed-success)

##  Project Overview
Understanding customer personality is crucial for tailoring marketing strategies and product offerings. This project investigates **how customer demographics (e.g., income, family structure) and seller strategies (promotions) influence spending behaviors** across different product categories (Wine, Meat, and Sweets).

Using a dataset from **iFood** (a leading food delivery platform), we applied econometric models to quantify these relationships and identify ideal customer profiles.

##  Research Questions
1. **Heterogeneity:** How do different consumer characteristics (e.g., education, marital status) affect spending on specific goods?
2. **Elasticity:** To what extent do marketing promotions drive actual sales?
3. **Model Robustness:** Does variable selection (LASSO) improve prediction accuracy compared to full models?

##  Data Source
* **Dataset:** `marketing_campaign` (Source: iFood / GitHub)
* **Sample Size:** 2,240 customers.
* **Key Features:**
    * **Demographics:** Income, Education, Marital Status, Kidhome/Teenhome.
    * **Behavioral:** Recency, Complain, Web/Store Visits.
    * **Promotional:** Responses to 5 marketing campaigns.
* **Target Variables:** Spending amounts on Wine, Meat, and Sweets.

##  Methodology

### 1. Data Preprocessing
* **Imputation:** Missing `Income` values were imputed using group averages based on Education and Marital Status.
* **Feature Engineering:**
    * Converted categorical variables (`Education`, `Marital_Status`) into dummy variables.
    * Aggregated marketing campaign responses into a single engagement metric.
    * Log-transformation applied to skewed data.
* **Outlier Removal:** Excluded extreme values to ensure model stability.

### 2. Modeling Strategy
We focused on **Regularized Regression** to handle multicollinearity and perform feature selection:
* **LASSO Regression (Primary):** Used for automatic variable selection (shrinking coefficients of irrelevant features to zero).
* **Ridge Regression (Robustness Check):** Used to handle multicollinearity and validate LASSO results.
* **White Test:** Conducted to detect heteroscedasticity in the residuals.

##  Key Findings

| Product Category | Model $R^2$ | Key Drivers (Positive) | Key Inhibitors (Negative) |
| :--- | :--- | :--- | :--- |
| **Wine** | **66.8%** | Income, PhD Education, Store Purchases | **Kids at home**, Low Education (2nd Cycle) |
| **Meat** | **60.4%** | Income, Catalog Purchases | **Teens at home** (Surprising insight), Web Visits |
| **Sweets** | **39.4%** | Web Purchases, Catalog Purchases | PhD Education, Teens at home |

###  Business Insights
1.  **The "Kid" Effect:** Households with small children significantly reduce alcohol consumption, while households with teenagers surprisingly spend *less* on meat (contrary to the "growing teen appetite" hypothesis).
2.  **Channel Preference:** Wine buyers prefer **in-store** experiences, while meat buyers respond better to **catalogs**.
3.  **Marketing Efficiency:** Simply accepting a campaign offer (`Response`) does not strictly correlate with higher spending across all categories, suggesting quality over quantity in targeting.

## Repository Structure
```text
├── data/
│   └── marketing_campaign.csv   # Raw dataset
├── notebooks/
│   ├── 01_Data_Cleaning.ipynb   # Imputation & encoding
│   ├── 02_EDA.ipynb             # Summary statistics & distributions
│   └── 03_Modeling.ipynb        # LASSO/Ridge regression & White Test
├── results/
│   └── regression_tables.xlsx   # Full coefficient outputs
├── 326_project_v1.pdf           # Full research paper
└── README.md
