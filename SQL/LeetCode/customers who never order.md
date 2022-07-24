### Customers Who Never Order
[문제링크](https://leetcode.com/problems/customers-who-never-order/)
```sql
SELECT name AS customers
FROM customers AS c
     LEFT JOIN orders AS o ON c.id = o.customerid  
WHERE o.customerid IS NULL
```
