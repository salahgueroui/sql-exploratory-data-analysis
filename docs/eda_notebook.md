# 📓 SQL Analytics & EDA Notebook

This document serves as a detailed companion to the SQL scripts, documenting the analytical approach, methodologies, SQL techniques, and key findings.

---

## 🏗️ Methodology & Analysis Flow

The project follows a structured, multi-phase analytical flow to explore, analyze, and build reports from the data warehouse:

```
[Phase 1: Ingestion & Metadata Exploration]
  ├── Script 00: Database Setup & Load  → Set up schemas and load CSV datasets
  └── Script 01: Metadata Exploration   → Explore database schemas, tables, and columns

[Phase 2: Data Exploration & Integrity Checks]
  ├── Script 02: Dimensions Exploration  → Discover unique values in categorical variables
  ├── Script 03: Date Range Exploration  → Analyze temporal boundaries and age spans
  └── Script 04: Measures Exploration    → Calculate baseline business counts and sums

[Phase 3: Advanced Business Analytics (EDA)]
  ├── Script 05: Magnitude Analysis       → Quantify and aggregate metrics across dimensions
  ├── Script 06: Ranking Analysis         → Find top/bottom products, customers, and orders
  ├── Script 07: Change Over Time         → Track monthly and yearly revenue trends
  ├── Script 08: Cumulative Analysis      → Calculate running totals and moving averages
  ├── Script 09: Performance Analysis     → Conduct Year-over-Year (YoY) product growth analysis
  ├── Script 10: Data Segmentation        → Classify customers and products into behavioral tiers
  └── Script 11: Part-to-Whole Analysis   → Measure sales contributions by category

[Phase 4: Reporting & BI Views Layer]
  ├── Script 12: Customer Report View     → Consolidate customer KPIs (recency, AOV, spend)
  └── Script 13: Product Report View      → Consolidate product KPIs (AOR, monthly revenue)
```

---

## 📝 Script Breakdown & Core Learning

### 🧱 Phase 1: Database Setup & Exploration

#### Script 00 — Database Setup (`00_init_database.sql`)
- Recreates the `DataWarehouseAnalytics` database cleanly.
- Establishes a `gold` schema and creates three tables (`dim_customers`, `dim_products`, `fact_sales`).
- Performs `BULK INSERT` from CSV datasets to load the star schema tables.
- Runs quick validation `COUNT(*)` queries to check that data is fully loaded.

#### Script 01 — Metadata Exploration (`01_database_exploration.sql`)
- Uses system metadata tables (`INFORMATION_SCHEMA.TABLES` and `INFORMATION_SCHEMA.COLUMNS`).
- Queries column names and data types to understand the table designs before writing logic.

---

### 🔍 Phase 2: Exploratory Data Analysis (EDA)

#### Script 02 — Dimensions Exploration (`02_dimensions_exploration.sql`)
- Uses `DISTINCT` to check the quality and range of categorical values.
- Identifies unique countries, categories, subcategories, and genders.

#### Script 03 — Date Range Exploration (`03_date_range_exploration.sql`)
- Checks the time frame of sales transactions using `MIN()` and `MAX()`.
- Calculates date intervals (`DATEDIFF()`) to see the dataset's historical span.

#### Script 04 — Measures Exploration (`04_measures_exploration.sql`)
- Aggregates basic business metrics: total sales, quantity sold, average unit prices, unique orders, and unique customers.
- Employs `UNION ALL` to compile these metrics into a structured, unified summary.

#### Script 05 — Magnitude Analysis (`05_magnitude_analysis.sql`)
- Groups transactions by dimensions (country, category) to see where the bulk of sales are concentrated.
- Joins the fact table to the dimension tables to align numeric transactions with labels.

#### Script 06 — Ranking Analysis (`06_ranking_analysis.sql`)
- Utilizes ranking window functions (`RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`) to identify performance.
- Determines the top 5 products by revenue, top 10 customers by revenue, and worst performing products.

---

### 📈 Phase 3: Advanced Business Analytics

