The refresher/intro is found [here](https://www.windowfunctions.com/questions/intro/), and the questions [here](https://www.windowfunctions.com/questions/intro/0).

### Question: <br>
We would like to find the total weight of cats grouped by age. But only return those groups with a total weight larger than 12. \
Return: age, sum(weight) Order by: age

```
SELECT age, SUM(weight) AS total_weight FROM cats
GROUP BY age HAVING SUM(weight) > 12
ORDER BY age ;
```
