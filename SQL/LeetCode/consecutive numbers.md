## Consecutive Numbers
[문제링크](https://leetcode.com/problems/consecutive-numbers/)

```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM logs l1
     INNER JOIN logs l2 ON l2.id = l1.id + 1 
     INNER JOIN logs l3 ON l3.id = l2.id + 1
WHERE l1.num = l2.num = l3.num
```
