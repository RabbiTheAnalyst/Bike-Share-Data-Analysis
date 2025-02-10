![SQL](https://img.shields.io/badge/language-SQL-brightgreen)

## 🚴‍♂️ Bike Share Data Analysis  

This project analyzes bike-sharing data using **SQL, Excel, and Power BI**. The following SQL query extracts key insights, including revenue and profit calculations.
### **📌 SQL Query Used (MS SQL Server)**
```tsql 
with cte as (
select *  from  bike_share_yr_0
Union all
select *  from  bike_share_yr_1)

select 
dteday,
season,
a.yr,
weekday,
hr,
rider_type,
riders,
price,
COGS,
riders*price as revenue,
riders*price-COGS as profit
from cte a 
left join cost_table b 
on a.yr = b.yr
