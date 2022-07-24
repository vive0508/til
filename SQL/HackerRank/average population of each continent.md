## Average Population of Each Continent
[문제링크](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?h_r=internal-search)
```sql
SELECT country.continent
     , FLOOR(AVG(city.population))
FROM city
     INNER JOIN country ON city.countrycode = country.code
GROUP BY country.continent
```
