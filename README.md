# Instacart Grocery Basket Analysis

## Project Overview

This project presents an exploratory data analysis (EDA) of Instacart's order and customer data using Python. The goal is to uncover sales patterns, understand customer purchasing behaviour, and generate actionable segmentation insights that business stakeholders can use to inform marketing and inventory strategies.

The analysis simulates a real-world analyst engagement — data is ingested, cleaned, transformed, enriched with derived variables, and segmented into customer profiles, culminating in a final stakeholder report.

---

## Business Questions Answered

- When do customers place the most orders (day of week, hour of day)?
- What price ranges drive the most volume?
- Which products and departments are most popular?
- How loyal are customers, and how does loyalty correlate with spending?
- How do purchasing behaviours differ across customer demographics (age, family status, income, region)?

---

## Dataset

Source: [Instacart Market Basket Analysis – Kaggle](https://www.kaggle.com/competitions/instacart-market-basket-analysis/data)

Key tables used:
- `orders.csv` — order-level data including day, time, and frequency
- `products.csv` — product catalogue with department and aisle mappings
- `order_products__prior.csv` — historical product-order associations
- `customers.csv` — demographic data including age, income, family status, and region

## Project Structure

- IC Project/
├── 03 Scripts/                  # Jupyter notebooks (analysis pipeline)
│   ├── 4.2  Library setup and data types
│   ├── 4.3  Data import and descriptive analysis
│   ├── 4.4  Data wrangling
│   ├── 4.5  Data consistency checks
│   ├── 4.6  Dataset merging (orders + products + customers)
│   ├── 4.7  Deriving new variables
│   ├── 4.8  Grouping, aggregation, and customer flags
│   ├── 4.9  Customer profiling (Parts 1 & 2)
│   └── 4.10 Final aggregations and visualizations
├── 04 Analysis/
│   └── Visualizations/          # All exported charts (PNG)
└── 05 Sent to clients/
└── Instacart_final_report.xlsx   # Stakeholder deliverable


---

## Analysis Pipeline

**1. Data Import & Descriptive Analysis**
Raw CSVs are loaded with selective column imports for efficiency. Initial shape, data types, and descriptive statistics are reviewed across orders and products datasets.

**2. Data Consistency Checks**
- Null value detection and handling (e.g. `days_since_prior_order` nulls retained as valid first-order indicators)
- Mixed-type column detection
- Duplicate identification and removal
- Outlier flagging (prices > $100 set to NaN)

**3. Dataset Merging**
Orders, products, and customer datasets are merged sequentially into a single unified dataframe, exported as a `.pkl` file for downstream use.

**4. Derived Variables**
New columns engineered from existing data:
- `busiest_day` / `busiest_days` — order volume labels by day of week
- `busiest_period_of_day` — peak hour classification (Most / Average / Fewest orders)
- `price_range_loc` — product price tier (Low / Mid / High-range)

**5. Customer Segmentation Flags**
Three behavioural flags created via `groupby` + `transform`:
- **Loyalty flag** — New / Regular / Loyal customer based on total order count
- **Spending flag** — Low / High spender based on average order price
- **Order frequency flag** — Frequent / Regular / Non-frequent based on median days between orders

**6. Customer Profiling & Aggregations**
Segments analysed across demographic dimensions including age group, family status, income bracket, and region. Key aggregations include mean/min/max spend, most purchased products per segment, and total sales contribution.

---

## Visualizations

Charts exported to `04 Analysis/Visualizations/`:

| Chart | Description |
|---|---|
| `bar_orders_dow.png` | Order volume by day of week |
| `hist_popular_hours.png` | Order distribution by hour |
| `hist_prices.png` | Product price distribution |
| `price_range_bar.png` | Orders by price tier (%) |
| `loyalty_pie.png` | Customer loyalty breakdown |
| `loyalty_region.png` | Loyalty distribution by region |
| `loyalty_products_bar.png` | Top products by loyalty segment |
| `age_income.png` | Spending patterns by age and income |
| `age_family_bar.png` | Order behaviour by age and family status |
| `family_income_bar.png` | Revenue contribution by family/income profile |
| `products_region_bar.png` | Product popularity by region |

---

## Tools & Libraries

- **Python 3** — pandas, NumPy, Matplotlib, Seaborn, SciPy
- **Jupyter Notebook** — analysis environment
- **Excel** — final stakeholder report delivery

---

## Key Findings (Summary)

- Orders peak on **Sundays and Mondays**, with the heaviest activity between **9am and 4pm**
- The majority of products fall in the **mid-range price tier ($5–$15)**
- Purchasing behaviour varies meaningfully across **age, family status, and region**, supporting targeted segmentation strategies

---

## Deliverable

A final stakeholder report (`Instacart_final_report.xlsx`) was produced summarising all insights and recommendations, formatted for a non-technical business audience.
