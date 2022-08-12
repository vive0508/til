## Weather Observation Station 11
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-11/problem?isFullScreen=true)
```sql
SELECT DISTINCT city
FROM station
WHERE (city NOT LIKE 'a%'
       AND city NOT LIKE 'e%'
       AND city NOT LIKE 'i%'
       AND city NOT LIKE 'o%'
       AND city NOT LIKE 'u%')
OR
      (city NOT LIKE '%a'
       AND city NOT LIKE '%e'
       AND city NOT LIKE '%i'
       AND city NOT LIKE '%o'
       AND city NOT LIKE '%u')
```
