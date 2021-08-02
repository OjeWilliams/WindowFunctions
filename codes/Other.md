[Questions](https://www.windowfunctions.com/questions/other/) based on: 
[window](http://dcx.sap.com/1200/en/dbreference/window-statement.html), 
[array_agg](https://docs.snowflake.com/en/sql-reference/functions/array_agg.html),
[filter](https://modern-sql.com/feature/filter).

\
[Question1](https://www.windowfunctions.com/questions/other/0): \
This SQL function can be made simpler by using the WINDOW statement. Please try and use the WINDOW clause.
Each cat would like to see what half, third and quartile they are in for their weight.\
Return: name, weight, by_half, thirds, quartile \
Order by: weight

```
-- This was how I thought about it first
SELECT name, weight, NTILE(2) OVER (ORDER BY WEIGHT) AS by_half,  NTILE(3) OVER (ORDER BY WEIGHT) AS thirds,  NTILE(4) OVER (ORDER BY WEIGHT) AS quart
FROM cats ;

-- This was implemented using window functions
SELECT name, weight, NTILE(2) OVER NTILE_WIN AS by_half,  NTILE(3) OVER NTILE_WIN AS thirds,  NTILE(4) OVER NTILE_WIN AS quart
FROM cats
WINDOW NTILE_WIN AS (ORDER BY weight) ;
```



