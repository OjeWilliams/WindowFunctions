[Questions](https://www.windowfunctions.com/questions/grouping/) based on: 
[nth_value](https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions114.htm#SQLRF30031), 
[ntile](https://docs.microsoft.com/en-us/sql/t-sql/functions/ntile-transact-sql?view=sql-server-ver15_),
[lag](https://docs.microsoft.com/en-us/sql/t-sql/functions/lag-transact-sql?view=sql-server-ver15),
[lead](https://docs.microsoft.com/en-us/sql/t-sql/functions/lead-transact-sql?view=sql-server-ver15).


[Question1](https://www.windowfunctions.com/questions/grouping/0): \
We are worried our cats are too fat and need to diet.
We would like to group the cats into quartiles by their weight. \
Return: name, weight, weight_quartile \
Order by: weight

```
SELECT name, weight, NTILE(4) OVER (order by weight) AS weight_quartile
FROM cats ;
```
\
[Question2](https://www.windowfunctions.com/questions/grouping/1): \
Cats are fickle. Each cat would like to lose weight to be the equivalent weight of the cat weighing just less than it.
Print a list of cats, their weights and the weight difference between them and the nearest lighter cat ordered by weight. \
Return: name, weight, weight_to_lose \
Order by: weight 

```
SELECT name, weight, COALESCE(weight - LAG(weight,1) OVER (ORDER BY weight),0) AS weight_to_lose
FROM cats ;
```
\
[Question3](https://www.windowfunctions.com/questions/grouping/2): \
The cats now want to lose weight according to their breed. Each cat would like to lose weight to be the equivalent weight of the cat in the same breed weighing just less than it.Print a list of cats, their breeds, weights and the weight difference between them and the nearest lighter cat of the same breed. \
Return: name, breed, weight, weight_to_lose \
Order by: weight 
```
SELECT name, breed, weight, COALESCE( weight - lag(weight,1) OVER (PARTITION BY breed ORDER BY weight),0) AS weight_to_lose
FROM cats
ORDER BY weight ;
```
\
[Question4](https://www.windowfunctions.com/questions/grouping/3): \
Cats are vain. Each cat would like to pretend it has the lowest weight for its color.
Print cat name, color and the minimum weight of cats with that color. \
Return: name, color, lowest_weight_by_color\
Order by: color, name \
`we could have used first_value() and nth_value() to achieve the same results`
```
SELECT name, color, MIN(weight) OVER (PARTITION BY COLOR ORDER BY weight) AS lowest_weight_by_color
FROM cats
ORDER BY color, name ;
```

\
[Question5](https://www.windowfunctions.com/questions/grouping/4): \
Each cat would like to see the next heaviest cat's weight when grouped by breed. If there is no heavier cat print 'fattest cat'
Print a list of cats, their weights and either the next heaviest cat's weight or 'fattest cat'.\
Return: name, weight, breed, next_heaviest \
Order by: weight 
```
SELECT name, weight, breed, COALESCE( CAST(LEAD(weight,1) OVER (PARTITION BY breed ORDER BY weight) AS varchar), 'fattest cat') AS next_heaviest
FROM cats
ORDER BY weight ;
```

\
[Question6](https://www.windowfunctions.com/questions/grouping/5): \
The cats have decided the correct weight is the same as the 4th lightest cat. All cats shall have this weight. Except in a fit of jealous rage they decide to set the weight of the lightest three to 99.9
Print a list of cats, their weights and their imagined weight\

```
SELECT name, weight, COALESCE( NTH_VALUE(weight,4) OVER (ORDER BY weight),99.9) AS imagined_weight
FROM cats ;
```

\
[Question7](https://www.windowfunctions.com/questions/grouping/6): \
The cats want to show their weight by breed. The cats agree that they should show the second lightest cat's weight (so as not to make other cats feel bad)
Print a list of breeds, and the second lightest weight of that breed \
Return: breed, imagined_weight \
Order by: breed

```
SELECT DISTINCT breed, NTH_VALUE(weight,2) OVER (PARTITION BY breed ORDER BY weight RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS imagined_weight
FROM cats 
ORDER BY breed;
```
