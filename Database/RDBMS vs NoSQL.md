# RDBMS vs NoSQL

### RDBMS

- **관계형 데이터베이스 관리 시스템(Oracle, MySQL)**
- 2차원 테이블로 `Attribute와 Value`를 사용하는 데이터베이스
- 테이블 간의 관계를 가지고 이렇게 보관된 데이터들을 `SQL`을 사용해서 활용한다.
- 데이터 중복을 줄이는 것이 목적이고 일반적으로 조인을 필요로 한다.
- **장점**
    - 엄격한 사전 정의된 스키마에 맞춰 데이터를 저장하기에 명확한 데이터 구조를 보장한다.
    - 각 데이터를 중복없이 한번만 저장할 수 있다.
- **단점**
    - 시스템이 커질 수록 JOIN문이 많은 쿼리가 복잡해지고 성능이 저하된다.
    - 수평적 확장(서버 전체의 확장, **scale-out**)이 어려워 수직적 확장(기존 서버의 교체, **scale-up**)만을 지원한다.

</br>

### NoSQL

- **Not Only SQL(몽고DB)**
- 테이블 간의 관계를 정의하지 않고 정해진 스키마가 없다.
- RDBMS로 처리할 수 없을 정도의 크고 복잡한 데이터들을 관리한다.
- `Key와 Value`만으로 데이터 관리를 한다.(JSON문서, 키값, 그래프)
- 빠른 애플리케이션 변경과 확장을 목적으로 두고 일반적으로 조인을 필요로 하지 않는다.
- 장점
    - 유연한 데이터 모델:  스키마가 없어 비정형 데이터를 보다 자유롭게 조작할 수 있다.
    - 성능 향상을 위한 scale-up, scale-out 모두 가능하다.
    - 빠른 쿼리: 조인을 필요로 하지 않아 쿼리가 빠르다.
- 단점
    - 중복된 데이터가 추가 가능하여, 이에 대한 관리가 필요하다.
    - ACID 트랜잭션을 지원하지 않는다.
    - 데이터베이스의 유형에 따라 단일 데이터베이스에서 모든 use case를 구현하지 못 한다.

</br>

---
참고 및 출처

[RDBMS와 NoSQL의 차이점 완벽 정리 (universitytomorrow.com)](https://universitytomorrow.com/26)
[NoSQL vs Relational Databases | MongoDB](https://www.mongodb.com/scale/nosql-vs-relational-databases)
[NoSQL vs SQL Databases | MongoDB](https://www.mongodb.com/nosql-explained/nosql-vs-sql)
