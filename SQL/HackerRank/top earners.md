## Top Earners
[문제링크](https://www.hackerrank.com/challenges/earnings-of-employees/problem?h_r=internal-search)   
- 서브쿼리를 활용하지 않은 방법
```sql
SELECT months*salary AS earnings
     , COUNT(*)
FROM employee
GROUP BY earnings
ORDER BY earnings DESC
LIMIT 1
```
- 서브쿼리 활용 1 : WHERE절 사용
```sql
SELECT months * salary AS earnings
     , COUNT(*)
FROM employee
WHERE months * salary = (SELECT MAX(months*salary) FROM employee)
GROUP BY earnings
```

- 서브쿼리 활용 2 : HAVING절 사용
```SQL
SELECT months * salary AS earnings
     , COUNT(*)
FROM employee
GROUP BY earnings
HAVING earnings = (SELECT MAX(months*salary) FROM employee)
```

- 서브쿼리 활용 3 : CASE 조건문 활용
```SQL
SELECT (SELECT MAX(months * salary) FROM employee)
     , COUNT(CASE WHEN months * salary = (SELECT MAX(months * salary) FROM employee) THEN 1 END)
FROM employee
```
