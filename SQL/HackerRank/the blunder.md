## The Blunder
[문제링크](https://www.hackerrank.com/challenges/the-blunder/problem?isFullScreen=true)
```sql
SELECT CEIL((SUM(salary)/COUNT(*))-(SUM(REPLACE(salary, 0, ''))/COUNT(*)))
FROM employees
```
