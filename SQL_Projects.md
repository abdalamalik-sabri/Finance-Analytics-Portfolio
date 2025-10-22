# 🧩 SQL Project — Sales Performance Analysis

**Objective:**  
Analyze sales data to identify top-performing regions, profitable products, and customer segments.

**Business Questions:**  
1. Which regions generate the highest total revenue?  
2. What are the top 5 most profitable products?  
3. Which customers have the highest lifetime value (CLV)?  
4. What’s the monthly sales trend across the company?  

**Techniques Used:**  
- Aggregations and Grouping  
- CTEs (Common Table Expressions)  
- Window Functions (RANK, LAG)  
- Filtering with WHERE and HAVING clauses  

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
