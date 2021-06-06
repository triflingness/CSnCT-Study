# DDL

> Data Definition Language는 데이터베이스 데이터를 보관하고 관리하기 위해 제공되는 여러 객체의 생성, 변경, 삭제 관련 기능을 수행

## 특징

- DML과 달리 명령어를 수행하자마자 데이터베이스에 수행한 내용이 바로 반영됨(자동으로 `COMMIT`)
- `ROLLBACK`을 통한 실행 취소가 불가능

## 1. CREATE

- 스키마

```sql
-- KIM이라는 계정을 가진 사용자가 MY_DB라는 스키마를 생성
CREATE SCHEMA MY_DB AUTHORIZATION KIM;
```

- 테이블

```sql
CREATE TABLE DEPARTMENT(
	DEPTNO INTEGER NOT NULL,
	DEPTNAME CHAR(10),
	FLOOR INTEGER,
	PRIMARY KEY(DEPTNO));

CREATE TABLE EMPLOYEE(
	EMPNO INTEGER NOT NULL,
	EMPNAME CHAR(10),
	TITLE CHAR(10),
	MANAGER INTEGER,
	SALARY INTEGER,
	PRIMARY KEY(EMPNO),
	FOREIGN KEY(MANAGER) REFERENCES EMPLYOEE(EMPNO),
	FOREIGN KEY(DNO) REFERENCES DEPARTMENT(DEPTNO));
```

- 인덱스
    - 릴레이션의 하나 이상의 애트리뷰트에 대해 인덱스 생성
    - 뷰에는 인덱스 생성 불가능

```sql
-- EMPLOYEE 릴레이션의 DNO 애트리뷰트에 EMPDNO_IDX라는 이름의 인덱스 생성
CREATE INDEX EMPDNO_IDX ON EMPLOYEE(DNO);
```

- 뷰

```sql
-- 문법
CREATE VIEW 뷰이름[(속성이름[,속성이름])] AS SELECT문;

-- 고객 테이블에서 주소가 서울시인 고객들의 성명과 전화번호를 서울고객이라는 뷰로 만들어라
CREATE VIEW 서울고객(성명, 전화번호)
AS SELECT 성명, 전화번호
FROM 고객
WHERE 주소 = '서울시';
```

- 도메인
    - 한 스키마의 여러 애트리뷰트에서 사용되는 어떤 도메인의 데이터 타입을 쉽게 변경 가능
    - 도메인을 정의한 곳에서 도메인 정의를 변경하면 도메인 정의를 사용하는 모든 곳에서 일관되게 적용됨
    - 도메인 정의에 디폴트 값 지정 가능

```sql
CREATE DOMAIN DEPTNAME CHAR(10) DEFAULT '개발';
```

## 2. ALTER

- 테이블

```sql
-- 1. ADD
ALTER TABLE EMPLOYEE ADD PHONE CHAR(13);
-- 2. RENAME
ALTER TABLE EMPLOYEE RENAME COLUMN PHONE TO TEL;
-- 3. MODIFY
ALTER TABLE EMPLOYEE MODIFY EMPNAME CHAR(20);
-- 4. DROP
ALTER TABLE EMPLOYEE DROP COLUMN TEL;
```

## 3. DROP

- 스키마

```sql
-- 스키마가 비어 있지 않으면 거절
DROP SCHEMA MY_DB;
```

- 테이블

```sql
-- 릴레이션의 정의와 릴레이션의 튜플이 모두 삭제
-- 다른 릴레이션이나 뷰에서 참조되지 않은 릴레이션들만 제거 가능
DROP TABLE DEPARTMENT;
```

- 인덱스

```sql
-- EMPLOYEE 릴레이션의 EMPDNO_IDX라는 이름의 인덱스 삭제
DROP INDEX EMPLOYEE.EMPDNO_IDX;
```

- 뷰
    - 뷰는 ALTER문을 사용하여 변경할 수 없으므로 필요한 경우는 삭제한 후 재생성

```sql
-- 문법
DROP VIEW 뷰이름 RESTRICT or CASCADE

-- 서울고객이라는 뷰를 삭제해라
DROP VIEW 서울고객 RESTRICT;
```

- 도메인

```sql
-- RESTRICT 절을 명시하여 도메인을 제거하려 할 때,
-- 이 도메인 정의가 애트리뷰트 정의에서 참조되고 있으면 제거 거절
DROP DOMAIN DEPTNAME RESTRICT;
```

## 4. RENAME

- 테이블 이름 변경

```sql
RENAME EMPLOYEE TO EMP;
```

## 제약 조건

```sql
CREATE TABLE EMPLOYEE(
	EMPNO INTEGER NOT NULL, -- 1. NOT NULL
	EMPNAME CHAR(10) UNIQUE, -- 2. UNIQUE
	TITLE CHAR(10) DEFAULT '사원', -- 3. DEFAULT
	MANAGER INTEGER,
	SALARY INTEGER CHECK (SALARY < 6000000), -- 4. CHECK
	DNO INTEGER CHECK (DNO IN (1,2,3,4,5,6)) DEFAULT 1, -- CHECK, DEFAULT
	PRIMARY KEY(EMPNO), -- 기본키 제약조건
	FOREIGN KEY(MANAGER) REFERENCES EMPLYOEE(EMPNO), -- 참조 무결성 제약조건
	FOREIGN KEY(DNO) REFERENCES DEPARTMENT(DEPTNO) -- 참조 무결성 제약조건
		ON DELETE SET DEFAULT ON UPDATE CASCADE);
```

### ON DELETE

- ON DELETE NO ACTION
    - RESTRICT과 같음
    - 절을 생략하면 디폴트는 NO ACTION
- ON DELETE CASCADE
- ON DELETE SET NULL
- ON DELETE SET DEFAULT

### ON UPDATE

- ON UPDATE NO ACTION
    - RESTRICT과 같음
    - 절을 생략하면 디폴트는 NO ACTION
- ON UPDATE CASCADE
- ON UPDATE SET NULL
- ON UPDATE SET DEFAULT
