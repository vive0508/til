SQL
===

## 1. 용어 정리
- 데이터베이스 (database, DB)
```
여러 사람이 공유하여 사용할 목적으로 체계화해 통합, 관리하는 데이터의 집합이다.
```
- DBMS (Database Management System)
```
다수의 사용자들이  데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어 도구의 집합이다. 
```
- 관계형 데이터베이스 (Relatinal Database, RDB)
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

- like
```sql
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
