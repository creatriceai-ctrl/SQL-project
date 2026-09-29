# Retail Sales Analysis (SQL Project)

## 📌 Project Overview
This project focuses on analyzing retail sales data using SQL (MySQL Workbench) to extract actionable business insights. Using a Reverse Learning approach, the analysis addresses key business questions around customer demographics, temporal sales trends, product category performance, and Average Order Value (AOV).

---

## 🛠️ Tools & Skills
- Database Management: MySQL Workbench
- SQL Concepts Used: AVG(), ROUND(), GROUP BY, ORDER BY, Aggregate Functions, Data Cleaning (IS NULL).
- Documentation: Markdown & GitHub.

## Key Queries, Screenshots & Business Insights

### 1. Data Cleaning

SQl
SELECT * FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;

![Data Cleaning](Screenshot%202026-09-27%20110141.png)

---

### 2. total profits and revenue anaysis

SQL
SELECT 
    category,
    SUM(quantity) AS total_quantity,
    SUM(total_sale) AS total_revenue
FROM retail_sales
GROUP BY category
ORDER BY total_revenue DESC;
select category 
sum(total_sale) as total_revenue,
 sum(cogf) as total_cost,
 sum(total_sale - cogf) as total_profit,
 sum(quantiy) as total_quantity_sold
  From retail_sales
  group by category
  order by total_revenue;

<img src="Screenshot 2026-09-27 110223.png" width="100%">


### 3. Customer Demographics and category breakdown
Business Question: How are sales distributed across different genders?

SQL
SELECT 
    gender,
    COUNT(DISTINCT customer_id) AS total_customers,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY gender;
select gender, category, 
round(avg(age), 0) as avg_age,
count(*) as total_orders,
sum(total_sale) as total_sales
from retail_sales 
group by gender, category
order by gender, total_sales desc;

---
<img src="Screenshot 2026-09-27 110252.png" width="100%">

### 4. Average Order Value (AOV)
Business Question: What is the Average Order Value (AOV) across product categories?
select category,
round(avg(total_sale),2) as avg_order_value
from retail_sales
group by category
order by avg_order_value desc;

<img src="Screenshot 2026-09-29 015626.png" width="100%">

<img src="Screenshot 2026-09-29 015714.png" width="100%">

SQL
SELECT 
    category,
    ROUND(AVG(total_sale), 2) AS avg_order_value
FROM retail_sales
GROUP BY category
ORDER BY avg_order_value DESC;

---

### 5. Temporal Sales Trends
Business Question: How do sales trends change month by month?

SQL
SELECT 
    EXTRACT(MONTH FROM sale_date) AS sale_month,
    SUM(total_sale) AS monthly_sales
FROM retail_sales
GROUP BY sale_month
ORDER BY monthly_sales DESC;


