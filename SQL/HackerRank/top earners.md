## Top Earners
[문제링크](https://www.hackerrank.com/challenges/earnings-of-employees/problem?h_r=internal-search)
```sql
SELECT months*salary AS earnings
     , COUNT(*)
FROM employee
GROUP BY earnings
ORDER BY earnings DESC
LIMIT 1
```
