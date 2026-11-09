# 🛍️ Customer Shopping Behavior Analysis

End-to-end data analysis of customer purchasing behavior using **Python**, **PostgreSQL** and **Power BI**. The project cleans a 3,900-record retail dataset, answers ten business questions with SQL, and presents the results in an interactive dashboard.

![Python](https://img.shields.io/badge/Python-3.9+-blue)
![pandas](https://img.shields.io/badge/pandas-data%20cleaning-150458)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-SQL%20analysis-336791)
![Power BI](https://img.shields.io/badge/Power%20BI-dashboard-F2C811)

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Workflow](#-workflow)
- [Business Questions](#-business-questions-answered-in-sql)
- [Key Findings](#-key-findings)
- [Dashboard](#-dashboard)
- [Recommendations](#-business-recommendations)
- [Limitations](#-limitations)
- [Repository Structure](#-repository-structure)
- [How to Run](#-how-to-run)

---

## 📖 Project Overview

The goal is to uncover insights into **spending patterns, customer segments, product preferences and subscription behavior** to support strategic business decisions such as pricing, loyalty programs and marketing.

## 📊 Dataset

| Attribute | Detail |
|---|---|
| Rows | 3,900 |
| Columns | 18 |
| Missing data | 37 values in `Review Rating` |

**Feature groups**

- **Demographics:** Age, Gender, Location, Subscription Status
- **Purchase details:** Item Purchased, Category, Purchase Amount (USD), Season, Size, Color
- **Shopping behavior:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type, Payment Method

## 🛠️ Tech Stack

| Stage | Tool |
|---|---|
| Data cleaning and feature engineering | Python (pandas) |
| Database and business queries | PostgreSQL |
| Dashboard | Power BI |

## 🔄 Workflow

### 1. Data preparation (Python)

- Loaded the data with `pandas` and explored it with `df.info()` and `df.describe()`
- Imputed the 37 missing `Review Rating` values using the **median rating per product category**
- Standardized column names to **snake_case**
- Engineered features:
  - `age_group`: binned customer ages
  - `purchase_frequency_days`: numeric version of purchase frequency
- Checked `discount_applied` vs. `promo_code_used`; found them redundant and dropped `promo_code_used`
- Loaded the cleaned DataFrame into **PostgreSQL**

### 2. Analysis (PostgreSQL)

Ten business questions answered with aggregations, `CASE` logic, subqueries and window functions.

### 3. Visualization (Power BI)

Interactive dashboard with KPI cards and filters for subscription status, gender, category and shipping type.

## ❓ Business Questions Answered in SQL

1. **Revenue by Gender:** male vs. female revenue
2. **High-Spending Discount Users:** customers who used a discount but spent above average (839 customers)
3. **Top 5 Products by Rating:** highest average review ratings
4. **Shipping Type Comparison:** average purchase amount, Standard vs. Express
5. **Subscribers vs. Non-Subscribers:** average spend and total revenue
6. **Discount-Dependent Products:** top 5 products by share of discounted purchases
7. **Customer Segmentation:** New, Returning and Loyal customers
8. **Top 3 Products per Category:** most purchased items within each category
9. **Repeat Buyers and Subscriptions:** are customers with more than 5 purchases more likely to subscribe?
10. **Revenue by Age Group:** revenue contribution of each age group

## 🔍 Key Findings

| Metric | Result |
|---|---|
| Total revenue | **$233,081** |
| Average purchase amount | **$59.76** |
| Average review rating | **3.75 / 5** |
| Subscription rate | **27%** (1,053 of 3,900) |

- **Gender:** Male customers generate $157,890 (67.7%) vs. $75,191 for female customers. The gap comes from customer count (68% male), not spend per customer (about $59.5 vs. $60.3).
- **Subscriptions:** Subscribers spend about the same as non-subscribers ($59.49 vs. $59.87), so subscriptions show no spending uplift.
- **Repeat buyers:** 958 of 3,476 repeat buyers (27.6%) subscribe, nearly identical to the overall 27.0% rate.
- **Shipping:** Express buyers spend slightly more than Standard ($60.48 vs. $58.46).
- **Top-rated products:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.78).
- **Most discount-dependent:** Hat (50.00%), Sneakers (49.66%), Coat (49.07%), Sweater (48.17%), Pants (47.37%).
- **Segments:** Loyal 3,116 · Returning 701 · New 83.
- **Age groups:** Young Adult $62,143 · Middle-aged $59,197 · Adult $55,978 · Senior $55,763. Revenue is spread fairly evenly.
- **Categories:** Clothing is the largest category (1,737 of 3,900 purchases), followed by Accessories, Footwear and Outerwear.

## 📈 Dashboard

The Power BI dashboard includes:

- KPIs: number of customers (3.9K), average purchase amount ($59.76), average review rating (3.75)
- Subscription split (27% subscribed / 73% not)
- Revenue and sales by category
- Revenue and sales by age group
- Slicers: subscription status, gender, category, shipping type

> Add a screenshot here:
> `![Dashboard](images/dashboard.png)`

## 💡 Business Recommendations

- **Boost subscriptions:** add exclusive benefits (free or express shipping, early access, member pricing), since subscribers do not currently spend more.
- **Convert repeat buyers:** target the 2,518 non-subscribed repeat buyers.
- **Review discount policy:** about half of purchases of the top discount-dependent items are discounted; balance sales with margin.
- **Loyalty programs:** reward repeat buyers and redefine segment thresholds, since 80% of customers are labeled Loyal.
- **Product positioning:** feature top-rated and best-selling products in campaigns.
- **Targeted marketing:** grow the female customer base and promote express shipping.

## ⚠️ Limitations

- No purchase date, so no trend, seasonality or cohort analysis
- No cost or margin data, so discount impact on profit cannot be measured
- One row per customer, so lifetime value cannot be calculated
- Differences such as Express vs. Standard are small; statistical testing is recommended before acting on them

## 📁 Repository Structure

> Adjust this to match your actual files.

```
customer-shopping-behavior-analysis/
├── data/
│   └── customer_shopping_behavior.csv
├── notebooks/
│   └── eda_and_cleaning.ipynb
├── sql/
│   └── business_queries.sql
├── dashboard/
│   └── customer_behavior_dashboard.pbix
├── images/
│   └── dashboard.png
├── reports/
│   └── Customer_Shopping_Behavior_Analysis.pdf
├── requirements.txt
└── README.md
```

## ▶️ How to Run

**1. Clone the repository**

```bash
git clone https://github.com/<your-username>/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
```

**2. Install dependencies**

```bash
pip install pandas numpy sqlalchemy psycopg2-binary jupyter
```

**3. Run the cleaning notebook**

Open `notebooks/eda_and_cleaning.ipynb` and run all cells. This cleans the data and loads it into PostgreSQL.

**4. Configure the database connection**

```python
from sqlalchemy import create_engine

engine = create_engine("postgresql://<user>:<password>@localhost:5432/<database>")
df.to_sql("customer", engine, if_exists="replace", index=False)
```

> Use environment variables for credentials. Never commit passwords.

**5. Run the SQL queries**

Execute `sql/business_queries.sql` in pgAdmin or `psql`.

**6. Open the dashboard**

Open `dashboard/customer_behavior_dashboard.pbix` in Power BI Desktop.

## 👤 Author

**Your Name** · [LinkedIn](https://linkedin.com/in/your-profile) · [GitHub](https://github.com/your-username)

---

⭐ If you found this project useful, consider giving it a star!