#### Script 07 — Change Over Time Analysis (`07_change_over_time_analysis.sql`)
- Tracks revenue growth and seasonality across months and years.
- Demonstrates three formatting and truncation techniques for time groupings: `YEAR() + MONTH()`, `DATETRUNC()`, and `FORMAT()`.

#### Script 08 — Cumulative Analysis (`08_cumulative_analysis.sql`)
- Calculates monthly running totals of revenue and moving averages of selling prices.
- Uses window aggregate functions: `SUM(...) OVER (ORDER BY ...)` and `AVG(...) OVER (ORDER BY ...)`.

#### Script 09 — Performance Analysis (`09_performance_analysis.sql`)
- Benchmarks annual product performance against previous-year figures and overall averages.
- Uses the `LAG()` window function to fetch previous-year sales and partition-based averages (`AVG(...) OVER (PARTITION BY ...)`).

#### Script 10 — Data Segmentation (`10_data_segmentation.sql`)
- Groups customers and products into behavioral tiers.
- Sets up product cost ranges (`Below 100`, `100-500`, etc.).
- Categorizes customers into `VIP` (spending > $5k and lifecycle >= 12 months), `Regular` (spending <= $5k and lifecycle >= 12 months), or `New` (lifecycle < 12 months) based on sales figures and lifespan in months.

#### Script 11 — Part-to-Whole Analysis (`11_part_to_whole_analysis.sql`)
- Evaluates the sales contribution percentage of each product category to total sales.
- Uses a grand-total window sum (`SUM(sales_amount) OVER ()`) as the denominator to perform calculations.

---

### 📊 Phase 4: Reporting & BI Views Layer

#### Script 12 — Customer Report View (`12_report_customers.sql`)
- Consolidates demographic details (name, age, age-group) and purchase habits at the individual customer level.
- Calculates crucial customer lifetime metrics: **Recency** (months since last purchase), **Lifespan** (duration active), **Average Order Value (AOV)**, and **Average Monthly Spend**.
- Standardizes customer segmentations (`VIP`, `Regular`, `New`) into a queryable view (`gold.report_customers`) to enable downstream BI reporting.

#### Script 13 — Product Report View (`13_report_products.sql`)
- Builds a unified view (`gold.report_products`) containing key metrics for products: category, subcategory, lifespan, average selling price.
- Computes product metrics: **Average Order Revenue (AOR)** and **Average Monthly Revenue**.
- Segments products into performance tiers: `High-Performer` (sales > $50k), `Mid-Range` (sales $10k–$50k), and `Low-Performer` (sales < $10k).

---

## 🛠️ SQL Techniques Covered

This project demonstrates proficiency in several critical SQL techniques:

| Technique | SQL Syntax / Functions | Scripts |
|-----------|------------------------|---------|
| **Metadata Queries** | `INFORMATION_SCHEMA.TABLES`, `INFORMATION_SCHEMA.COLUMNS` | 01 |
| **Basic Aggregations** | `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()` | 03, 04, 05 |
| **Conditional Logic** | `CASE WHEN ... THEN ... ELSE ... END` | 09, 10, 12, 13 |
| **Temporal Math** | `DATEDIFF()`, `DATETRUNC()`, `YEAR()`, `MONTH()`, `FORMAT()` | 03, 07, 08, 10, 12, 13 |
| **Window Functions (Ranking)** | `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()` | 06 |
| **Window Functions (Aggs)** | `SUM() OVER ()`, `SUM() OVER (ORDER BY ...)`, `AVG() OVER (PARTITION BY ...)` | 08, 09, 11 |
| **Window Functions (Value)** | `LAG() OVER (PARTITION BY ... ORDER BY ...)` | 09 |
| **Data Shaping & CTEs** | `WITH table_name AS (...)`, `UNION ALL` | 04, 09, 10, 11, 12, 13 |
| **View Creation & DDL** | `CREATE VIEW`, `OBJECT_ID()`, `DROP VIEW` | 12, 13 |
