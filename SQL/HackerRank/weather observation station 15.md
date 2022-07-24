## Weather Observation Station 15

[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-15)  
```sql
SELECT round(long_w, 4) FROM station
WHERE lat_n < 137.2345
ORDER BY lat_n DESC
LIMIT 1
```
___

#### MySQL 소숫점처리
- CEIL(수) : 값보다 큰 정수 중 가장 작은 정수를 구한다   
- FLOOR(수) : 값보다 작은 정수 중 가장 큰 정수를 구한다   
- ROUND(수, 자릿수)   
