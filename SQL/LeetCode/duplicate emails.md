## Duplicate Emails
[문제링크](https://leetcode.com/problems/duplicate-emails/submissions/)
```sql
SELECT email
FROM person
GROUP BY email
HAVING COUNT(email) >= 2
```
