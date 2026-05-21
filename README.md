# 🛍️ Customer Shopping Behavior Analysis

## 📌 Project Overview

This project analyzes customer shopping behavior using transactional data from 3,900 purchases across various product categories. The goal is to uncover insights into spending patterns, customer segments, product preferences, and subscription behavior to guide strategic business decisions.

**Tools Used:**
- Python (pandas, sqlalchemy) - Data cleaning & preparation
- SQL Server - Data analysis & business queries
- Power BI - Interactive dashboard
- Jupyter Notebook - Development environment

---

## 📁 Repository Files

| File | Description |
|------|-------------|
| [customer_shopping_behavior.csv](data/customer_shopping_behavior.csv) | Raw dataset |
| [data_cleaning.ipynb](notebooks/data_cleaning.ipynb) | Jupyter notebook with Python code |
| [business_queries.sql](sql/business_queries.sql) | All 10 SQL queries |
| [customer_dashboard.pbix](dashboard/customer_dashboard.pbix) | Power BI dashboard file |
| [requirements.txt](requirements.txt) | Python package dependencies |

---

## 📊 Dataset Summary

- **Rows:** 3,900
- **Columns:** 18
- **Key Features:**
  - Customer demographics (Age, Gender, Location, Subscription Status)
  - Purchase details (Item Purchased, Category, Purchase Amount, Season, Size, Color)
  - Shopping behavior (Discount Applied, Previous Purchases, Review Rating, Shipping Type)
- **Missing Data:** 37 values in Review Rating column (imputed using median by category)

---

## 🐍 Data Preparation ([data_cleaning.ipynb](notebooks/data_cleaning.ipynb))

- Loaded dataset using pandas
- Handled missing values in Review Rating column using median imputation by category
- Renamed columns to snake_case for consistency
- Created new features: `age_group`, `purchase_frequency_days`
- Removed redundant column (`promo_code_used`)
- Loaded cleaned data into SQL Server for analysis

---

## 📈 SQL Analysis ([business_queries.sql](sql/business_queries.sql))

| # | Question |
|---|----------|
| 1 | Revenue by Gender |
| 2 | High-spending discount users |
| 3 | Top 5 products by rating |
| 4 | Shipping type comparison (Standard vs Express) |
| 5 | Subscribers vs non-subscribers (avg spend & total revenue) |
| 6 | Top 5 products with highest discount percentage |
| 7 | Customer segmentation (New, Returning, Loyal) |
| 8 | Top 3 most purchased products per category |
| 9 | Repeat buyers (>5 purchases) vs subscription status |
| 10 | Revenue by age group |

**Sample Query - Customer Segmentation:**
```sql
select 
    case 
        when previous_purchases = 1 then 'New'
        when previous_purchases between 2 and 10 then 'Returning'
        else 'Loyal'
    end as customer_segment,
    count(*) as customer_count
from customer
group by 
    case 
        when previous_purchases = 1 then 'New'
        when previous_purchases between 2 and 10 then 'Returning'
        else 'Loyal'
    end;
