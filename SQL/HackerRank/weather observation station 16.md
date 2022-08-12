## Weather Observation Station 16
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-16/problem?isFullScreen=true)
```sql
SELECT ROUND(lat_n, 4)
FROM station
WHERE lat_n > 38.7780
ORDER BY lat_n ASC
LIMIT 1
```
