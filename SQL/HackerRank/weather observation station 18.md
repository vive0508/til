## Weather Observation Station 18
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)
```sql
SELECT ROUND(ABS(MIN(lat_n)-MAX(lat_n)) + ABS(MIN(long_w)-MAX(long_w)),4)
FROM station
```
