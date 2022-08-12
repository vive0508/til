## Weather Observation Station 17

[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-17/problem?isFullScreen=true)
```sql
SELECT ROUND(long_w, 4)
FROM station
WHERE lat_n > 38.7780
ORDER BY lat_n ASC
LIMIT 1
```
