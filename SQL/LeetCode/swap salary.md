## Swap Salary
[문제링크](https://leetcode.com/problems/swap-salary/)
```sql
UPDATE salary
SET sex = CASE WHEN sex = 'f' THEN 'm' ELSE 'f' END
```