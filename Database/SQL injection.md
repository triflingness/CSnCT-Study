# SQL injection

`SQL injection`(SQL 주입)은 웹 페이지 입력을 통해서 SQL 문에 악성 코드를 삽입하는 가장 일반적인 *웹 해킹 기술*이다.

</br>

- 데이터베이스를 파괴할 수 있는 코드 주입 기술이다.
- 데이터베이스에 개발자가 의도하지 않은 동적 쿼리(Dynamic Query)를 생성하여 DB 정보를 열람하거나 조작할 수 있는 기술이다.
    - 쿼리는 사용자가 입력한 데이터를 포함하여 동적으로 변하기 때문이다.
- PHP, JSP, ASP 등의 스크립트 언어를 이용하여 DBMS와 연동하는데 이와 같은 웹 애플리케이션은 사용자의 잘못된 입력값을 검증하지 않아 비정상적인 SQL 쿼리를 발생할 수 있다.
    - 이와 같은 비정상적인 쿼리는 사용자 인증을 우회하거나 DB의 데이터를 노출시킬 수 있다.
- 웹 애플리케이션이 데이터베이스와 연동이 되는 로그인, 검색, 게시판과 같은 부분을 특정 SQL Query를 입력하여 비정상적인 결과를 얻는다.

</br>

### **SQL Injection 공격** 방법

#### Error based SQL Injection

- **1=1, ""=""는 항상 참이다.**
- 사용자 로그인 시 입력 값으로 `" or ""="` , `or 1=1` 을 입력하여 SQL 질의문이 항상 올바른 값으로 인식되어 로그인이 가능하게 된다.

```sql
-- 정상 입력
SELECT * FROM Users WHERE id ="John" AND Pass ="myPassWard"

-- 비정상 입력
SELECT * FROM Users WHERE id ="" or ""="" AND Pass ="" or ""=""
```

- `--` 주석을 이용한 방법
- `" or 1=1 --` 을 입력값으로 넣어 WHERE절을 참으로 만들고 뒤의 구문을 모두 주석 처리한다.

```sql
-- 정상 입력
SELECT * FROM Users WHERE id ="John" AND Pass ="myPassWard"

-- 비정상 입력
SELECT * FROM Users WHERE id ="" or 1=1 --" AND Pass ="myPassWard"
```

- 이외의 입력값으로 *`/*, –, ‘, “, ?, #, (, ), ;, @, =, *, +, union, select, drop, update, from, where, join, substr, user_tables, user_table_columns, information_schema, sysobject, table_schema, declare, dual,…` 가 있다.*
- 에러 메시지의 출력으로 DBMS의 정보(DB,TABLE, DATA)를 얻을 수 있다.

</br>

### **SQL Injection 공격 방어**

1. 입력값 검증
    - 입력값이 개발자가 의도한 값인지 검증한다.
2. SQL parameters 사용
    - 매개 변수는 `@marker` 로 SQL문에 표시되어 사용자의 입력값이 SQL의 일부가 아닌 문자 그대로 처리되도록 한다.
3. 서버 보안
    - 에러 메시지 노출 금지
    - 웹 방화벽 사용
</br>

--- 
출처 및 참고

[SQL 주입 (w3schools.com)](https://www.w3schools.com/sql/sql_injection.asp)

[SQL Injection 대응 방안 – PLURA'S BLOG](http://blog.plura.io/?p=6056)

[공격코드 사례분석을 기반으로 한 SQL Injection에 대한 단계적 대응모델 연구 -융합보안논문지 | Korea Science](http://www.koreascience.or.kr/article/JAKO201218553920970.page?&lang=ko)
