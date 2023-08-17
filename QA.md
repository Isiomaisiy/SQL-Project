## Risk Areas
- Relationships among some of the tables cannot be enforced.
  
## QA Process
### Relationships among some of the tables cannot be enforced

I observed, for example, that some of the tables in the database have product skus whose sku are not available in the **product** table.

This makes it impossible to build a relationship between those tables and the **product** table.

The script here shows that the **sales_by_sku** table has 8 different skus which cannot be found in the **product** table.

```
select distinct productsku from(
select productsku from sales_by_sku
except
select sku from products
) a
```

Here is the screensht of the result.

![](/pictures/qa/1.png)
