## 🚴‍♂️ Bike Share Data Analysis  

This project analyzes bike-sharing data using **SQL, Excel, and Power BI**. The following SQL query extracts key insights, including revenue and profit calculations.

### **📌 SQL Query Used**
```sql
WITH cte AS (
    SELECT * FROM bike_share_yr_0
    UNION ALL
    SELECT * FROM bike_share_yr_1
)
SELECT 
    dteday,
    season,
    a.yr,
    weekday,
    hr,
    rider_type,
    riders,
    price,
    COGS,
    riders * price AS revenue,
    riders * price - COGS AS profit
FROM cte a 
LEFT JOIN cost_table b 
ON a.yr = b.yr;

📊 Insights from the Analysis
🚲 Calculated total revenue and profit for each year.
📅 Analyzed ridership trends based on season, weekdays, and hours.
🔍 Used CTE (Common Table Expression) to merge yearly data efficiently.

📌 Want to see the full analysis? Check out the dataset and Power BI visualization! 🚀
---
🚀 Created by **Md Rabbi Ali** | 📧 rabbi.stat.iu@gmail.com
