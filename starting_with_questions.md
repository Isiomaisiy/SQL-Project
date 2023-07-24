Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT country, city, SUM(CAST(totalTransactionRevenue AS NUMERIC)) AS totalTransactionRevenue
FROM all_sessions
WHERE totalTransactionRevenue IS NOT null AND city is NOT null
GROUP BY country, city
ORDER BY totalTransactionRevenue DESC
LIMIT 1


Answer:
This script returns the country and city with the highest number of total transaction revenues,because the column was created as TEXT data type and cast was used to convert data type to numeric.

pictures\Starting with questions 1.png



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT analytics.fullvisitorid, all_sessions.country, all_sessions.city , cast(AVG(CAST(units_sold AS NUMERIC)) as numeric(6,2)) as AverageQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY analytics.fullvisitorid, all_sessions.country, all_sessions.city
ORDER BY AverageQty DESC



Answer:

The null values were eliminated for city and unit sold

pictures\Starting with questions 2.png




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL AND v2ProductCategory IS NOT null
GROUP BY all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductCategory




Answer:

There was no recognizable pattern in the types (product categories) of products ordered from visitors in each city and country.

pictures\Starting with questions 3.png





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT all_sessions.v2ProductName, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY all_sessions.v2ProductName, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductName


Answer:

There was no regonizable pattern worthy of noting in the product sold.

pictures\Starting with questions 4.png





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

with cte as (
SELECT all_sessions.country, all_sessions.city , SUM(CAST(revenue AS NUMERIC)) as TotalRevenue
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE revenue IS NOT null AND city IS NOT NULL
GROUP BY all_sessions.country, all_sessions.city
--ORDER BY all_sessions.country, all_sessions.city, TotalRevenue desc
)
select 
*,
RANK() OVER(ORDER BY TotalRevenue DESC) AS global_rank

FROM CTE
ORDER BY global_rank



Answer:

The UNITED STATES had the highest number of revenue generated as it has 15 states generating revenue more than other countries.

pictures\Starting with questions 5.png