## 이름에 el이 들어가는 동물 찾기
[문제링크](https://school.programmers.co.kr/learn/courses/30/lessons/59047)
```sql
SELECT animal_id
     , name
FROM animal_ins
WHERE name LIKE '%el%'
AND animal_type = "Dog"
ORDER BY name
```
