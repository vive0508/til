Higher Than 75 Marks
===
[문제링크](https://www.hackerrank.com/challenges/more-than-75-marks)
```sql
SELECT name FROM students
WHERE marks > 75
ORDER BY RIGHT(name, 3) ASC, id ASC  
```

___
#### MySQL 문자열 자르기
- LEFT(컬럼명 또는 문자열, 문자열의 길이)
- RIGHT(컬럼명 또는 문자열, 문자열의 길이)
- SUBSTRING(컬럼명 또는 문자열, 시작 위치, 길이)
