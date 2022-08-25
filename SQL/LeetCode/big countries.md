## Big Countries
[문제링크](https://leetcode.com/problems/big-countries/)
```sql
SELECT name
     , population
     , area
FROM world
WHERE population >= 25000000
OR area >= 3000000
```
