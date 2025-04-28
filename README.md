# 🚴‍♂️ Bike Share Data Analysis Project

<div align="center">

![SQL](https://img.shields.io/badge/SQL-Data_Analysis-blue?style=for-the-badge&logo=databricks&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-Data_Cleaning-green?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

</div>

---

## 📚 Project Overview

This project is focused on analyzing bike-sharing service data using **SQL**, **Excel**, and **Power BI**.  
The objective was to derive actionable insights, understand customer behavior, and visualize findings professionally.

---

## 🛠️ Tools Used

- **SQL Server Management Studio (SSMS)** - Data querying and profitability analysis
- **Microsoft Excel** - Data cleaning, preprocessing
- **Microsoft Power BI** - Data visualization and dashboard creation

---

## 🎯 Objectives

- Clean and transform raw bike share data
- Perform Exploratory Data Analysis (EDA)
- Analyze customer behavior across seasons and rider types
- Build a dynamic dashboard for better storytelling

---


---

## 🔍 Core SQL Analysis

```sql
-- Bike Share Profitability Analysis (MS SQL Server)
WITH combined_years AS (
  SELECT * FROM bike_share_yr_0
  UNION ALL
  SELECT * FROM bike_share_yr_1
)

SELECT 
  FORMAT(dteday, 'yyyy-MM') AS month,
  rider_type,
  COUNT(riders) AS total_rides,
  SUM(price) AS total_revenue,
  SUM(price * riders) - SUM(COGS) AS net_profit,
  ROUND((SUM(price * riders) - SUM(COGS)) / SUM(price * riders), 2) * 100 AS profit_margin
FROM combined_years c
LEFT JOIN cost_table ct ON c.yr = ct.yr
GROUP BY FORMAT(dteday, 'yyyy-MM'), rider_type
ORDER BY month, profit_margin DESC;

