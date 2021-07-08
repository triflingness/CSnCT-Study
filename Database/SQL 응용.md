# DECODE

- DECODE문으로 **IF문**을 구현 가능

```sql
DECODE(EMPNO, 1000, 'TURE', 'FALSE')
-- EMPNO=1000과 같으면 TRUE를 응답하고, 같지 않으면 FALSE를 응답
```

# CASE문

- IF~THEN~ELSE-END의 프로그래밍 언어처럼 **조건문**을 사용할 수 있음
- 조건을 WHEN구에 사용하고 THEN은 해당 조건이 참이면 실행되고 거짓이면 ELSE구가 실행됨

```sql
CASE [expression]
	WHEN condition_1 THEN result_1
	WHEN condition_2 THEN result_2
	...
	WHEN condition_n THEN result_n
	ELSE result
END
```

# ROWNUM

- Oracle 데이터베이스의 SELECT문 결과에 대해서 **논리적인 일련번호**를 부여
- 조회되는 행 수를 제한할 때 많이 사용됨
- 화면에 데이터를 출력할 때 부여되는 논리적 순번
- ROWNUM을 사용해서 페이지 단위 출력을 하기 위해서는 인라인 뷰(Inline view)를 사용해야 함

    > 인라인 뷰(Inline view)는 SELECT문에서 FROM절에 사용되는 서브쿼리를 의미

```sql
-- 한 행을 조회
-- ROWNUM < 2까지는 사용 사능
-- 여러 행을 조회하기 위해서는 인라인 뷰를 사용해야 함
SELECT * FROM EMP
WHERE ROWNUM <= 1;

-- ROWNUM에 별칭 list를 사용
-- 5건의 행을 조회
SELECT *
FROM ( SELECT ROWNUM list, ENAME
				FROM EMP)
WHERE list <= 5;
```

```sql
-- SQL Server
SELECT TOP(10) FROM EMP;

-- MySQL
SELECT * FROM EMP LIMIT 10;
```

# ROWID

- Oracle 데이터베이스 내에서 **데이터를 구분할 수 있는 유일한 값**
- `SELECT ROWID, EMPNO FROM EMP`와 같은 SELECT 문으로 확인 가능
- 데이터가 어떤 데이터 파일, 어느 블록에 저장되어 있는지 알 수 있음

## ROWID의 구조

|구조|길이|설명|
|:-:|:-:|-|
|오브젝트 번호|1~6|오브젝트(Object) 별로 유일한 값을 가지고 있으며, 해당 오브젝트가 속해 있는 값|
|상대 파일 번호|7~9|테이블스페이스(Tablespace)에 속해 있는 데이터 파일에 대한 상대 파일 번호|
|블록 번호|10~15|데이터 파일 내부에서 어느 블록에 데이터가 있는지 알려줌|
|데이터 번호|16~18|데이터 블록에 데이터가 저장되어 있는 순서를 의미|

# WITH 구문

- 서브쿼리를 사용해서 **임시 테이블이나 뷰처럼 사용할 수 있는 구문**
- 서브쿼리 블록에 별칭 지정 가능
- 옵티마이저는 SQL을 인라인 뷰나 임시 테이블로 판단

```sql
WITH viewData AS
	(SELECT *
	 UNION ALL
	 SELECT * FROM EMP
	)
	SELECT * FROM viewData WHERE EMPNO=1000;
```
