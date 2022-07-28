## Delete Duplicate Emails
[문제링크](https://leetcode.com/problems/delete-duplicate-emails/)
- DELETE with 서브쿼리    
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
- DELETE with INNER JOIN   
```sql
DELETE p1
FROM person p1
     INNER JOIN person p2 ON p1.email = p2.email
WHERE p1.id > p2.id     
```
