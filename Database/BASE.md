# BASE

Basically Available, Soft state, Eventually Consistence의 약자, ACID와 대조적으로 가용성과 성능을 중시하는 특성을 가진 분산 시스템의 특성

❕BASE 속성은 NoSQL의 분산 데이터베이스 환경, ACID 속성은 일반적인 데이터베이스 환경에 적용한다.

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




---
참고 및 출처

[지식덤프 (jidum.com)](http://jidum.com/jidums/view.do?jidumId=11)
