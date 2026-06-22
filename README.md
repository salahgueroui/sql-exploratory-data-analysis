# 📊 SQL Exploratory Data Analysis

A hands-on SQL project demonstrating **Exploratory Data Analysis (EDA)** techniques on a star-schema data warehouse. This project walks through a structured approach to understanding data — from schema discovery to ranking analysis — using pure SQL on SQL Server.

[![SQL Server](https://img.shields.io/badge/SQL_Server-2019+-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)](https://www.microsoft.com/sql-server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

## 🏗️ Project Overview

This project uses a **Gold-layer star schema** consisting of two dimension tables and one fact table, pre-loaded from a data warehouse pipeline. The focus is on writing analytical SQL queries to explore and understand the data.

### Star Schema

```
                ┌──────────────────┐
                │  dim_customers   │
                │──────────────────│
                │ customer_key (PK)│
                │ customer_id      │
                │ first_name       │
                │ last_name        │
                │ country          │
                │ marital_status   │
                │ gender           │
                │ birthdate        │
                │ create_date      │
                └────────┬─────────┘
                         │
                         │ customer_key
                         ▼
┌──────────────────┐    ┌──────────────────────┐
│  dim_products    │    │     fact_sales        │
│──────────────────│    │──────────────────────│
│ product_key (PK) │◄───│ product_key (FK)     │
│ product_id       │    │ customer_key (FK)    │
│ product_number   │    │ order_number         │
│ product_name     │    │ order_date           │
│ category_id      │    │ shipping_date        │
│ category         │    │ due_date             │
│ subcategory      │    │ sales_amount         │
│ maintenance      │    │ quantity             │
│ cost             │    │ price                │
│ product_line     │    └──────────────────────┘
│ start_date       │
└──────────────────┘
```

---

## 📂 Repository Structure

```
sql-exploratory-data-analysis/
│
├── datasets/                          # Source data files
│   ├── dim_customers.csv              # Customer dimension (18K+ rows)
│   ├── dim_products.csv               # Product dimension (295 rows)
│   └── fact_sales.csv                 # Sales fact table (60K+ rows)
│
├── scripts/                           # SQL scripts (run in order)
│   ├── 00_init_database.sql           # Create DB, tables & load CSVs
│   ├── 01_database_exploration.sql    # Explore schema & metadata
│   ├── 02_dimensions_exploration.sql  # Explore dimension values
│   ├── 03_date_range_exploration.sql  # Analyze temporal boundaries
│   ├── 04_measures_exploration.sql    # Calculate key business metrics
│   ├── 05_magnitude_analysis.sql      # Group & quantify by dimensions
│   └── 06_ranking_analysis.sql        # Rank top/bottom performers
│
├── docs/                              # Documentation & references
│   └── eda_notebook.md                # Analysis notes & findings
│
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- **SQL Server** 2019 or later (Developer/Express edition is fine)
- **SQL Server Management Studio (SSMS)** or Azure Data Studio

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/sql-exploratory-data-analysis.git
   ```

2. **Update the CSV file paths** in `scripts/00_init_database.sql`
   
   Find these lines and replace with your actual path:
   ```sql
   -- Change this:
   FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_customers.csv'
   -- To your path, for example:
   FROM 'C:\Users\YourName\Desktop\sql-exploratory-data-analysis\datasets\dim_customers.csv'
   ```

3. **Run scripts in order** (00 → 06) in SSMS

---

## 📋 Analysis Walkthrough

| # | Script | What You'll Learn | Key SQL Concepts |
|---|--------|-------------------|------------------|
| 00 | `init_database.sql` | Set up the database & load data | `CREATE DATABASE`, `BULK INSERT` |
| 01 | `database_exploration.sql` | Discover tables, columns, data types | `INFORMATION_SCHEMA` |
| 02 | `dimensions_exploration.sql` | Find unique categories, countries | `DISTINCT`, `ORDER BY` |
| 03 | `date_range_exploration.sql` | Understand time boundaries of the data | `MIN()`, `MAX()`, `DATEDIFF()` |
| 04 | `measures_exploration.sql` | Calculate totals, averages, counts | `SUM()`, `AVG()`, `COUNT()`, `UNION ALL` |
| 05 | `magnitude_analysis.sql` | Compare sizes across categories | `GROUP BY`, aggregate + `JOIN` |
| 06 | `ranking_analysis.sql` | Find top/bottom performers | `TOP`, `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` |

---

## 🔑 Key Business Questions Answered

- 📈 What is the total revenue, quantity sold, and average price?
- 🌍 How are customers distributed across countries?
- 🏆 Which 5 products generate the highest revenue?
- 📉 What are the worst-performing products?
- 👥 Who are the top 10 highest-revenue customers?
- 📅 What is the date range of our sales data?
- 🔢 How many unique orders, products, and customers exist?

---

## 🛡️ License

This project is licensed under the [MIT License](LICENSE).

---

## About Me

Hello, I'm **Salah Gueroui**, passionate about **Data Analytics, Business Intelligence, Data Engineering, and Artificial Intelligence**. I enjoy building data-driven solutions using **SQL, Python, Power BI, and modern database technologies**, turning raw data into meaningful insights and business value.
