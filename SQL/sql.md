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

### 2.2 데이터 조작 언어 (DML : Data Manipulation Language)
- 데이터 관리(데이터 CRUD)를 위한 언어   
- INSERT : Create   
- SELECT : Read     
```sql
# 사용자 정보는 mysql에서 관리
USE mysql;
SELECT host, user FROM user;
```
- UPDATE : Update    
- DELETE : Delete    
 
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
