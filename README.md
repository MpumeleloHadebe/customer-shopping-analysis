# Customer Shopping Behavior Analysis

## Project Overview

This project analyzes customer shopping behavior using transactional data from 3,900 purchases across various product categories. The goal is to uncover insights into spending patterns, customer segments, product preferences, and subscription behavior to guide strategic business decisions.

**Tools Used:**
- Python (pandas, sqlalchemy) - Data cleaning & preparation
- SQL Server - Data analysis & business queries
- Power BI - Interactive dashboard
- Jupyter Notebook - Development environment

---

## Repository Files

| File | Description |
|------|-------------|
| [customer_shopping_behavior.csv](data/customer_shopping_behavior.csv) | Raw dataset |
| [data_cleaning.ipynb](notebooks/data_cleaning.ipynb) | Jupyter notebook with Python code |
| [business_queries.sql](sql/business_queries.sql) | All 10 SQL queries |
| [customer_dashboard.pbix](dashboard/customer_dashboard.pbix) | Power BI dashboard file |
| [presentation.pptx](presentation.pptx) | PowerPoint presentation for stakeholders |
| [requirements.txt](requirements.txt) | Python package dependencies |

---

## Dataset Summary

- **Rows:** 3,900
- **Columns:** 18
- **Key Features:**
  - Customer demographics (Age, Gender, Location, Subscription Status)
  - Purchase details (Item Purchased, Category, Purchase Amount, Season, Size, Color)
  - Shopping behavior (Discount Applied, Previous Purchases, Review Rating, Shipping Type)
- **Missing Data:** 37 values in Review Rating column (imputed using median by category)

---

## Data Preparation ([data_cleaning.ipynb](notebooks/data_cleaning.ipynb))

- Loaded dataset using pandas
- Handled missing values in Review Rating column using median imputation by category
- Renamed columns to snake_case for consistency
- Created new features: `age_group`, `purchase_frequency_days`
- Removed redundant column (`promo_code_used`)
- Loaded cleaned data into SQL Server for analysis

---

## SQL Analysis ([business_queries.sql](sql/business_queries.sql))

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
```

---

## Power BI Dashboard ([dashboard_preview.png](dashboard/dashboard_preview.png))

**Key Features:**
- KPI Cards (Total Revenue, Avg Purchase Amount, Avg Review Rating)
- Filters: Subscription Status, Gender, Location, Category, Shipping Method
- Visuals: Revenue by subscription, Top 5 products, Revenue by category, Customer segments

---

## Business Recommendations

| Recommendation | Action |
|----------------|--------|
| Boost Subscriptions | Promote exclusive benefits for subscribers (current rate: 27%) |
| Customer Loyalty Programs | Reward repeat buyers to move them into "Loyal" segment |
| Review Discount Policy | Balance sales boosts with margin control |
| Product Positioning | Highlight top-rated and best-selling products in campaigns |
| Targeted Marketing | Focus on high-revenue age groups and express shipping users |

---

## Repository Structure


```text
customer-behavior-analysis/
│
├── data/
│   └── customer_shopping_behavior.csv
│
├── notebooks/
│   └── data_cleaning.ipynb
│
├── sql/
│   └── business_queries.sql
│
├── dashboard/
│   ├── customer_dashboard.pbix
│   └── dashboard_preview.png
│
├── presentation.pptx
├── README.md
└── requirements.txt
```

---

## How to Reproduce

### 1. Clone the repository

```bash
git clone [https://github.com/MpumeleloHadebe/customer-shopping-analysis.git
```

### 2. Install Python packages

```bash
pip install -r requirements.txt
```

### 3. Run Jupyter notebook

Open:

```text
notebooks/data_cleaning.ipynb
```

### 4. Run SQL queries

Execute:

```text
sql/business_queries.sql
```

in SQL Server.

### 5. Open Power BI Dashboard

Open:

```text
dashboard/customer_dashboard.pbix
```

---

## Requirements (`requirements.txt`)

```text
pandas==2.0.3
sqlalchemy==2.0.19
pyodbc==5.0.1
openpyxl==3.1.2
```

---

## Author
Mpumelelo Hadebe

---

##  Date

2026
