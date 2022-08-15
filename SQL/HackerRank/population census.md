## Population Census
[문제링크](https://www.hackerrank.com/challenges/asian-population)
```sql
SELECT SUM(city.population)
FROM city
     INNER JOIN country ON city.countrycode = country.code
WHERE country.continent = "Asia"
```
