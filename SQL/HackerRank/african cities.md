African Cities
===
[문제링크](https://www.hackerrank.com/challenges/african-cities/problem?h_r=internal-search&isFullScreen=true)
```sql
SELECT city.name
FROM city
     INNER JOIN country ON city.countrycode =  country.code
WHERE country.continent = "Africa"
```
