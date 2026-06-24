# Customer Shopping Behavior Analysis

End-to-end analysis of 3,900 retail transactions covering data cleaning (Python), business querying (SQL), and visualization (Power BI).

## Project Overview

This project analyzes customer shopping behavior to uncover patterns in spending, product preferences, customer segments, and subscription behavior. The goal is to turn raw transactional data into business recommendations.

**Tech stack:** Python (pandas) · PostgreSQL · Power BI

## Repository Contents

| File | Description |
|---|---|
| `customer_shopping_behavior.csv` | Raw dataset (3,900 rows, 18 columns) |
| `Customer_Shopping_Behavior_Analysis.ipynb` | Python notebook: cleaning, feature engineering, EDA |
| `customer_shopping_behavior_DB.sql` | SQL queries answering 10 business questions |
| `customer_behavior_dashboard.pbix` | Power BI dashboard |
| `Customer_Shopping_Behavior_Analysis.pdf` | Full written report with results and recommendations |

## Dataset

- **Rows:** 3,900
- **Columns:** 18
- **Features:** Customer demographics (Age, Gender, Location, Subscription Status), purchase details (Item, Category, Amount, Season, Size, Color), shopping behavior (Discount Applied, Promo Code, Previous Purchases, Frequency, Review Rating, Shipping Type)
- **Missing data:** 37 nulls in `Review Rating`

## Methodology

### 1. Data Cleaning & Feature Engineering (Python)
- Loaded and inspected data with `pandas` (`df.info()`, `.describe()`)
- Imputed missing `Review Rating` values using the median rating per product category
- Standardized column names to snake_case
- Engineered `age_group` (binned) and `purchase_frequency_days`
- Checked redundancy between `discount_applied` and `promo_code_used`; dropped the latter
- Loaded the cleaned dataset into PostgreSQL

### 2. Business Analysis (SQL)
10 queries answering specific business questions — revenue by gender, discount behavior, top-rated products, shipping cost comparison, subscriber value, customer segmentation, category leaders, repeat-buyer subscription correlation, and revenue by age group. Full queries in `customer_shopping_behavior_DB.sql`.

### 3. Dashboard (Power BI)
Interactive dashboard with filters for subscription status, gender, category, and shipping type. KPIs include customer count, average purchase amount, and average review rating, plus revenue/sales breakdowns by category and age group.

## Key Findings

| Question | Result |
|---|---|
| Revenue by gender | Male: $157,890 vs. Female: $75,191 |
| Standard vs. Express shipping (avg spend) | $58.46 vs. $60.48 |
| Subscriber avg spend vs. non-subscriber | $59.49 vs. $59.87 (no meaningful difference) |
| Top-rated product | Gloves (3.86) |
| Most discount-dependent product | Hat (50% of purchases discounted) |
| Customer segments | Loyal: 3,116 · Returning: 701 · New: 83 |
| Repeat buyers (>5 purchases) subscribed | 958 of 2,518 non-subscribers vs. fewer among subscribers — no strong link between repeat purchases and subscribing |
| Highest revenue age group | Young Adult ($62,143) |

> Note: subscriber count (1,053) and average spend are nearly identical to non-subscribers — subscription status alone is **not** a strong revenue driver in this dataset.

## Business Recommendations

1. **Boost subscriptions** — current subscriber base is small (27%) relative to non-subscribers; promote exclusive benefits, since spend parity suggests subscription isn't yet capturing extra value.
2. **Loyalty programs** — convert "Returning" (701) and "New" (83) segments into "Loyal" through repeat-purchase incentives.
3. **Review discount policy** — high-discount items (Hat, Sneakers, Coat) may be eroding margin; test reduced discount depth against conversion impact.
4. **Product positioning** — feature top-rated items (Gloves, Sandals, Boots) and category leaders (Jewelry, Blouse, Sandals, Jacket) in campaigns.
5. **Targeted marketing** — prioritize Young Adult segment and Express-shipping users, the highest-revenue cohorts.

## How to Reproduce

```bash
# 1. Clone repo
git clone <repo-url>
cd customer-shopping-behavior-analysis

# 2. Set up Python environment
pip install pandas numpy matplotlib jupyter

# 3. Run the notebook
jupyter notebook Customer_Shopping_Behavior_Analysis.ipynb

# 4. Load cleaned data into PostgreSQL, then run customer_shopping_behavior_DB.sql

# 5. Open customer_behavior_dashboard.pbix in Power BI Desktop
```

## Limitations

- Dataset is synthetic/sample data — findings illustrate methodology, not real market conditions.
- Subscriber vs. non-subscriber comparison is observational; no causal claims (e.g., A/B test) are made.
- Discount-rate query in SQL uses integer division for the rate calculation — verify with `::numeric` cast if extending the analysis.

## Author

Zyad Omar — [github.com/Zyad665](https://github.com/Zyad665)
