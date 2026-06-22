# 📓 EDA Analysis Notebook

This document serves as a companion to the SQL scripts, documenting the analytical approach and key findings.

---

## Methodology

The EDA follows a structured 6-step approach:

```
Step 1: Database Exploration     → What tables/columns do we have?
Step 2: Dimensions Exploration   → What are the unique categories and values?
Step 3: Date Range Exploration   → What time period does the data cover?
Step 4: Measures Exploration     → What are the key business metrics?
Step 5: Magnitude Analysis       → How does data distribute across groups?
Step 6: Ranking Analysis         → Who/what are the top and bottom performers?
```

---

## Notes

### Script 00 — Database Setup
- Creates `DataWarehouseAnalytics` database with a `gold` schema
- Loads 3 CSV files: `dim_customers`, `dim_products`, `fact_sales`
- **Remember to update file paths** before running

### Script 01 — Database Exploration
- Uses `INFORMATION_SCHEMA.TABLES` and `INFORMATION_SCHEMA.COLUMNS`
- Helps understand table structure before writing queries

### Script 02 — Dimensions Exploration
- Identifies unique values in categorical columns
- Countries, categories, subcategories, product names

### Script 03 — Date Range Exploration
- Finds the first and last order dates
- Calculates total months of sales history
- Determines age range of customer base

### Script 04 — Measures Exploration
- Calculates: Total Sales, Total Quantity, Avg Price, Total Orders, Total Products, Total Customers
- Uses `UNION ALL` to build a consolidated KPI report

### Script 05 — Magnitude Analysis
- Groups data by dimensions (country, gender, category)
- Joins fact and dimension tables for cross-dimensional analysis
- Shows revenue by category, by customer, items sold by country

### Script 06 — Ranking Analysis
- Uses `TOP N` for simple ranking
- Uses `RANK()` window function for flexible ranking
- Identifies top 5 products, top 10 customers, bottom 3 customers

---

## SQL Techniques Covered

| Technique | Scripts |
|-----------|---------|
| `INFORMATION_SCHEMA` queries | 01 |
| `DISTINCT`, `ORDER BY` | 02 |
| `MIN()`, `MAX()`, `DATEDIFF()` | 03 |
| `SUM()`, `AVG()`, `COUNT()` | 04, 05 |
| `UNION ALL` | 04 |
| `GROUP BY` with aggregates | 05 |
| `JOIN` (fact ↔ dimension) | 05, 06 |
| `TOP N` | 06 |
| `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` | 06 |
