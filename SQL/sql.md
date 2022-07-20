SQL
===

## 1. 용어 정리
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

## 2. SQL 언어
### 2.0 기타
- 데이터베이스 목록 확인 : SHOW DATABASES;    
- 데이터베이스 사용 : USE databasename;   
- 테이블 확인 : SHOW TABLES;
- 테이블 정보 확인 : DESC tablename;

### 2.1 데이터 정의 언어 (DDL : Data Definition Lanaguage)
- 각 릴레이션(데이터베이스 테이블)을 정의하기 위해 사용하는 언어   
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
 columnname datatype NOT NULL AUTO_INCREMENT PRIMATY KEY, # null : no, extra : auto_increment 
 columnname datatype NOT NULL DEFAULT '', # default not null
 ...
)

# 내부 접근 유저 생성
CREATE USER 'username'@'localhost' identified by 'password';

# 외부 접근 유저 생성 (호스트 정보가 다른 user는 이름이 같아도 상관없음)
CREATE USER 'username'@'%' identified by 'password';
```
- ALTER : 테이블 변경   
```sql
# 테이블 변경(필수)
ALTER TABLE tablename

# 테이블 이름 변경
RENAME new_tablename;

# 컬럼 생성
ADD COLUMN columnname datatype;

# 컬럼명 변경
CHANGE COLUMN old_columnname new_columnname new_datatype;

# 컬럼 데이터타입 변경
MODIFY COLUMN columnname datatype;

# 컬럼 삭제
DROP COLUMN columnname;
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

# 유저 삭제
DROP USER 'username'@'localhost';
DROP USER 'username'@'%';
```

___

### 2.2 데이터 조작 언어 (DML : Data Manipulation Language)
- 데이터 관리(데이터 CRUD)를 위한 언어   
- INSERT : Create   
```sql
# 입력한 컬럼 이름의 순서와 값의 순서가 일치하도록 주의
INSERT INTO tablename (column1, column2, ...)
VALUES (value1, value2, ...);

# 모든 컬럼의 값을 추가하는 경우 컬럼 이름을 지정하지 않아도 됨
INSERT INTO tablename
VALUES (value1, value2, ...);
```
- SELECT : Read     
```sql
# 테이블 전체내용 조회
SELECT * from tablename;

# 테이블 특정 컬럼 조회
SELECT column1, colum2, ...
FROM tablename;

# 사용자 정보는 mysql에서 관리
USE mysql;
SELECT host, user FROM user;

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
- UPDATE : Update    
```sql
Update tablename
SET column1 = value1, colum2=value2, ...
WHERE condition;
```
- DELETE : Delete    
```sql
# 조건에 부합하는 데이터 삭제
DELETE FROM tablename
WHERE condition;
```
___
 
### 2.3 데이터 제어 언어 (DCL : Data Control Language)   
- 사용자 관리 & 사용자별 권한 (릴레이션 및 데이터에 대한 관리/접근)을 다루기 위한 언어   
- GRANT : 권한 부여
```sql
# 사용자에게 부여된 모든 권한 목록을 확인
SHOW GRANTS FOR 'username'@'localhost';

# 사용자에게 특정 데이터베이스의 모든 권한을 부여
GRANT ALL ON databasename.* to 'username'@'localhost';

# 새로 부여한 권한이 확인이 안되면, 새로고침
FLUSH PRIVILIEGES;
```
- REVOKE : 권한 해제 
```sql
# 부여한 권한 삭제
REVOKE ALL ON databasename.* from 'username'@'localhost';
```
- COMMIT
- ROLLBACK

___

### 2.4 연산자
> WHERE를 연산자와 함께 사용한다.

#### 2.4.1 비교 연산자

| 비교 연산자 | 논리 연산자 |
| :--: | :-- |
| A=B | A와 B가 같다 |
| A>B | A가 B보다 크다 (초과) |
| A<B | A가 B보다 작다 (미만) |
| A>=B | A가 B보다 크거나 같다 (이상) |
| A<=B | A가 B보다 작거나 같다 (이하) |
| A<>B | A가 B보다 크거나 작다 (같지 않다) |
| A!=B | A와 B가 같지 않다 |

#### 2.4.2 논리 연산자

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
### 2.5 UNION
- SQL문을 합치는 방법   
- 컬럼의 갯수가 같아야 한다
```sql
# 중복된 값을 제거하고 알려준다
# 중복된 값도 모두 보여준다
SELECT column1, column2, ... FROM tableA
UNION | UNION ALL
SELECT column1, column2, ... FROM tableB;
```

---
### 2.6 JOIN
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
ON tableA.column = tableB.column
UNION
WHERE condition;
```

- SELF JOIN : 교집합
```sql
SELECT column1, column2, ...
FROM tableA, tableB, ...
WHERE condition; # where절에 조건으로 기준 설정
```

___
### 2.7 CONCAT / ALIAS
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
### 2.8 DISTINCT
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
### 2.9 LIMIT
- 검색결과를 정렬된 순으로 주어진 숫자만큼 조회
```sql
# WHERE와 함께 사용
SELECT column1, column2, ...
FROM tablename
WHERE condition
LIMIT number;

# ORDER BY와 함께 사용
SELECT * from tablename
ORDER BY columnname
LIMIT number;
```

---
### 2.10 기타
- 새로고침
```sql
flush privileges;
```

___
### 2.11 SQL 파일 실행 및 백업

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
### 2.12 Python with MySQL
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
### 2.13 Python with CSV
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
### 2.14 Primary key
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
### 2.15 Foreign key
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
### 2.16 Aggregate Function (집계함수)

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
SELECT Aggregate_Functions(column)
FROM tablename
WHERE condition;
```
___
### 2.17 GROUP BY
```sql
SELECT colunm1, colunm2, ...
FROM table
WHERE condition
GROUP BY colunm1, colunm2, ... # DISTINCT로 대체하여 사용 가능
ORDER BY colunm1, colunm2, ...; # DISTINCT를 사용하는 경우 ORDER BY 불가능
```

___
### 2.18 HAVING
- 조건에 집계함수가 포함되는 경우 WHERE 대신 HAVING 사용
```sql
SELECT colunm1, colunm2, ...
FROM table
WHERE condition
GROUP BY colunm1, colunm2, ... 
HAVING condition (Aggregate_Functions)
ORDER BY colunm1, colunm2, ...; 
```
---
### 2.19 Scalar Function
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
### 2.20 SQL Subquery
- Scalar subquery : Select절에 사용   
```sql
SELECT column1, (SELECT column2 FROM table2 WHERE condition)
FROM table1
WHERE condtion;
```
- Inline View : From절에 사용   
```sql
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
  
  - Multiple Column : 하나 이상의 행을 검색하는서브 쿼리
  ```sql
  SELECT column_names
  FROM tablename a
  WHERE (a.column1, a.column2, ...) IN (SELECT b.column1, b.column2,...
                                        FROM tablename b
                                        WHERE a.column_name=b.column_name)
  ORDER BY column_names;
  ```
