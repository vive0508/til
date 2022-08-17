## NULL 처리하기
[문제링크](https://school.programmers.co.kr/learn/courses/30/lessons/59410)
```sql
SELECT animal_type
     , CASE
            WHEN name IS NULL THEN "No name" 
            ELSE name
       END AS name
     , sex_upon_intake
FROM animal_ins
```
