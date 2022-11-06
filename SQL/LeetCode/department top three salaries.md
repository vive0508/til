## Department Top Three Salaries
[문제링크](https://leetcode.com/problems/department-top-three-salaries/description/)

```sql
WITH salary_rank AS(
    SELECT d.name AS department
        , e.name AS employee
        , e.salary
        , DENSE_RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC) AS dr
    FROM employee e
        INNER JOIN department d ON e.departmentId = d.id
)

SELECT department, employee, salary
FROM salary_rank
WHERE dr <= 3
```
