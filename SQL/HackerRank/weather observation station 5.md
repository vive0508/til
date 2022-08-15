## Weather Observation Station 5
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)
```sql
SELECT city, LENGTH(city)
FROM station
ORDER BY LENGTH(city) ASC, city ASC
LIMIT 1;
SELECT city, LENGTH(city)
FROM station
ORDER BY LENGTH(city) DESC, city ASC
LIMIT 1
```
- UNION은 ORDER BY가 가장 마지막에 오기 때문에, UNION을 사용하는 쿼리문은 실행이 되지 않는다.   
- UNION을 사용하지 않고 ;(세미콜론)을 사용하면 두 쿼리문을 이어줄 수 있다.
