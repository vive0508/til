## Not Boring Movies
[문제링크](https://leetcode.com/problems/not-boring-movies/)
```sql
SELECT *
FROM cinema
WHERE id%2 != 0
AND description != 'boring'
ORDER BY rating DESC
```
