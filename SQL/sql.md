SQL  
=== 

## 1. 기초개념
### 1.1 용어 정리
- 데이터
```
컴퓨터 안에 기록되어 있는 숫자
```

- 데이터베이스 (database, DB)
```
데이터의 집합으로 하드디스크나 플래시메모리 같은 비휘발성 저장장치에 저장됩니다.
단지 저장에 그치지 않고 용이한 검색을 실현하도록 정리해줍니다.
```
- DBMS (Database Management System)
```
데이터베이스를 관리하는 소프트웨어입니다.
```
- 관계형 데이터베이스 관리 소프트웨어 시스템(RDBMS)
```
관계형 데이터베이스는 데이터베이스를 관계형 모델로 관리하는 소프트웨어를 의미합니다.
RDBMS의 종류에는 Oracle, DB2, SQL Server, PostgreSQL, MySQL, SQLite 등이 있습니다.
(cf. 계층형 데이터베이스, 객체지향 데이터베이스, XML 데이터베이스, 키-밸류 스토어(KVS) 등)
```
- SQL (Structured Query Lanagauge)
```
RDBMS에서 데이터를 조작하는 명령입니다.
데이터베이스의 종류에 따라 표준과 다른 SQL 명령을 사용하기도 합니다.(SQL 방언)
```
- 데이터베이스 서버
```
RDBMS는 클라이언트/서버 모델로 구성됩니다.
클라이언트는 데이터베이스 서버에 접속해 SQL 명령을 실행하여 데이터베이스를 조작할 수 있습니다.
```

