## The Report
[문제링크](https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true)
```sql
SELECT CASE WHEN grade >= 8 THEN s.name END
     , g.grade
     , s.marks
FROM students s
     INNER JOIN grades g ON s.marks BETWEEN g.min_mark AND g.max_mark
ORDER BY g.grade DESC, s.name ASC, s.marks ASC
```
