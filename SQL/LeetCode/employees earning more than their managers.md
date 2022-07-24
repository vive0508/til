## Employees Earning More Than Their Managers
[문제링크](https://leetcode.com/problems/employees-earning-more-than-their-managers/)
```sql
SELECT employee.name AS Employee
FROM employee
     INNER JOIN employee AS Manager ON employee.managerid = Manager.id
WHERE employee.salary > manager.salary
```
