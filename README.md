# 🚴‍♂️ Bike Share Data Analysis Project

<div align="left">
  <img src="https://img.shields.io/badge/SQL-Data_Analysis-blue?style=for-the-badge&logo=databricks&logoColor=white" alt="SQL">
  <img src="https://img.shields.io/badge/Excel-Data_Cleaning-green?style=for-the-badge&logo=microsoft-excel&logoColor=white" alt="Excel">
  <img src="https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI">
</div>

---

## 📚 Project Overview
Analyzed 2+ years of bike-sharing data to uncover:
- Revenue and profit trends
- Peak usage patterns
- Rider type comparisons (casual vs members)

---

## 🔍 Core SQL Analysis

```sql
-- Bike Share Profitability Analysis (MS SQL Server)
WITH combined_data AS (
  SELECT 
    dteday,
    yr,
    season,
    weekday,
    hr,
    rider_type,
    riders,
    price
  FROM bike_share_yr_0
  
  UNION ALL
  
  SELECT 
    dteday,
    yr,
    season,
    weekday,
    hr,
    rider_type,
    riders,
    price
  FROM bike_share_yr_1
),

profit_calculation AS (
  SELECT
    c.*,
    ct.cogs,
    (c.riders * c.price) AS revenue,
    (c.riders * c.price) - ct.cogs AS profit
  FROM combined_data c
  JOIN cost_table ct ON c.yr = ct.yr
)

SELECT
  FORMAT(dteday, 'yyyy-MM') AS month,
  rider_type,
  COUNT(*) AS total_rides,
  SUM(revenue) AS total_revenue,
  SUM(profit) AS net_profit,
  ROUND((SUM(profit) / SUM(revenue)) * 100, 2) AS profit_margin_pct,
  SUM(CASE WHEN hr BETWEEN 7 AND 9 THEN riders ELSE 0 END) AS morning_commute_rides,
  SUM(CASE WHEN hr BETWEEN 17 AND 19 THEN riders ELSE 0 END) AS evening_commute_rides
FROM profit_calculation
GROUP BY FORMAT(dteday, 'yyyy-MM'), rider_type
ORDER BY month, profit_margin_pct DESC;
