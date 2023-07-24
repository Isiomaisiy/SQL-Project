Question 1: find all duplicate records

SQL Queries: 

select count(1) from analytics;  --4301122

select count(1) from 
(select distinct * from analytics) a  --1739308

-------------------------------------------------------------
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

--select count(1) from cte
--where rn > 1

Answer: The analytics table has 2561814 records that are duplicates.



Question 2: find the total number of unique visitors (`fullVisitorID`)

SQL Queries:
select
count (distinct fullvisitorid)
from analytics 

Answer: 120018



Question 3: find the total number of unique visitors by referring sites

SQL Queries: 
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

Answer:
pictures\QUESTION 3.png


Question 4: find each unique product viewed by each visitor

SQL Queries: 
select
distinct fullvisitorid, v2productName
from all_sessions
order by fullvisitorid

Answer:

pictures\QUESTION_4.png



Question 5: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:

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

Answer:

pictures\QUESTION 5.png
