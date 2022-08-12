## Higher Than 75 Marks
[문제링크](https://www.hackerrank.com/challenges/more-than-75-marks)
```sql
SELECT name
FROM students
WHERE marks > 75
ORDER BY RIGHT(NAME, 3) ASC, id ASC 
```
