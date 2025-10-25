# 🧩 SQL Project — Sales Performance Analysis

A modular SQL playbook for monitoring regional revenue, product profitability, and customer retention trends.

## 🎯 Objective
Provide finance and sales leaders with reusable queries that surface high-performing regions, profitable products, and early-warning signals for churn.

## 🗂️ Schema Snapshot
```
sales_data (
    order_id SERIAL,
    order_date DATE,
    region TEXT,
    customer_id TEXT,
    product_name TEXT,
    sales_amount NUMERIC,
    cost_amount NUMERIC,
    profit_margin NUMERIC
)
```

## 📚 Data Notes
- Designed for a typical sales fact table exported from CRM/ERP systems.
- Margin values assumed to be stored as decimals (e.g., 0.32 for 32%).
- Extend the schema with dimensional tables (regions, products, customers) for production deployments.

## 🛠️ Techniques Used
- Aggregations, window functions (`RANK`, `LAG`), and CTE pipelines for clarity.
- Conditional filters in `HAVING` clauses to isolate priority segments.
- Year-over-year comparisons to detect declining customers early.

## 💡 Business Impact
Use the declining-customer query to trigger retention campaigns, the product profitability query to inform assortment decisions, and the monthly trend query to manage revenue pacing against targets.

## ▶️ How to Run
1. Create a staging database (PostgreSQL, Snowflake, or SQL Server) and load your `sales_data` fact table.
2. Copy the queries below into your SQL IDE and replace table names if needed.
3. Schedule the relevant queries as part of a BI refresh or reporting automation pipeline.

---

## 📜 SQL Code
```sql
-- =========================================
-- SQL Project: Sales Performance Analysis
-- Author: Abdalmalik Sabri
-- =========================================

-- 1️⃣ Total Sales by Region
SELECT
    region,
    ROUND(SUM(sales_amount), 2) AS total_sales,
    RANK() OVER (ORDER BY SUM(sales_amount) DESC) AS region_rank
FROM sales_data
GROUP BY region;

-- 2️⃣ Top 5 Profitable Products
SELECT
    product_name,
    ROUND(SUM(sales_amount - cost_amount), 2) AS profit,
    ROUND(AVG(profit_margin * 100), 2) AS avg_margin_percent
FROM sales_data
GROUP BY product_name
ORDER BY profit DESC
LIMIT 5;

-- 3️⃣ Monthly Sales Trend
SELECT
    DATE_TRUNC('month', order_date) AS month,
    ROUND(SUM(sales_amount), 2) AS monthly_sales
FROM sales_data
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;

-- 4️⃣ Customer Lifetime Value (CLV)
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(sales_amount) AS total_spent,
        COUNT(DISTINCT order_id) AS num_orders
    FROM sales_data
    GROUP BY customer_id
)
SELECT
    customer_id,
    total_spent,
    num_orders,
    ROUND(total_spent / num_orders, 2) AS avg_order_value
FROM customer_sales
ORDER BY total_spent DESC
LIMIT 10;

-- 5️⃣ Identify Declining Customers (YoY Sales Drop)
WITH yearly_sales AS (
    SELECT
        customer_id,
        EXTRACT(YEAR FROM order_date) AS year,
        SUM(sales_amount) AS total_sales
    FROM sales_data
    GROUP BY customer_id, EXTRACT(YEAR FROM order_date)
),
compare_years AS (
    SELECT
        a.customer_id,
        a.total_sales AS sales_2023,
        b.total_sales AS sales_2024,
        (b.total_sales - a.total_sales) AS sales_change
    FROM yearly_sales a
    JOIN yearly_sales b
      ON a.customer_id = b.customer_id AND a.year = b.year - 1
)
SELECT
    customer_id,
    sales_2023,
    sales_2024,
    sales_change
FROM compare_years
WHERE sales_change < 0
ORDER BY sales_change ASC;
```
