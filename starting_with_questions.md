## **Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

#### Answer
This script returns the country and city with the highest number of total transaction revenues

```
SELECT country, city, SUM(CAST(totalTransactionRevenue AS NUMERIC)) AS totalTransactionRevenue
FROM all_sessions
WHERE totalTransactionRevenue IS NOT null AND city is NOT null
GROUP BY country, city
ORDER BY totalTransactionRevenue DESC
LIMIT 1
```
Here is the screenshot of the result.

![](/pictures/Starting_with_questions_1.png)



## **Question 2: What is the average number of products ordered from visitors in each city and country?**
#### Answer
I made an assumtion here that we want to see this metric for records whose **city** and **country** are not null.

```
SELECT analytics.fullvisitorid, all_sessions.country, all_sessions.city , cast(AVG(CAST(units_sold AS NUMERIC)) as numeric(6,2)) as AverageQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY analytics.fullvisitorid, all_sessions.country, all_sessions.city
ORDER BY AverageQty DESC
```
Here is the screenshot of the result.

![](/pictures/Starting_with_questions_2.png)


## **Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**
#### Answer

This script generates the total quantity of items sold by product category by city and country. The metric helps to answer the question of any pattern in the items sold by city and coiuntry.

The result shows that the city of Toronto, Canada has the highest activity fo items sold, while Sydney, Australia has the least.

```
SELECT all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL AND v2ProductCategory IS NOT null
GROUP BY all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductCategory
```
Here is the screenshot of the result.

![](/pictures/Starting_with_questions_3.png)


## **Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**
#### Answer

Here we look at the distribution of products by city and country. 

Again, the result shows that the city of Toronto, Canada has the highest activity for items sold, while Sydney, Australia has the least. 

```
SELECT all_sessions.v2ProductName, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY all_sessions.v2ProductName, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductName
```
Here is the screenshot of the result.

![](/pictures/Starting_with_questions_4.png)


## **Question 5: Can we summarize the impact of revenue generated from each city/country?**
#### Answer

This script generates the global ranking of the revenue by city and country.
The result shows that Mountain View, United States has the highest gross revenue while Jersey City, United States has the least.

```
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
```
Here is the screenshot of the result.

![](/pictures/Starting_with_questions_5.png)
