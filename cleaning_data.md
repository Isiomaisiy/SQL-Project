What issues will you address by cleaning the data?

The all_sessions and analytics tables has duplicates which can cause a bias in the results of my qury.
Removing the duplicates was addressed by cleaning the data 


Queries:
Below, provide the SQL queries you used to clean your data.

--This qury was used to get total rows in the table before cleaning.
select count(1) from analytics  --4301122


--This qury was used to get the total number of distinct rolls expected after cleaning.
select count(1) from 
(select distinct * from analytics) a  --1739308

--This qury was used to get the number of duplicates in the table
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

The analytics table has 2561814 records that are duplicates.

--The below qury was used to create a new table of distinct values,

create table temp_analytics as
select distinct on (visitNumber
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
					,unit_price) *
from analytics

-- drop the old table, then rename the temp table to the old filename

drop table analytics;
alter table temp_analytics rename to analytics;



--script to identify dulicates in all_sessions table


with cte as (
select 
*,
row_number() over(partition by fullVisitorId
,channelGrouping
,time
,country
,city
,totalTransactionRevenue
,transactions
,timeOnSite
,pageviews
,sessionQualityDim
,date
,visitId
,type
,productRefundAmount
,productQuantity
,productPrice
,productRevenue
,productSKU
,v2ProductName
,v2ProductCategory
,productVariant
,currencyCode
,itemQuantity
,itemRevenue
,transactionRevenue
,transactionId
,pageTitle
,searchKeyword
,pagePathLevel1
,eCommerceAction_type
,eCommerceAction_step
,eCommerceAction_option) as rn
from all_sessions
)

-- select count(1) from cte
-- where rn > 1

create table temp_all_sessions as
select distinct on (fullVisitorId
,channelGrouping
,time
,country
,city
,totalTransactionRevenue
,transactions
,timeOnSite
,pageviews
,sessionQualityDim
,date
,visitId
,type
,productRefundAmount
,productQuantity
,productPrice
,productRevenue
,productSKU
,v2ProductName
,v2ProductCategory
,productVariant
,currencyCode
,itemQuantity
,itemRevenue
,transactionRevenue
,transactionId
,pageTitle
,searchKeyword
,pagePathLevel1
,eCommerceAction_type
,eCommerceAction_step
,eCommerceAction_option) *
from all_sessions

-- drop the old table, then rename the temp table to the old filename

drop table all_sessions;
alter table temp_all_sessions rename to all_sessions;