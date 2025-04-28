## 🚴‍♂️ Bike Share Data Analysis Project

<div align="left">
  
**Tech Stack**  
![Microsoft SQL Server](https://img.shields.io/badge/Microsoft_SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

</div>

### 📌 Project Overview
- Analyzed **2+ million ride records** across 2 years
- Calculated revenue/profit metrics per rider type
- Built **3 interactive Power BI dashboards**
- Achieved **92% data accuracy** after cleaning

---

### 🔍 Core SQL Analysis
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
