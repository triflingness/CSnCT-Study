# DML

> Date Manipulation Language는 테이블에서 데이터를 입력, 수정, 삭제, 조회하는 언어

## INSERT

```sql
-- 구조
INSERT INTO 테이블명(col1, col2, ...) VALUES (값1, 값2, ...);
```

- 특정 테이블의 모든 칼럽에 대한 데이터를 삽입하는 경우에는 **칼럼명**(col1, col2, ...) **생략 가능**
- 데이터를 입력할 때 문자열을 입력하는 경우에는 **작은따옴표**를 사용해야 함
- 최종적으로 데이터를 저장하려면 TCL 문인 Commit을 실행해야 함
- Auto Commit(Set auto commit on)으로 설정된 경우에는 Commit을 실행하지 않아도 바로 저장됨
- SELECT 문을 사용하여 데이터를 조회해서 해당 테이블에 바로 삽입 가능

    ```sql
    INSERT INTO DEPT SELECT * FROM DEPT;
    ```

## UPDATE

```sql
UPDATE EMP SET ENAME = '조조';
```

- 원하는 조건으로 데이터를 검색해서 해당 데이터 수정 가능
- 조건문을 입력하지 않으면 모근 데이터가 수정되므로 유의해야 함

## DELETE

```sql
DELETE FROM EMP WHERE EMPNO = 100;
```

- 원하는 조건을 검색해서 해당되는 행을 삭제
- 조건문을 입력하지 않으면 모든 데이터 삭제
- DELETE 문으로 데이터를 삭제한다고 해서 **테이블의 용량이 초기화되지는 않음**
- `TRUNCATE TABLE 테이블명;`은 모든 데이터를 삭제하면서 **테이블의 용량이 초기화**됨

## SELECT

```sql
SELECT * FROM EMP WHERE 사원번호 = 1000;
```

- SELECT 문에서 EMP 테이블의 모든 칼럼'*'을 출력

```sql
SELECT ENAME || '님' FROM EMP;
-- 'ENAME님'이라고 출력됨
```
