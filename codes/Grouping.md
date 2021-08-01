[Questions](https://www.windowfunctions.com/questions/grouping/) based on: \
[nth_value](https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions114.htm#SQLRF30031), 
[ntile](https://docs.microsoft.com/en-us/sql/t-sql/functions/ntile-transact-sql?view=sql-server-ver15_),
[lag](https://docs.microsoft.com/en-us/sql/t-sql/functions/lag-transact-sql?view=sql-server-ver15),
[lead](https://docs.microsoft.com/en-us/sql/t-sql/functions/lead-transact-sql?view=sql-server-ver15).

<br>
[Question1](https://www.windowfunctions.com/questions/grouping/0): \
We are worried our cats are too fat and need to diet.
We would like to group the cats into quartiles by their weight. \
Return: name, weight, weight_quartile \
Order by: weight

<br>
```
SELECT name, weight, NTILE(4) OVER (order by weight) AS weight_quartile
FROM cats ;
```
