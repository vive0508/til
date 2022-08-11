SQL  
=== 

## 1. 용어 정리 (위키백과)
- 데이터베이스 (database, DB)
```
여러 사람이 공유하여 사용할 목적으로 체계화해 통합, 관리하는 데이터의 집합이다.
```
- DBMS (Database Management System)
```
다수의 사용자들이 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어 도구의 집합이다. 
```
- 관계형 데이터베이스 (Relational Database, RDB)
```
서로간에 관계가 있는 데이터를 키(key)와 값(value)로 테이블화 시킨 매우 간단한 원칙의 전산정보 데이터베이스이다.
```
- SQL (Structured Query Lanagauge)
```
관계형 데이터베이스 관리 시스템(RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어이다. 
```

---

## 2. SQL 명령어
- 데이터베이스 목록 확인 : SHOW DATABASES;       
- 데이터베이스 사용 : USE databasename;      
- 테이블 확인 : SHOW TABLES;   
- 테이블 정보 확인 : DESC tablename;   
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

# 컬럼 생성
ADD COLUMN columnname datatype;

# 컬럼명 변경
CHANGE COLUMN old_columnname new_columnname new_datatype;

# 컬럼 데이터타입 변경
MODIFY COLUMN columnname datatype;
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
> 데이터의 갱신 : INSERT(등록) / UPDATE(수정) / DELETE(제거)  

- SELECT : Read     
> **순서 익히기**   
> 1. SELECT
> 2. FROM   
> 3. INNER JOIN ~~ ON ~~ 
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

# ORDER BY : 특정 컬럼 기준으로 오름차순 혹은 내림차순 정렬
SELECT column1, colum2, ...
FROM tablename
ORDER BY column1, colum2, ... ASC; # Ascending, 오름차순 (default)
ORDER BY column1, colum2, ... DESC; # Descending, 내림차순
ORDER BY column1 DESC, column2 ASC;

# WHERE 조건
SELECT column1, colum2, ...
FROM tablename
WHERE condition;

# NULL값 조회
-- NULL, NaN (Not a Number) : 숫자도 문자도 아니고 비어있는 값이다
SELECT *
FROM tablename
WHERE columnname IS NULL;

# NULL이 아닌 값을 조회
SELECT *
FROM tablename
WHERE columnname IS NOT NULL;
```

- INSERT : Create   
```sql
# 입력한 컬럼 이름의 순서와 값의 순서가 일치하도록 주의
INSERT INTO tablename (column1, column2, ...)
VALUES (value1, value2, ...);

# 모든 컬럼의 값을 추가하는 경우 컬럼 이름을 지정하지 않아도 됨
INSERT INTO tablename
VALUES (value1, value2, ...);
```

- UPDATE : Update    
```sql
UPDATE tablename
SET column1 = value1, colum2=value2, ...
WHERE condition;

# 예시 
UPDATE tablename
SET columnA = comlumnA + 100
WHERE condition;

# CASE와 함께 사용
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
# 테이블에 전체 데이터 삭제
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
- GRANT : 권한 부여   
- REVOKE : 권한 해제   
- COMMIT
- ROLLBACK

___

## 3. 연산자
### 3.1 비교 연산자

| 비교 연산자 | 논리 연산자 |
| :--: | :-- |
| A=B | A와 B가 같다 |
| A>B | A가 B보다 크다 (초과) |
| A<B | A가 B보다 작다 (미만) |
| A>=B | A가 B보다 크거나 같다 (이상) |
| A<=B | A가 B보다 작거나 같다 (이하) |
| A<>B | A가 B보다 크거나 작다 (같지 않다) |
| A!=B | A와 B가 같지 않다 |

