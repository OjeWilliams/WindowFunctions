[Questions](https://www.windowfunctions.com/questions/over/) based on [over](https://docs.microsoft.com/en-us/sql/t-sql/queries/select-over-clause-transact-sql?view=sql-server-ver15).
### `Note This was done with a single line code block. Use ctrl + e`

[Question1](https://www.windowfunctions.com/questions/over/0): \
The cats must be ordered by name and will enter an elevator one by one. We would like to know what the running total weight is.\
Return: name, running total weight\
Order by: name

Using Window Clause

```
SELECT name,  SUM(weight) OVER (ORDER BY name) AS running_total_weight
FROM cats ;

OR
--Using Window Clause

SELECT
name, SUM(weight) OVER bat AS running_total_weight
FROM cats 
WINDOW bat AS (ORDER BY name) ;
```

<br>

[Question2](https://www.windowfunctions.com/questions/over/1): \
The cats must be ordered first by breed and second by name. They are about to enter an elevator one by one. When all the cats of the same breed have entered they leave. \
We would like to know what the running total weight of the cats is. \
Return: name, breed, running total weight \
Order by: breed, name

```
SELECT name, breed, SUM(weight) OVER (PARTITION BY breed ORDER BY name) AS running_total_weight
FROM cats ;

OR
--Using Window Clause

SELECT name, breed, SUM(weight) OVER cappy AS running_total_weight
FROM cats
WINDOW cappy AS (PARTITION BY breed ORDER BY name)
```

<br>

[Question3](https://www.windowfunctions.com/questions/over/2): \
The cats would like to see the average of the weight of them, the cat just after them and the cat just before them.
The first and last cats are content to have an average weight of consisting of 2 cats not 3. \
Return: name, weight, average_weight \
Order by: weight

```
SELECT name, weight, AVG(weight) OVER (ORDER BY weight ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS average_weight
FROM cats ;

OR
--Using Window Clause

SELECT name, weight, AVG(weight) OVER goat AS average_weight
FROM cats
WINDOW goat AS ( ORDER BY weight ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) ;
```

<br>

[Question4](https://www.windowfunctions.com/questions/over/3): \
The cats must be ordered by weight descending and will enter an elevator one by one. We would like to know what the running total weight is. \
If two cats have the same weight they must enter separately\
Return: name, running total weight \
Order by: weight desc

```
SELECT name, SUM(weight) OVER (ORDER BY weight DESC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS runnning_total_weight
FROM cats ;

OR
--Using Window Clause

SELECT name, SUM(weight) OVER horsey AS running_total_weight
FROM cats
WINDOW horsey AS ( ORDER BY weight DESC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) ;
```

