# DB lock

데이터의 일관성을 보장하기 위한 방법

- 트랜잭션의 처리 순차성을 보장하기 위한 방법이다.
- 하나의 트랜잭션이 완벽하게 끝날 때까지 다른 요청을 막는다.

</br>

### DB lock의 종류

- **공유 락(Shared Lock, Read Lock)**
    - 데이터를 읽을 때 사용한다. (*SELECT*)
    - 다른 트랜잭션이 같이 읽는 것을 허용하지만 변경하는 것은 허용하지 않는다.
    - 공유 잠금이 설정된 동안은 여러 트랜잭션이 동시에 하나의 데이터를 읽을 수 있다.
- **배타 락(Exclusive Lock, Write Lock)**
    - 데이터를 변경할 때 사용한다. (*INSERT, UPDATE, DELETE*)
    - 다른 트랜잭션이 읽는 것, 변경하는 것 모두 허용하지 않음
    - 한 트랜잭션만이 잠금된 데이터를 사용할 수 있다.

</br>

### Lock 단위(범위, Level)

- RID : 하나의 행을 잠글 때 사용 (ROW)
- KEY : 인덱스가 있을 때의 행을 잠글 때 사용
- PAGE : 8kb 데이터 페이지 또는 인덱스 페이지
- EXTENT : 인접한 8개의 데이터 페이지 또는 인덱스 페이지
- TABLE : 데이터와 인덱스가 포함된 전체 테이블 (DDL LOCK-CREATE, ALTER, DROP)
- DB : 데이터베이스

</br>

---
참고 및 출처

[[DB] Lock이란?. DBMS에서 데이터의 일관성을 보장하기 위한 기본적인 방법인 Lock에… | by chrisjune | Medium](https://chrisjune-13837.medium.com/db-lock-%EB%9D%BD%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-d908296d0279)
[[데이터베이스] Lock에 대해서 알아보자 - 기본편 (tistory.com)](https://sabarada.tistory.com/121)
