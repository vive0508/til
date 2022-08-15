## Type of Triangle
[문제링크](https://www.hackerrank.com/challenges/what-type-of-triangle/problem?h_r=internal-search)
```sql
SELECT CASE
            WHEN (a+b<=c) OR (b+c<=a) OR (a+c<=b) THEN 'Not A Triangle'
            WHEN a=b AND b=c THEN 'Equilateral'
            WHEN (a=b AND b!=c) OR (b=c AND c!=a) OR (a=c AND b!=c) THEN 'Isosceles'
            ELSE 'Scalene'
       END
FROM triangles
```
