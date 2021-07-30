[Questions](https://www.windowfunctions.com/questions/over/) based on [over](https://docs.microsoft.com/en-us/sql/t-sql/queries/select-over-clause-transact-sql?view=sql-server-ver15).

[Question1](https://www.windowfunctions.com/questions/over/0):
The cats must be ordered by name and will enter an elevator one by one. We would like to know what the running total weight is.\
Return: name, running total weight\
Order by: name

```
SELECT name,  SUM(weight) OVER (ORDER BY name) AS running_total_weight
FROM cats
;
```

<br>

[Question2](https://www.windowfunctions.com/questions/over/1):
The cats must be ordered first by breed and second by name. They are about to enter an elevator one by one. When all the cats of the same breed have entered they leave. \
We would like to know what the running total weight of the cats is. \
Return: name, breed, running total weight
Order by: breed, name

```

```
