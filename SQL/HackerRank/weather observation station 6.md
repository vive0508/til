## Weather Observation Station 6
[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true)
- 풀이방법 1
```sql
SELECT DISTINCT city FROM station
WHERE city LIKE 'i%'
OR city LIKE 'e%'
OR city LIKE 'a%'
OR city LIKE 'o%'
OR city LIKE 'u%'
```
- 풀이 방법 2
```sql
SELECT DISTINCT city
FROM station
WHERE city REGEXP '^[aeiou].*'
```
