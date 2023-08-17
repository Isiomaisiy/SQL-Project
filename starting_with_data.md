## Question 1: find all duplicate records

#### Answer
This query returns the count of duplicate records in the **analytics** table.

```
-- This shows the total count of the records in the queried table
select
(select count(1) from analytics) as TotalCount,
(select count(1) from 
(select distinct * from analytics) a) as TotalDistinctCount
```

This query however gives the actual records that are duplicated.

```
with cte as (
select 
*,
row_number() over(partition by visitNumber
				,visitId
				,visitStartTime
				,analytics_date
				,fullvisitorId
				,userid
				,channelGrouping
				,socialEngagementType
				,units_sold
				,pageviews
				,timeonsite
				,bounces
				,revenue
				,unit_price) as rn
from analytics
)

select count(1) from cte
where rn > 1
```

## Question 2: find the total number of unique visitors (`fullVisitorID`)

#### Answer

```
select
count (distinct fullvisitorid)
from analytics
```

The screenshot of the result is seen here.

![](/pictures/swd/1.png)

## Question 3: find the total number of unique visitors by referring sites

The assumption I made here is that visitors who have a **channelGrouping** of **Referal** are the ones in question.

#### Answer
```
with cte as
(
select distinct
s.pageTitle, 
s.fullvisitorid
from all_sessions s
where s.channelGrouping = 'Referral'
)
select
pageTitle, count(fullvisitorid) as NumUniqueVisitors
from cte
group by pageTitle
order by NumUniqueVisitors desc
```
The screenshot of the result is shown here.

![](/pictures/QUESTION_3.png)


## Question 4: find each unique product viewed by each visitor

#### Answer
```
select
distinct fullvisitorid, v2productName
from all_sessions
order by fullvisitorid
```
The screenshot of the result is shown here.

![](/pictures/QUESTION_4.png)


## Question 5: compute the percentage of visitors to the site that actually makes a purchase

####
```
with uniqueviewvisitors as
(select 
	count(distinct fullvisitorid) as count_viewvisitors
from all_sessions),
uniquepurchasevisitors as
(select
	count(distinct a.fullvisitorid) as count_purchasevisitors
from all_sessions s
inner join analytics a on s.fullvisitorid = a.fullvisitorid)

select
	(select count_viewvisitors from uniqueviewvisitors) as TotalViewVisitors,
	(select count_purchasevisitors from uniquepurchasevisitors) as TotalPurchaseVisitors,
	--(select cast(count_purchasevisitors as numeric) from uniquepurchasevisitors)/(select cast(count_viewvisitors as numeric) from uniqueviewvisitors)*100
	round(((select cast(count_purchasevisitors as numeric) from uniquepurchasevisitors)/(select cast(count_viewvisitors as numeric) from uniqueviewvisitors))::numeric,3)*100 as PctPurchaseVisitors
```
The result of the screenshot is shown here.

![](/pictures/QUESTION_5.png)
