[Questions](https://www.windowfunctions.com/questions/ranking/) based on: \
[rank](https://docs.microsoft.com/en-us/sql/t-sql/functions/rank-transact-sql?view=sql-server-ver15),
[row number](https://docs.microsoft.com/en-us/sql/t-sql/functions/rank-transact-sql?view=sql-server-ver15),
[dense rank](https://docs.microsoft.com/en-us/sql/t-sql/functions/dense-rank-transact-sql?view=sql-server-ver15),
[cumulative distribution](https://docs.microsoft.com/en-us/sql/t-sql/functions/cume-dist-transact-sql?view=sql-server-ver15),
[percent rank](https://docs.microsoft.com/en-us/sql/t-sql/functions/percent-rank-transact-sql?view=sql-server-ver15).

[Question1](https://www.windowfunctions.com/questions/ranking/0): \
The cats form a line grouped by color. Inside each color group the cats order themselves by name. Every cat must have a unique number for its place in the line.
We must assign each cat a unique number while maintaining their color & name ordering. \
Return: unique_number, name, color

```
SELECT ROW_NUMBER() OVER ( ORDER BY color, name ) AS unique_number, name, color
FROM cats 
;
```
<br>

[Question2](https://www.windowfunctions.com/questions/ranking/1): \
We would like to find the fattest cat. Order all our cats by weight.
The two heaviest cats should both be 1st. The next heaviest should be 3rd. \
Return: ranking, weight, name \
Order by: ranking, name

```
SELECT RANK() OVER (ORDER BY weight DESC) AS ranking, weight, name
FROM cats
ORDER BY ranking, name ; 
```

<br>

[Question3](https://www.windowfunctions.com/questions/ranking/2): \
For cats age means seniority, we would like to rank the cats by age (oldest first).
However we would like their ranking to be sequentially increasing. \
Return: ranking, name, age \
Order by: ranking, name

```
SELECT DENSE_RANK() OVER (ORDER BY age DESC) AS r, name, age
FROM cats
ORDER BY r ,name ;
```