### 3.2 논리 연산자

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
---
### 4 MySQL 함수
- 문자열 자르기
```sql
LEFT(컬럼명 또는 문자열, 문자열의 길이)
RIGHT(컬럼명 또는 문자열, 문자열의 길이)
SUBSTRING/SUBSTR(컬럼명 또는 문자열, 시작 위치, 길이)
``` 
- [숫자 함수](https://jjeongil.tistory.com/928)
```sql
CEIL(수) -- 값보다 큰 정수 중 가장 작은 정수를 구한다
FLOOR(수) -- 값보다 작은 정수 중 가장 큰 정수를 구한다
ROUND(수, 자릿수)
```
- 시간 더하기 빼기
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
```

---
## 5. UNION
- SQL문을 합치는 방법   
- 컬럼의 갯수가 같아야 한다
```sql
# UNION : 중복된 값을 제거하고 알려준다
# UNION ALL : 중복된 값도 모두 보여준다
SELECT column1, column2, ... FROM tableA
UNION | UNION ALL
SELECT column1, column2, ... FROM tableB
ORDER BY columname;
```

---
## 6 JOIN
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
- SELF JOIN : 한 테이블을 자기 자신에 같다 붙이는 방법
```
SELECT columnname
FROM tablename
     INNER JOIN tablename AS new_tablename ON tablename.columnA = newtablename.columnB
WHERE condition;
```

___
## 7. CONCAT / ALIAS
- CONCAT
```sql
SELECT CONCAT('stringA', ' ', 'stringB', ...); # stringA stringB
SELECT CONCAT('정답 :', colmname) FROM tablename; # 정답: ooo
```
- ALIAS
```sql
# 컬럼명 별칭 생성
SELECT column1 as alias1, column2 as alias2, ... FROM tablename;

# 테이블명 별칭 생성
SELECT column1, column2, ... FROM tablename as alias;

# ALIAS (with CONCAT)
SELECT CONCAT(columnA, ' : ', columnB) as alias FROM tablename;

# ALIAS (with SELF JOIN)
SELECT a.column1, a.column2, b.column3, b.column3 
FROM tableA as a, tableB as b
WHERE condition; # where절에 조건으로 기준 설정
```
as를 생략해도 결과는 똑같이 나온다
___
## 8. DISTINCT
- 검색한 결과의 중복 제거
```python
SELECT DISTINCT column1, column2, ...
FROM tablename
WHERE condition;
```
- SELECT와 함께 사용
```python
# 중복제거된 데이터를 3개만 확인할 때
SELECT DISTINCT column1, column2, ...
FROM tablename
WHERE condition
LIMIT 3;

# 중복값 제외한 결과의 수 확인
SELECT COUNT (DISTINCT columnname) from tablename;
```
___
## 9. LIMIT
- 검색결과를 정렬된 순으로 주어진 숫자만큼 조회
```sql
# WHERE와 함께 사용
SELECT column1, column2, ...
FROM tablename
WHERE condition
LIMIT number;


___
## 10. SQL 파일 실행 및 백업

- mysql 로그인
```sql
# 로컬에서 사용시
mysql -u root -p비밀번호

# aws rds 사용시
mysql -h "앤드포인트 주소" -P 포트번호 -u admin -p

# mysql 로그인 종료
exit
```
- sql 파일 실행
```sql
# mysql에 접속하여 파일을 실행하는 방법
mysql> source </path/filename.sql>
mysql> \. </path/filename.sql> # source 대신 \. 사용가능
mysql> \. </path/filename.sql> # 현재 폴더에 파일이 있으면 path 생략

# 터미널에서 파일을 바로 실행시키는 방법
mysql -u username -p <dbname> < </path/filename.sql> #-p 다음에 뛰어쓰면 데이터베이스로 인식
```
- sql 파일 백업
```sql
# 데이터베이스 백업
mysqldump -u username -p dbname > backup.sql # 특정 Database Backup
mysqldump -u username -p --all-databases > backup.sql # 모든 Database Backup

# 테이블 백업
mysqldump -u username -p dbname tablename > backup.sql

# 테이블 생성 쿼리 백업 (데이터 제외)
mysqldump -d -u username -p dbname tablename > backup.sql # 특정 Table Schema Backup
mysqldump -d -u username -p dbname > backup.sql # 모든 Table Schema Backup

# AWS RDS에서 백업하는 경우 필요한 옵션
mysqldump --set-gtid-purged=OFF -h <hostname> -P <port> -u <username> -p <databasename> > <filename>.sql
```

___
## 11. Python with MySQL
- 설치 및 불러오기
```sql
pip install mysql-connector-python
import mysql.connector
```
- mysql에 접속하기 위한 코드 (커넥션 만들기)
```sql
local = mysql.connector.connect(
 host = "<hostname>",
 user = "<username>",
 password = "<password>",
 database = "<databasename>" #옵션
)

remote = mysql
mysql.connector.connect(
 host = "<hostname>",
 port = "<port>",
 user = "<username>",
 password = "<password>"
 database = "<databasename>" #옵션
)
```
- mysql 종료
```sql
local.close()
remote.close()
```
- 쿼리 및 파일 실행 & 결과 확인
```sql
import mysql.connector

mydb = mysql.connector.connec(
host = "<hostname>",
 user = "<username>",
 password = "<password>",
 database = "<databasename>" #옵션
)

cur = mydb.cursor(burffered=True) # 읽을 데이터의 양이 많은 경우

# Query를실행하기 위한 코드
cur.execute(<querty>)

# SQL 파일을 실행하기 위한 코드
sql = open("<filename>.sql").read()
cur.execute(sql)

# SQL 파일 내에 쿼리가 여러개 존재하는 경우
sql = open("<filename>.sql").read()
cur.execute(sql)

# 결과값 확인
result = cur.fetchall()
for result_iterator in result:
    print(result_iterator)

mydb.close()

# 결과값 확인 (with Pandas)
import pandas as pd

df = pd.DataFrame(result)
df.head()
```
___
## 12. Python with CSV
#### 예제 1
- 파일 불러오기
```sql
import pandas as pd
import mysql.connector

# 파일 불러오기 
df = pd.read_csv('ooo.csv', encoding='utf-8') # utf-8이 안되면 euc-kr로

# mysql에 접속하기 위한 코드 만들기
conn = mysql.connector.connect(
 host = "<hostname>",
 port = "<port>",
 user = "<username>",
 password = "<password>"
 database = "<databasename>"
)

# cursor 만들기
cur = conn.cursor(burffered=True)

# insert와 itterows를 활용하여 데이터를 넣고
sql = "INSERT INTO tablename VALUES ('2022', %s, %s, ...)"

for i, row in df.interrows():
 cursor.execute(sql, tuple(row)):
 conn.commit()  # commit() : 데이터베이스에 적용하기 위한 명령어
 
# 결과를 확인한다
cursor.execute("SELECT * FROM tablename")
result = cursor.fetchall()

for row in result;
 print(row)
 
# 판다스로 다시 확인
import pandas as pd

df = pd.DataFrame(result)
df.head()
```
___
## 13. Primary key
- Primary key 생성
```sql
CREATE TABLE tablename
(
  column1 datatype NOT NULL,
  column2 datatype NOT NULL,
  ...
  CONSTRAINT constraint_name # 생략가능
   PRIMARY KEY (column1, column2, ...)
);
```
- Primary key 추가
```sql
# 하나의 컬럼을 기본키로 지정
ALTER TABLE tablename
ADD CONSTRAINT constraint_name # 생략가능
PRIMARY KEY (column1, column2, ...);
```
- Primary key 삭제
```sql
ALTER TABLE tablename
DROP PRIMARY KEY;
```
___
## 14. Foreign key
- Foreign key 생성
```sql
# 한 테이블을 다른 테이블과 연결
CREATE TABLE tablename
(
 column1 datatype NOT NULL,
 column2 datatype NOT NULL,
 column3 datatype,
 column4 datatype,
 ...
 CONSTRAINT constraint_name # 생략가능
  PRIMARY KEY (column1, column2, ...),
 CONSTRAINT constraint_name # 생략가능
  FOREINGN KEY (column2, column4, ...) REFERENCES REF_tablename(REF_column)
```
- 자동생성된 CONSTRAINT 확인방법
```sql
SHOW CREATE TABLE tablename;
```
- FOREIGN KEY 추가
```sql
ALTER TABLE tablename
ADD FOREIGN KEY (column) REFERENCES REF_tablename(REF_column);
```
- FOREIGN KEY 삭제
```sql
ALTER TABLE tablename
DROP FOREIGN KEY FK_constraint;
```
___
## 15. Aggregate Function (집계함수)

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
___
## 16. GROUP BY
```sql
-- 집계함수와 함께 사용할 수 있다.
SELECT colunm1, colunm2, ...
FROM table
WHERE condition
GROUP BY colunm1, colunm2, ... # DISTINCT와 함께 사용 가능
ORDER BY colunm1, colunm2, ...; # DISTINCT와 함께 사용하는 경우 ORDER BY 불가능
```

___
## 17. HAVING
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
---
## 18. 조건문
- CASE
```sql
-- ELSE 이후의 값을 입력하지 않으면 NULL이 기본값으로 들어간다.
SELECT CASE
            WHEN condition1 THEN resultA
            WHEN condition2 THEN resultB
            ...
            ELSE resultZ
       END AS sth, *
FROM tablename
GROUP BY sth
```   
-  IF
```sql
SELECT IF(조건, 조건이 True일 때, 조건이 false일 때)
FROM tablename
```
- 피봇테이블 사용
[관련문제]([https://github.com/vive0508/TIL/tree/main/SQL/LeetCode](https://github.com/vive0508/TIL/blob/main/SQL/LeetCode/reformat%20department%20table.md))
---
## 20. Scalar Function
- 입력값을 기준으로단일 값을 반환하는 함수

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
## 20. Subquery
- Scalar subquery : Select절에 사용   
```sql
SELECT column1, (SELECT column2 FROM table2 WHERE condition)
FROM table1
WHERE condtion;
```
- Inline View : From절에 사용   
```sql
# 가상의 테이블을 하나 더 만든다고 생각하고 사용
SELECT columnnameA, Aggregate_Functions(columnnameB)
FROM (
      SELECT column1
           , column2
           , Aggregate_Functions(column3)
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
- Nested Subquery : Where절에 사용
  - Single ROW : 하나의 열을 검색하는 서브쿼리
  ```sql
  # 서브쿼리가 비교연산자와 함게 사용되는 경우, 한 개의 결과값을 가져와야 한다.
  SELECT column_names
  FROM table_name
  WHERE column_name = (SELECT column_name From table_name WHERE condtion)
  ORDER BY column_name;
  ```
  - Multiple ROW : 하나 이상의 열을 검색하는 서브쿼리
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
  
  - Multiple Column : 하나 이상의 행을 검색하는 서브 쿼리
  ```sql
  SELECT column_names
  FROM tablename a
  WHERE (a.column1, a.column2, ...) IN (SELECT b.column1, b.column2,...
                                        FROM tablename b
                                        WHERE a.column_name=b.column_name)
  ORDER BY column_names;
  ```

---
### ERD(entity relationship diagram)
- 구성요소([참고링크](https://www.lucidchart.com/pages/er-diagrams#section_5))
  - entity : 개체, 테이블   
  - attribute : 컬럼명, 데이터타입(Primary key, foreign key)   
  - relationship : one to many, many to many   
---
### data type   
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

### Window Function
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
### 사용자 정의 함수(User-Defined Function)
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

---


