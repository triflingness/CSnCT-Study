# BASE

Basically Available, Soft state, Eventually Consistence의 약자, ACID와 대조적으로 가용성과 성능을 중시하는 특성을 가진 분산 시스템의 특성
</br>

❕BASE 속성은 NoSQL의 분산 데이터베이스 환경, ACID 속성은 RDBMS의 일반적인 데이터베이스 환경에 적용한다.
</br>

### BASE 속성

- Basically Available
    - 가용성
    - 부분적인 고장에도 사용할 수 있다.
    - 다수의 저장소에 복사본을 저장한다.
- Soft-State
    - 부드러운 상태
    - 노드의 상태는 외부에서 전송된 정보를 통해 결정된다.
    - 분산 노드 간 업데이트는 데이터가 노드에 도달한 시점에 갱신된다.
- Eventually Consistent
    - 최종 일관성
    - 일시적으로 비일관적인 상태가 되어도 최적으로는 일관성이 있는 상태가 되는 성질을 가진다.
    - 일정 시간 경과 시 데이터의 일관성이 유지되는 속성이다.
</br>

**속성 비교**
|속성|BASE|ACID|
|-|:-:|-|
|적용분야|NoSQL|RDBMS|
|범위|시스템 전체에 대한 특성|트랜잭션에 한정|
|일관성층면|약한 일관성|강한 일관성|
|중점사항|성능과 가용성|무결성과 일관성|
|관리주체|개발자|DBMS 트랜잭션|
|효율성|쿼리 디자인 중요|테이블 디자인 중요|
</br>


---
참고 및 출처

[지식덤프 (jidum.com)](http://jidum.com/jidums/view.do?jidumId=11)