### 1.2 ERD (entity relationship diagram)
- 구성요소([참고링크](https://www.lucidchart.com/pages/er-diagrams#section_5))
  - entity : 개체, 테이블   
  - attribute : 컬럼명, 데이터타입(Primary key, Foreign Key)   
  - relationship : one to one, one to many, many to many

- 데이터의 관계
  - 데이터의 관계는 Primary key(pk)와 Foreign key(FK)의 연결을 통해 만들어진다.    
  - PK는 레코드를 대표하는 값으로, 변하지 않고 중복되지 않은 컬럼이 존재해야 한다.   
  - PK는 보통 id 컬럼으로 명명되고, 보통 DB에 의해 자동 생성된다.     
  - FK는 관계 형성을 위한 key로 pk를 참조한다.   
  - 데이터의 관계는 one to one, one to many, many to many 으로 나타낼 수 있다.

### 1.3 Data Type
- 숫자형   
  - 정수 : tinyint(), sallint(), mediumint(), int(), bigint()     
  - 실수 : demical(), double(), float()   
- 문자형   
  - varchar() : various character의 약자   
  - char() : 글자수가 일정한 문자
- 날짜, 시간형
  - date()   
  - datetime()   
  - timestamp() = datetime() + timezone   
  - 문자형을 날짜, 시간형으로 바꾸기 위해서는 `str_to_date()` 함수를 사용한다.
---

## 2. SQL 명령어
- 데이터베이스 목록 조회 : SHOW DATABASES;       
- 데이터베이스 접근 : USE databasename;      
- 테이블 목록 조회 : SHOW TABLES;   
- 테이블 세부정보 조회 : DESC tablename;   
- 주석처리 : '--' or '/* */'   

---

### 2.1 데이터 정의 언어 (DDL : Data Definition Lanaguage)
> CREAT(테이블 생성) / ALTER(테이블 변경) / DROP(테이블 삭제)
- CREATE : 테이블 생성   
```sql
# 데이터베이스 생성
CREATE DATABASE databasename;

# 데이터베이스 생성 및 기본 자료형 설정
CREATE DATABASE databasename DEFAULT CHARACTER SET utf8mb4;

# 테이블 생성
CREATE TABLE tablename
(
 columnname datatype,
 columnname datatype,
 ...
)

# 테이블 생성 조건
CREATE TABLE tablename
(
 columnname datatype NOT NULL AUTO_INCREMENT PRIMATY KEY,  
 columnname datatype NOT NULL DEFAULT '', 
 ...
)
```
- ALTER : 테이블 변경   
```sql
# 테이블 변경(필수)
ALTER TABLE tablename;

# 테이블 이름 변경
RENAME new_tablename;

# 컬럼 데이터타입 변경
MODIFY COLUMN columnname datatype;

# 컬럼명 변경 (feat. 데이터타입 변경)
CHANGE COLUMN old_columnname new_columnname new_datatype;

# 컬럼 생성
ADD COLUMN columnname datatype;
```
- DROP : 테이블 삭제   
```sql
# 데이터베이스 삭제
DROP DATABASE databasename;

# 테이블 삭제
DROP TABLE tablename;

# 컬럼 삭제
ALTER TABLE tablename
DROP COLUMN columnname;
```

___

### 2.2 데이터 조작 언어 (DML : Data Manipulation Language)
> 데이터의 검색 : SELECT(질의)   
> 데이터의 갱신 : INSERT(추가) / UPDATE(수정) / DELETE(제거)  

- SELECT : Read     
> **순서 익히기**   
> 1. SELECT
> 2. FROM   
> 3. INNER JOIN ~~ ON ~~ / UNION  
> 4. WHERE   
> 5. GROUP BY ~~ HAVING ~~   
> 6. ORDER BY   
> 7. LIMIT
```sql
# 테이블 전체내용 조회
SELECT *
FROM tablename;

# 테이블 특정 컬럼 조회
SELECT column1
     , column2
     , ...
FROM tablename;
```

- INSERT : Create   
```sql
# 컬럼 리스트와 밸류 리스트의 순서가 일치하도록 주의
INSERT INTO tablename (column1, column2, ...)
VALUES (value1, value2, ...);

# 모든 컬럼에 밸류를 입력하는 경우 컬럼 이름을 지정하지 않아도 됨
INSERT INTO tablename
VALUES (value1, value2, ...);
```

- UPDATE : Update    
```sql
UPDATE tablename
SET column1 = value1, colum2=value2, ...
WHERE condition;

# example 1
UPDATE tablename
SET columnA = comlumnA + 100
WHERE condition;

# example 2 (with CASE 구문)
UPDATE tablename
SET coulumnname = CASE
                      WHEN condition1 then value_if_condition1_true
                      WHEN condition2 then value_if_condition2_true
                  ELSE value_other_case
                  END
WHERE condition;
```

- DELETE : Delete    
```sql
# 테이블에 데이터 전체 삭제
DELETE FROM tablename;

# 조건에 부합하는 특정 행만 삭제
DELETE FROM tablename
WHERE condition;

# DELETE에 JOIN 활용
DELETE T1, T2
FROM T1
INNER JOIN T2 ON T1.key = T2.key
WHERE condition;
```
___

### 2.3 데이터 제어 언어 (DCL : Data Control Language)   
- 유저 생성 및 삭제
```sql
# 현재 PC에서 접속이 가능한 유저 생성 (ex. 패스워드 1234)
CREATE USER 'test_1'@'localhost' identified by '1234';

# 외부에서 접속이 가능한 유저 생성 (ex. 패스워드 1234)
CREATE USER 'test_2'@'%' identified by '1234';

# 현재 PC에서 접속이 가능한 유저 삭제
DROP USER 'test_1'@'localhost';

# 외부에서 접속이 가능한 유저 삭제
DROP USER 'test_2'@'%';
```
- 유저에게 부여된 권한 조회
```sql
SHOW GRANTS FOR 'username'@'localhost';
SHOW GRANTS FOR 'username'@'%';
```

- GRANT : 권한 부여
```sql
GRANT ALL ON dbname.* to 'username'@'localhost';
GRANT ALL ON dbname.* to 'username'@'%';
```

- REVOKE : 권한 해제   
```sql
REVOKE ALL ON dbname.* from 'username'@'localhost';
REVOKE ALL ON dbname.* from 'username'@'%';
```
___
# 3. SELECT   
> 3.1 SELECT ~ FROM ~     
> 3.2 INNER JOIN ~~ ON ~~ / UNION     
> 3.3 WHERE      
> 3.4 GROUP BY ~~ HAVING ~~      
> 3.5 ORDER BY      
> 3.6 LIMIT   


## 3.1 SELECT ~ FROM ~
### 3.1.1 AS / DISTINCT / CONCAT 
- AS(ALIAS)
```sql
# MySQL에서는 SELECT문에서 정의한 alias를 GROUP BY, HAVING, ORDER BY절에서 사용할 수 있다.   
# as는 생략 가능하다
-- 컬럼명 별칭 생성
SELECT column1 as newcolumnname, ... FROM tablename;

-- 테이블명 별칭 생성
SELECT column1, column2, ... FROM tablename as newtablename;
```
- DISTINCT
```python
-- 검색한 결과의 중복 제거
SELECT DISTINCT column1, column2, ...
FROM tablename
WHERE condition;

-- 집계함수와 함께 사용
SELECT COUNT (DISTINCT columnname)
FROM tablename
WHERE condition;
```
- CONCAT
```sql
SELECT CONCAT('stringA', ' ', 'stringB', ...); # stringA stringB
SELECT CONCAT('정답 :', colmname) FROM tablename; # 정답: ooo
```

### 3.1.2 조건문 (CASE문, IF문, COALESCE 피봇테이블)
- CASE
```sql
-- ELSE 이후의 값을 입력하지 않으면 NULL이 기본값으로 들어간다.
SELECT CASE
            WHEN condition1 THEN result1
            WHEN condition2 THEN result2
            ...
            ELSE result3
       END
FROM tablename

-- 조건에 NULL을 사용할 때
SELECT CASE
            WHEN a = 1 THEN A
            WHEN a = 2 THEN B
            WHEN a IS NULL THEN '데이터 없음'
            ELSE '미지정'
       END
FROM tablename

            
```   
- IF
```sql
SELECT IF(조건, 조건이 True일 때, 조건이 false일 때)
FROM tablename
```
- COALESCE
```
-- a가 NULL이 아니면 a, NULL이면 0으로 반환
SELECT a
     , COALESCE(a, 0)
FROM tablename
```

- 피봇테이블 사용 : [관련문제](https://github.com/vive0508/TIL/blob/main/SQL/LeetCode/reformat%20department%20table.md)    
```sql
# 기존 테이블을
id avg 
1  3.5
2  7.0

# 아래와 같이 피봇테이블을 만드는 방법은
id1_avg  id2_avg
3.5        7.0

# 다음의 쿼리문을 활용하면 된다.
SELECT CASE WHEN id=1 THEN avg END AS id1_avg
     , CASE WHEN id=1 THEN avg END AS id2_avg
FROM tablename
```

---

> 3.1 SELECT ~ FROM ~     
> 3.2 INNER JOIN ~~ ON ~~ / UNION or UNION ALL    
> 3.3 WHERE      
> 3.4 GROUP BY ~~ HAVING ~~      
> 3.5 ORDER BY      
> 3.6 LIMIT   

### 3.2 INNER JOIN ~~ ON ~~
- INNER JOIN : 교집합   
- LEFT JOIN : 왼쪽 데이터 기준으로 JOIN   
- RIGHT JOIN : 오른쪽 데이터 기준으로 JOIN
```sql
SELECT tableA.column1, tableA.column2, ...,  tableB.column1, tableB.column2 ...
FROM tableA
INNER JOIN | LEFT JOIN | RIGHT JOIN | FULL OUTER JOIN tableB  # FULL OUTER JOIN 제외
ON tableA.column = tableB.column # 기준 설정
WHERE condition;
```

- SELF JOIN : 한 테이블을 자기 자신에 같다 붙이는 방법   
```sql
SELECT columnname
FROM tablename
     INNER JOIN tablename AS new_tablename ON tablename.columnA = newtablename.columnB
WHERE condition;
```
   
- FULL OUTER JOIN : 합집합   
```sql
# MySQL에서는 FULL OUTER JOIN을 지원하지 않아 하기의 코드로 대체
SELECT tableA.column1, tableA.column2, ...,  tableB.column1, tableB.column2 ...
FROM tableA
LEFT JOIN tableB  
ON tableA.column = tableB.column
UNION
SELECT tableA.column1, tableA.column2, ...,  tableB.column1, tableB.column2 ...
FROM tableA
RIGHT JOIN tableB  
ON tableA.column = tableB.column;
```

### UNION / UNION ALL
- UNION / UNION ALL
  - UNION : 중복된 값을 제거하고 알려준다
  - UNION ALL : 중복된 값도 모두 보여준다
```sql
-- SQL문을 합치는 방법 (컬럼의 갯수가 같아야 한다)
SELECT column1, column2, ... FROM tableA
UNION | UNION ALL
SELECT column1, column2, ... FROM tableB
ORDER BY columname;
```

> 3.1 SELECT ~ FROM ~     
> 3.2 INNER JOIN ~~ ON ~~ / UNION     
> 3.3 WHERE      
> 3.4 GROUP BY ~~ HAVING ~~      
> 3.5 ORDER BY      
> 3.6 LIMIT   

## 3.3 WHERE
- WHERE 조건
```sql
SELECT column1, colum2, ...
FROM tablename
WHERE condition;
```
### 3.3.1 IS NULL / IS NOT NULL
- NULL, NaN (Not a Number) : 숫자도 문자도 아니고 비어있는 값이다
```sql
# NULL값 조회
SELECT *
FROM tablename
WHERE columnname IS NULL;

# NULL이 아닌 값을 조회
SELECT *
FROM tablename
WHERE columnname IS NOT NULL;

# NULL 값의 연산
C나 PHP언어에서는 NULL이 0으로 처리되지만
SQL에서는 NULL값이 0으로 처리되지 않아 연산을 해도 NULL이 된다.
```

### 3.3.2 연산자
#### 3.3.2.1 비교 연산자

| 비교 연산자 | 논리 연산자 |
| :--: | :-- |
| A=B | A와 B가 같다 |
| A>B | A가 B보다 크다 (초과) |
| A<B | A가 B보다 작다 (미만) |
| A>=B | A가 B보다 크거나 같다 (이상) |
| A<=B | A가 B보다 작거나 같다 (이하) |
| A<>B | A가 B보다 크거나 작다 (같지 않다) |
| A!=B | A와 B가 같지 않다 |

#### 3.3.2.2 논리 연산자

| 연산자 | 의미 |
| :--: | :-- |
| AND | 두 조건을 모두 만족하면 TRUE |
| OR | 두 조건 중 하나라도 만족하면 TRUE |
| NOT | 조건을 만족하지 않으면 TRUE |
| BETWEEN | 조건이 범위안에 있으면 TRUE |
| IN | 조건이 목록에 있으면 TRUE |
| LIKE | 조건이 패턴에 맞으면 TRUE |

- AND vs BETWEEN
```sql
# AND
SELECT * FROM Customers
WHERE customerID >= 3 AND customerID <=5

# BETWEEN
SELECT * FROM Customers
WHERE customerID BETWEEN 3 AND 5
```
- OR vs IN 
```sql
# OR
SELECT * FROM customers
WHERE country = 'Germany' OR country = 'France'

# IN
-- 구문이 길어질 경우에는 IN을 활용
SELECT * FROM customers
WHERE country IN ('Germany', 'France')
```

- LIKE
```sql
-- 아래와 같이 패턴으로 찾을 경우에는 LIKE를 사용하지만
-- 원하는 문자가 명확하게 있을 경우에는 비교연산자(=)를 사용하는 것이 속도가 빠르다
-- '%'나 '_'와 같은 예약어로 인식하지 않게 하기 위해서는 이스케이프('\')사용
-- not과 같이 사용할 경우에는 LIKE앞에 NOT을 붙인다(NOT LIKE)

SELECT * FROM tablename
# a로 시작하는 경우
WHERE columnname LIKE 'a%';

# a로 끝나는 경우
WHERE columnname LIKE '%a';

# a가 포함된 경우
WHERE columnname LIKE '%a%';

# a가 두번째에 글자에 포함될 경우
WHERE columnname LIKE '_a%';

# a로 시작하고 최소 두글자 이상인 경우
WHERE columnname LIKE 'a_%';

# a로 시작하고 b로 끝나는 경우
WHERE columnname LIKE 'a%b';

# 요소가 2개 이상인 경우
WHERE columnname LIKE '%,%';
```
___

> 3.1 SELECT ~ FROM ~     
> 3.2 INNER JOIN ~~ ON ~~    
> 3.3 WHERE      
> 3.4 GROUP BY ~~ HAVING ~~      
> 3.5 ORDER BY      
> 3.6 LIMIT   

## 3.4 GROUP BY ~~ HAVING ~~  

### 3.4.1 Aggregate Function (집계함수)
| Function | Description |
| :--: | :-- |
| COUNT | 총 갯수를 계산해주는 함수 |
| SUM | 합계를 계산해주는 함수 |
| AVG | 평균을 계산해주는 함수 |
| MIN | 가장 작은 값을 찾아주는 함수 |
| MAX | 가장 큰 값을 찾아주는 함수 |
| FIRST | 첫번째 결과값을 리턴하는 함수 |
| LAST | 마지막 결과값을 리턴하는 함수 |

```sql
/*SELECT Aggregate_Functions(column)
FROM tablename
WHERE condition;*/

# COUNT
-- 테이블 안에 있는 모든 행(데이터 레코드)의 갯수를 센다.
SELECT COUNT(*)
FROM tablename

-- 컬럼에 Null값을 빼고 갯수를 센다.
SELECT COUNT(columnname)
FROM tablename

-- 컬럼의 Null, 중복값을 빼고 갯수를 센다.
SELECT COUNT(DISTINCT coulumnname)
FROM tablename

# AVG
-- AVG 함수에서는 Null값을 무시한다. 그래서 총합을 null을 제외한 값의 수로 나눈다.
SELECT AVG(columnname)
FROM tablename

-- Null을 무시하지 않고, 0으로 취급해서 계산을 해주기 위해서는 하기의 방법을 사용한다. 
SELECT SUM(columnname)/COUNT(*)
FROME tablename
```

### 3.4.2 GROUP BY
```sql
-- 집계함수와 함께 사용할 수 있다.
SELECT colunm1, colunm2, ...
FROM table
WHERE condition
GROUP BY colunm1, colunm2, ... # DISTINCT와 함께 사용 가능
ORDER BY colunm1, colunm2, ...; # DISTINCT와 함께 사용하는 경우 ORDER BY 불가능
```

### 3.4.3 HAVING
```sql
- WHERE는 GROUP BY를 사용하기 전에 필터링을 할 경우에 사용한다
- HAVING은 GROUP BY를 사용한 후에 필터링을 할 경우에 사용한다.
- 조건에 집계함수가 포함되는 경우 WHERE 대신 HAVING 사용

SELECT colunm1, colunm2, ... # as(alias)를 사용한 후
FROM table
WHERE condition
GROUP BY colunm1, colunm2, ... 
HAVING condition (Aggregate_Functions) # alias로 조건을 활용할 수 있다
ORDER BY colunm1, colunm2, ...; 
```
___

> 3.1 SELECT ~ FROM ~     
> 3.2 INNER JOIN ~~ ON ~~ / UNION or UNION ALL    
> 3.3 WHERE      
> 3.4 GROUP BY ~~ HAVING ~~      
> 3.5 ORDER BY      
> 3.6 LIMIT   

## 3.5 ORDER BY
```
# ORDER BY : 특정 컬럼 기준으로 오름차순 혹은 내림차순 정렬
SELECT column1, colum2, ...
FROM tablename
ORDER BY column1, colum2, ... ASC; # Ascending, 오름차순 (default)
ORDER BY column1, colum2, ... DESC; # Descending, 내림차순
ORDER BY column1 DESC, column2 ASC;

# NULL값의 정렬 순서
- NULL값은 특성상 대소비교를 할 수 없어 별도의 방식을 취급한다.
- 데이터베이스 제품에 따라 기준이 다른데, MySQL의 경우 NULL값을 가장 작은 값으로 취급합니다.
```

## 3.6 LIMIT
- 검색결과를 정렬된 순으로 주어진 숫자만큼 조회
```sql
SELECT *
FROM tablename
LIMIT number;

# LIMIT의 OFFSET은 생략 가능하면 기본값은 0이다.
-- number_b 행부터 nuber_a 건의 데이터를 표출한다.
SELECT *
FROM tablename
LIMIT number_a
OFFSET number_b
```
---
# 4. MySQL 함수
- [문자열 함수](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)
```sql
-- 문자열 자르기
SUBSTRING/SUBSTR(컬럼명 또는 문자열, 시작 위치, 길이)
LEFT(컬럼명 또는 문자열, 문자열의 길이)
RIGHT(컬럼명 또는 문자열, 문자열의 길이)

-- 문자 합치기
CONCAT(컬럼명 또는 문자열1, 컬럼명 또는 문자열2)
다른 데이터베이스에서는 '+'와 '||'를 사용하기도 한다.

-- 공백 제거
TRIM('ABC      ') -> 'ABC'

-- 문자열 길이
CHARACTER_LENGTH(문자열)

-- 대소문자 변환
LOWER(컬럼명 또는 문자열)
UPPER(컬럼명 또는 문자열)

-- 문자열 변경 함수
REPLACE(컬럼명 또는 문자열, 기존 변경된 문자열, 변경할 문자열)
-- 

``` 
- [숫자 함수](https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html)
```sql
-- 올림
CEIL(컬럼명 또는 값) -- 올림
FLOOR(컬럼명 또는 값) -- 내림
ROUND(컬럼명 또는 값, 자릿수) -- n자리 숫자로 반올림
TRUNCATE(컬럼명 또는 값, 자릿수) -- n자리 숫자 이하 버림
ABS(컬럼명 또는 값) -- 절댓값
POW(컬럼명 또는 값, n) / POWER(x,n) -- x의 n승
POWER(컬럼명 또는 값, 1/n) -- x의 n제곱근
SQRT(컬럼명 또는 값) -- s의 n제곱근
MOD(컬럼명 또는 값, n) -- x를 n로 나눈 나머지
```
- 날짜 연산
```sql
-- 시간 더하기 : DATE_ADD(기준날짜, INTERVAL)
SELECT DATE_ADD(NOW(), INTERVAL 1 SECOND)
SELECT DATE_ADD(NOW(), INTERVAL 1 MINUTE)
SELECT DATE_ADD(NOW(), INTERVAL 1 HOUR)
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY)
SELECT DATE_ADD(NOW(), INTERVAL 1 MONTH)
SELECT DATE_ADD(NOW(), INTERVAL 1 YEAR)
SELECT DATE_ADD(NOW(), INTERVAL -1 YEAR)

-- 시간 빼기
SELECT DATE_SUB(NOW(), INTERVAL 1 SECOND)

- 시간까지 나와 있는 데이터를 일자까지만 나오도록 변경
DATE()

- DATE_FORMAT(날짜, 형식) : 날짜를 원하는 형식으로 출력  
https://www.w3schools.com/sql/func_mysql_date_format.asp
```

- Scalar Function : 입력값을 기준으로 단일 값을 반환하는 함수

| Function | Description |
| :--: | :-- |
| UCASE | 영문을 대문자로 변환하는 함수 |
| LCASE | 영문을 소문자로 변환하는 함수 |
| MID | 문자열 부분을 반환하는 함수 |
| LENGTH | 문자열의 길이를 반환하는 함수 |
| ROUND | 지정한 자리에서 숫자를 반올림하는 함수 (0이 소숫점 첫째 자리) |
| FORMAT | 숫자를 천단위 콤마가 있는 형식으로 반환하는 함수 |
| NOW | 현재 날짜 및 시간을 반환하는 함수 |

```sql
# UCASE/LACASE/LENGTH
SELECT Scalar_function() #LENGTH의 경우 공백을 1로 반환, NULL은 NULL로 반환
FROM table
where condition;

# MID
SELECT MID(string, start_position, length) # 첫글자는 1
FROM table
where condition;

# ROUND / FORMAT
SELECT FORMAT(numer, decimal_place);

# NOW
SELECT NOW();
```

___
# 5. SUBQUERY
> Inner Query 라고 불리기도 한다. (cf. Outer Query)

## 5.1 WHERE절 서브쿼리 
- 단일 행 서브쿼리 (Single Row) :  서브쿼리의 결과값이 컬럼, 로우 모두 한 개일 때
```sql
# 서브쿼리가 비교연산자와 함게 사용되는 경우가 많다.
SELECT column_names
FROM table_name
WHERE column_name = (SELECT column_name From table_name WHERE condtion)
ORDER BY column_name;
```
- 다중 행 서브쿼리 (Multiple ROW) :  서브쿼리의 결과값이 컬럼은 한 개, 로우는 N개일 때
```sql
# IN : 서브쿼리 결과 중에 포함될 때
SELECT column_names
FROM table_name
WHERE column_name IN (SELECT column_name FROM table_name WHERE condtion)
ORDER BY column_name;

# EXISTS : 서브쿼리 결과에 값이 있을 때
SELECT column_names
FROM table_name
WHERE column_name EXISTS (SELECT column_name FROM table_name WHERE condtion)
ORDER BY column_name;

# ANY : 서브쿼리 결과 중에 최소한 하나라도 만족하면 (비교연산자 사용)
SELECT column_names
FROM table_name
WHERE column_name = ANY (SELECT column_name FROM table_name WHERE condtion)
ORDER BY column_name;

# ALL : 서브쿼리 결과를 모두 만족하면 (비교연산자 사용)
SELECT column_names
FROM table_name
WHERE column_name = ALL (SELECT column_name FROM table_name WHERE condtion);
```
- 다중 컬럼 서브쿼리 (Multiple Column) : 서브쿼리의 결과값이 컬럼, 로우 모두 N개일 때
```sql
SELECT column_names
FROM tablename
WHERE (column1, column2, ...) IN (SELECT column1_condition, column2_condition,...
                                  FROM tablename)
ORDER BY column_names;
```

## 5.2 FROM절 서브쿼리 (Inline View)
- Inline View : From절에 사용   
```sql
# 가상의 테이블을 하나 더 만든다고 생각하고 사용
# 서브쿼리에 별칭(alias) 필수
SELECT col_1, Aggregate_Functions(sample)
FROM (
      SELECT col_1
           , col_2
           , Aggregate_Functions(col_3) AS sample
      FROM tablename
      GROUP BY columname
      ) new_name
WHERE condition
GROUP BY columnname;

-- AVG 함수에서는 Null값을 무시한다. 그래서 총합을 null을 제외한 값의 수로 나눈다.
-- Null을 무시하지 않고, 0으로 취급해서 계산을 해주기 위해서는 하기의 방법을 사용한다. 
SELECT SUM(columnname)/COUNT(*)
FROM tablename

# 두 테이블을 동시에 활용할 경우
SELECT a.column, b.column
FROM table1 a, (SELECT  column1, column2 FROM table2) b
WHERE condition;
```
- WITH 구문
```sql
WITH new_name AS (
SELECT column1
           , column2
           , Aggregate_Functions(column3)
      FROM tablename
      GROUP BY columname
) new_name2 AS (
...
)

SELECT columnname
FROM new_name
WHERE condition;
```



## 5.3 SELECT절 서브쿼리 (Scalar Subquery)


- Scalar subquery : Select절에 사용   
```sql
SELECT column1, (SELECT column2 FROM table2 WHERE condition)
FROM table1
WHERE condtion;
```


---

# 6. Window Function
- 기본형태
```sql
-- GROUP BY와 달리 축약해서 보여주는 것이 아님
-- 함수(컬럼) OVER (PARTITION BY 컬럼 ORDER BY 컬럼)

# 기본형태
SELECT columnname1
     , columnname2
     ...
     , MAX(columnname) OVER (PARTITION BY columnname) AS columnnmae
FROM tablename

# 누적합 : 윈도우 함수 1
SELECT columnname1
     , columnname2
     ...
     , SUM(columnname) OVER (ORDER BY columnname) AS columnnmae
FROM tablename

# 누적합 : 윈도우 함수 2
SELECT columnname1
     , columnname2
     ...
     , SUM(columnname) OVER (PARTITION BY columnname ORDER BY columnname) AS columnname
FROM tablename

# 누적합 : 윈도우 함수 이외 1
SELECT a.column1
     , a.column2
     , SUM(column2) AS CusSum
FROM table1 a
INNER JOIN table2 b
      ON a.column1 = b.column1 AND a.column2 >= b.column2
GROUP BY 1,2,3 -- select절에 있는 인자 순서

# 누적합 : 윈도우 함수 이외 2
SELECT a.column1
     , a.column2
     , (SELECT SUM(b.columnname)
        FROM table2 b
        WHERE a.column1 = b.column2 AND a.column2 >= b.column2) AS CusSum
FROM table1 a
```
- 순위 정하기 : ROW_NUMBER(), RANK(), DENSE_RANK()   
```sql
SELECT columnname
     , ROW_NUMBER() OVER (ORDER BY val) AS new_name -- value에 따라 순위가 매겨짐
     , RANK() OVER (ORDER BY val) AS new_name -- value가 같으면 같은 순위, and 중복된 순위는 없음
     , DENSE_RANK() OVER (ORDER BY val) AS new_name -- value가 같으면 같은 순위, and 중복된 순위 있음
FROM tablename      
```
- 데이터 위치 바꾸기 : LAG(), LEAD()     
```sql
# 밀기
LAG(컬럼) OVER (PARTITION BY columnname ORDER BY columnname)
LAG(컬럼, 칸수) OVER (PARTITION BY columnname ORDER BY columnname)
LAG(컬럼, 칸수, Defalt) OVER (PARTITION BY columnname ORDER BY columnname)

# 당기기
LEAD(컬럼) OVER (PARTITION BY columnname ORDER BY columnname)
LEAD(컬럼, 칸수) OVER (PARTITION BY columnname ORDER BY columnname)
LEAD(컬럼, 칸수, Defalt) OVER (PARTITION BY columnname ORDER BY columnname)
```

---
## 7. 사용자 정의 함수(User-Defined Function)
```sql
# 함수생성
CREATE FUNCTION 'function name' ('parameter name', 'datatype')
       RETURNS 'datatype' (DETERMINISTIC)
BEGIN
       DECLARE 'variable name' 'datatype';
       SET ;
       RETURN (Query) / 'variable name';
END

# 함수 사용
SELECT 'function name'(parameter)
```
