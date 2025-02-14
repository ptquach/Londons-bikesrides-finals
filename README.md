# Bike Share Data Analysis

## Overview
This project analyzes bike share data across different years and integrates cost analysis for better financial insights. The SQL script extracts, transforms, and combines bike ride data from multiple years with cost data to calculate revenue and profit.

## SQL Query Breakdown

### 1. **Common Table Expression (CTE)**
```sql
WITH cte AS (
    SELECT * FROM [dbo].[bike_share_yr_0]
    UNION ALL
    SELECT * FROM [dbo].[bike_share_yr_1]
)
```
- The `cte` combines data from two years (`bike_share_yr_0` and `bike_share_yr_1`) using `UNION ALL`, allowing for seamless aggregation of historical bike ride data.

### 2. **Main Query**
```sql
SELECT dteday, season, a.yr, weekday, hr, rider_type, riders, price, [COGS],
       riders * price AS revenue,
       riders * price - [COGS] AS profit
FROM cte AS a
LEFT JOIN [dbo].[cost_table] AS b
ON a.yr = b.yr;
```
- Selects relevant columns for analysis: `dteday`, `season`, `year`, `weekday`, `hour`, `rider_type`, `riders`, `price`, and `COGS`.
- Calculates **revenue** (`riders * price`).
- Computes **profit** (`revenue - COGS`).
- Uses a `LEFT JOIN` to integrate cost data from `[cost_table]`, ensuring that all bike rides have corresponding cost data when available.

## Required Database Tables
1. **bike_share_yr_0**
2. **bike_share_yr_1**
3. **cost_table**

## Dependencies
- SQL Server (or any compatible SQL database)
- Proper indexing on `yr` in both `bike_share_yr_*` tables and `cost_table` for performance optimization.

## Usage
1. Load the `bike_share_yr_0` and `bike_share_yr_1` datasets into your database.
2. Ensure `cost_table` is available and properly formatted.
3. Execute the SQL script to extract insights.
4. Analyze the output for revenue and profit trends.

## Future Enhancements
- Add more historical data to `bike_share_yr_*` tables.
- Optimize indexing to improve query performance.
- Develop a Power BI dashboard for visualizing trends.

## Author
**Phong Quach**

