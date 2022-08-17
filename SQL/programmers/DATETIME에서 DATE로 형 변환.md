## DATETIME에서 DATE로 형 변환
[문제링크](https://school.programmers.co.kr/learn/courses/30/lessons/59414)
```sql
SELECT animal_id
     , name
     , DATE_FORMAT(datetime, '%Y-%m-%d') AS 날짜
FROM animal_ins
```
