## Weather Observation Station 8
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true)
```sql
SELECT DISTINCT city
FROM station
WHERE (city LIKE "a%"
       OR city LIKE "e%"
       OR city LIKE "i%"
       OR city LIKE "o%"
       OR city LIKE "u%")
AND
      (city LIKE "%a"
       OR city LIKE "%e"
       OR city LIKE "%i"
       OR city LIKE "%o"
       OR city LIKE "%u")
```
