## Type of Triangle
[문제링크](https://www.hackerrank.com/challenges/what-type-of-triangle/problem?h_r=internal-search)
```sql
SELECT CASE
            WHEN a=b AND b=c THEN 'Equilateral'
            WHEN a+b<=c OR a+c<=b OR b+c<=a THEN 'Not A Triangle'
            WHEN a=b OR b=c OR a=c THEN 'Isosceles'
            ELSE 'Scalene'
       END
FROM triangles
```
