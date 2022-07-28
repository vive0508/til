## Delete Duplicate Emails
[문제링크](https://leetcode.com/problems/delete-duplicate-emails/)
```sql
DELETE FROM person
WHERE id NOT IN(
    SELECT sub.min_id
    FROM(
        SELECT email, MIN(id) AS min_id
        FROM person
        GROUP BY email
        ) sub)
```
