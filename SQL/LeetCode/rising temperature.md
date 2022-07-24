## Rising Temperature
[문제링크](https://leetcode.com/problems/rising-temperature/)
```sql
SELECT today.id
FROM weather AS today
     INNER JOIN weather AS yesterday ON DATE_ADD(yesterday.recorddate, INTERVAL 1 DAY) = today.recorddate
WHERE today.temperature > yesterday.temperature
```
