## What issues will you address by cleaning the data?

### all_sessions

Analysis on this table revealed that both the **city** and **country** fields have values which should not be in the table. In my opinion, these values should be replaced by null.

![](/pictures/cleaning_data/1.png)

![](/pictures/cleaning_data/2.png)

### analytics

Initial analysis done on this table revealed that it has duplicates.

The query used to arrive at this conclusion is shown here.

```
-- This shows the total count of the records in the queried table
select
(select count(1) from analytics) as TotalCount,
(select count(1) from 
(select distinct * from analytics) a) as TotalDistinctCount
```
The result of the query is shown here.

![](/pictures/cleaning_data/3.png)


The idea is that if there are no duplicates, both counts should return the same result. But if there are duplicates in the table, the count will differ as is the case here.


### Issues Addressed

By cleaning the **all_sessions** table to replace the unnecessary values with **null**, it becomes intuitive that the values for those columns are not available.

Also, by cleaning up the **analytics** table, we can avoid double-counting of records when we are trying to write scripts to gain insights into the data.


## Clean-up Queries
### Below, provide the SQL queries you used to clean your data.

#### all_sessions

To replace the **not available in demo dataset** and **(not set)** values in the **city** and **country** fields of the table, the folowing scripts are used.

```
-- For city
update all_sessions
set city = NULL
where city like '%not%'

-- For country
update all_sessions
set country = NULL
where country like '%not%'

```

#### analytics

The script here shows the count of records vs count of records expected after removing duplicates.

```
-- This shows the total count of the records in the queried table
select
(select count(1) from analytics) as TotalCount,
(select count(1) from 
(select distinct * from analytics) a) as TotalDistinctCount
```

The result of the query shows that we expect to have **1739308** distinct records after cleanup.

To remove the duplicates, I created a temp table called **temp_analytics**, and I loaded the distinct values of the **analytics** table into it.
This query helped me do that.

```
create table temp_analytics as
select distinct on
		(visitNumber
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
```

Then I dropped the old **analytics** table and renamed the **temp_analytics** table to **analytics**.
This script helped me to do that.

```
-- drop the old table, then rename the temp table to the old filename

drop table analytics;
alter table temp_analytics rename to analytics;
```
After cleanup, I reran the script to check for duplicates, and it now shows that there are no duplicates. The record count is equal to the expected record count.

![](/pictures/cleaning_data/4.png)
