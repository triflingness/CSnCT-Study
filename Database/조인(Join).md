# 조인(Join)

# EQUI(등가) 조인 = 교집합

## EQUI(등가) 조인

- 조인은 **여러 개의 릴레이션을 사용해서 새로운 릴레이션을 만드는 과정**
- 조인의 가장 기본은 **교집합**을 만드는 것
- **두 개의 테이블 간에 일치하는 것**을 조인함
- 등가 조인은 A테이블과 B테이블에서 데이터 타입이 같은 칼럼을 사용하여 같은 것을 조인
- 등가 조인은 `=`을 사용해서 두 개의 테이블을 연결

```sql
SELECT * FROM EMP, DEPT
WHERE EMP.DEPTNO = DEPT.DEPTNO;
```

## INNER JOIN

- EQUI 조인과 마찬가지로 ISO 표준 SQL로 INNER JOIN이 있음
- INNER JOIN은 ON문을 사용해서 테이블을 연결함

```sql
-- INNER JOIN구로 테이블 정의
-- ON구를 사용해 조인 조건을 넣음
SELECT * FROM EMP INNER JOIN DEPT
ON EMP.DEPTNO = DEPT.DEPTNO;
```

## INTERSECT 연산

- INTERSECT 연산은 두 개의 테이블에서 교집합을 조회함
- 즉, 두 개 테이블에서 공통된 값을 조회

```sql
SELECT DEPTNO FROM EMP
INTERSECT
SELECT DEPTNO FROM DEPT;
-- 공통된 컬럼인 DEPTNO만 출력됨
```

# Non-EQUI(비등가) 조인

- Non-EQUI는 두개의 테이블 간에 조인하는 경우 `=`을 사용하지 않고 `>,<,>=,<=` 등을 사용함
- 즉, Non-EQUI 조인은 정확하게 일치하지 않는 것을 조인하는 것

# OUTER JOIN

- OUTER JOIN은 두 개의 테이블 간에 교집합(EQUI JOIN)을 조회하고 **한쪽 테이블에만 있는 테이터도 포함**시켜서 조회
- 왼쪽 테이블에 있는 행도 포함하면 LEFT OUTER JOIN
- 오른쪽 테이블에 있는 행만 포함시키면 RIGHT OUTER JOIN
- FULL OUTER JOIN은 LEFT OUTER JOIN과 RIGHT OUTER JOIN 모두를 하는 것
- Oracle 테이터베이스에서는 OUTER JOIN을 할 때 `(+)` 기호를 사용해서 할 수 있음

```sql
SELECT * FROM DEPT, EMP
WHERE EMP.DEPTNO (+)= DEPT.DEPTNO;
```

## LEFT OUTER JOIN과 RIGHT OUTER JOIN

- LEFT OUTER JOIN은 두 개의 테이블에서 같은 것을 조회하고 **왼쪽 테이블에만 있는 것을 포함**해서 조회

```sql
SELECT * FROM DEPT LEFT OUTER JOIN EMP
ON EMP.DEPTNO = DEPT.DEPTNO;
```

- RIGHT OUTER JOIN은 두 개의 테이블에서 같은 것을 조회하고 **오른쪽 테이블에만 있는 것을 포함**해서 조회

```sql
SELECT * FROM DEPT RIGHT OUTER JOIN EMP
ON EMP.DEPTNO = DEPT.DEPTNO;
```

# CROSS JOIN

- CROSS JOIN은 **조인 조건구 없이** 2개의 테이블을 하나로 조인함
- 조인구가 없기 때문에 카테시안 곱이 발생
- 예를 들어 행이 14개 있는 테이블과 행이 4개 있는 테이블을 조인하면 56개의 행이 조회됨
- CROSS JOIN은 FROM절에 CROSS JOIN구를 사용하면 됨

```sql
SELECT * FROM EMP CROSS JOIN DEPT;
```

# UNION을 사용한 합집합 구현

## UNION

- UNION 연산은 두 개의 테이블을 하나로 만드는 연산
- 즉, 2개의 테이블을 하나로 합치는 것
- 주의사항은 두 개의 **테이블의 칼럼 수, 칼럼의 테이터 형식 모두가 일치**해야 함
- 만약 두 개의 테이블에 UNION 연산이 사용될 때 칼럼 수 혹은 테이터 형식이 다르면 오류가 발생
- UNION 연산을 두 개의 테이블을 하나로 합치면서 중복된 데이터를 제거함
- 그래서 UNION은 정렬(SORT) 과정을 발생시킴

```sql
SELECT DEPTNO FROM EMP
UNION
SELECT DEPTNO FROM EMP;
```

## UNION ALL

- UNION ALL은 두 개의 테이블을 하나로 합치는 것
- UNION처럼 중복을 제거하거나 정렬을 유발하지 않음

```sql
-- UNION ALL은 단순하게 테이블을 합침
SELECT DEPTNO FROM EMP
UNION ALL
SELECT DEPTNO FROM EMP;
```

# 차집합을 만드는 MINUS

- MINUS 연산은 두 개의 테이블에서 차집합을 조회
- 즉, 먽저 쓴 SELECT문에는 있고 뒤에 쓰는 SELECT문에는 없는 집합을 조회하는 것
- MS-SQL에서는 MINUS와 동일한 연산이 EXCEPT임

```sql
SELECT DEPTNO FROM EMP
MINUS
SELECT DEPTNO FROM EMP;
```
