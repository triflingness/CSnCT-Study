# DCL

> Data Control Language는 데이터베이스 사용자에게 권한을 부여하거나 회수하는 언어

## GRANT

- 데이터베이스 사용자에게 **권한을 부여**
- 데이터베이스 사용을 위해서는 권한이 필요하며 **연결, 입력, 수정, 삭제, 조회**를 할 수 있음

```sql
GRANT privileges ON object TO user;
-- privileges는 권한을 의미하며 object는 테이블명
-- user는 Oracle 데이터베이스 사용자를 지정하면 됨
```

### 권한(Privileges)

|권한|설명|
|:-:|-|
|SELECT|지정된 테이블에 대해서 **SELECT 권한**을 부여|
|INSERT|지정된 테이블에 대해서 **INSERT 권한**을 부여|
|UPDATE|지정된 테이블에 대해서 **UPDATE 권한**을 부여|
|DELETE|지정된 테이블에 대해서 **DELETE 권한**을 부여|
|REFERENCES|지정된 테이블을 참조하는 **제약조건을 생성**하는 권한을 부여|
|ALTER|지정된 테이블에 대해서 **수정**할 수 있는 권한을 부여|
|INDEX|지정된 테이블에 대해서 **인젝스를 생성**할 수 있는 권한을 부여|
|ALL|테이블에 대한 **모든 권한**을 부여|

### WITH GRANT OPTION

- WITH GRANT OPTION
    - 특정 사용자에게 권한을 부여할 수 있는 권한을 부여
    - 권한을 A 사용자가 B에 부여하고 B가 다시 C를 부여한 후에 권한을 취소하면 **모든 권한 회수**
- WITH ADMIN OPTION
    - 테이블에 대한 모든 권한을 부여
    - 권한을 A 사용자가 B에 부여하고 다시 B가 C에게 부여한 후에 권한을 취소하면 **B 사용자 권한만 취소**

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
	ON EMP
	TO LIMBEST WITH GRANT OPTION;
```

## REVOKE

- 데이터베이스 사용자에게 부여된 권한을 회수

```sql
REVOKE privileges ON object FROM user;
```

## TURNCATE

- 특정 테이블의 모든 데이터를 삭제
- 데이터만 삭제하므로 테이블 구조에는 영향 X

```sql
TURNCATE TABLE EMPLOYEE;
```
