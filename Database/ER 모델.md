# ER 모델 (Entity Relationship)

→ 데이터베이스 설계를 용이하게 하기 위해서  P.P Chen이 1976년 제안했다.

✔️ 의미적으로 풍부한 데이터 모델을 제공하고, 개념들을 그래픽하게 나타낼 수 있으며, 네트워크 데이터 모델, 관계 데이터 모델, 엔티티 집합 모델의 좋은 특성들을 결합하기 위한 것이다.

### ER 모델은

- 물리적인 데이터베이스 설계의 효율성에 관심을 두지 않으면서 한 조직의 개념적 스키마를 설명하기 위해 사용된다.
- 실세계를 엔티티, 애트리뷰트, 엔티티들 간의 관계로 표현한다.
- ER 모델을 기반으로 만들어진 다수의 CASE 도구들이 존재한다. 데이터베이스 설계 시간과 비용을 감소시키고, 데이터베이스 설계 방법론을 표준화하며, CASE 도구를 사용하여 개발된 응용 시스템의 유지 보수를 용이하게 한다.

→ 대규모 기업의 데이터베이스 설계에서는 UML(Unified Modeling Language)을 사용한다.

### ER 모델 구성 요소

<img src="./images/EERD표기법.jpg" width="60%" height="40%">

- 엔티티 __Entity__ : 사람, 장소, 사물, 사건 등과 같이 독립적으로 존재하면서 고유하게 식별이 가능한 실세계의 객체이다. 
- 엔티티 타입 __Entity Type__ : 연관된 개체들의 집합이다. (네모) 
    - 정규 엔티티 타입(강한 엔티티 타입) : 독자적으로 존재하며 엔티티 타입 내에서 자신의 키 애트리뷰트를 사용하여 고유하게 엔티티들을 식별할 수 있는 엔티티 타입이다.
    - 약한 엔티티 타입 : 키를 형성하기에 충분한 애트리뷰트들을 갖지 못한 엔티티 타입이다. (이중선 네모, 해당 타입의 부분 키는 점선 밑줄)
        - 소유 엔티티 타입이 있어야만 약한 엔티티 타입이 존재할 수 있다. 소유 엔티티 타입의 키 애트리뷰트를 결합해야만 고유하게 약한 엔티티 타입의 엔티티들을 식별할 수 있다.
        - 자체적으로 키를 보유하지 못한 엔티티이다. 엔티티들을 식별하기 위해서 다른 엔티티 타입으로부터 키 애트리뷰트를 가져오는 엔티티 타입이다.
        - 이때 키 애트리뷰트를 제공하는 엔티티 타입을 소유 엔티티 타입 또는 식별 엔티티 타입이라고 한다.
- 애트리뷰트 __Attribute__ : 개체가 갖는 속성이다. (원)
    - 단순 애트리뷰트 : 더 이상 다른 애트리뷰트로 나눌 수 없는 애트리뷰트이다.
    - 복합 애트리뷰트 : 두 개 이상의 애트리뷰트로 이루어진 애트리뷰트이다.
    - 키 애트리뷰트 : 다른 개체들과 중복되지 않는 고유한 값을 가진 애트리뷰트이다. (밑줄 원)
    - 다치 애트리뷰트 : 각 엔티티마다 여러 개의 값을 가질 수 있는 애트리뷰트이다. (이중선 원)
    - 유도된 애트리뷰트 : 다른 애트리뷰트의 값으로부터 얻어진 애트리뷰트이다. (점선 원)
- 관계 __Relationship__ : 엔티티 타입간의 관계이다. (마름모)
    - 카디날리티 비율 : 관계를 맺는 두 개체 간의 수적 비율, 한 개체가 몇 개의 다른 개체와 연관되는가를 나타내는 제약조건이다.
        - 일대일(1:1) : 두 엔티티 타입의 개체들이 서로 일대일로 연관됨
        - 일대다(1:N) : 하나의 개체가 다른 엔티티 타입의 많은 개체들과 관련되지만, 그 역은 성립하지 않음
        - 다대다(N:N) : 하나의 개체가 다른 엔티티 타입의 많은 개체들과 관련되며, 그 역이 성립
    - 참여 제약 조건 : 관계를 맺는 두 Entitiy Type에 대한 개체의 존재가 다른 개체의 존재에 의존하는지 여부를 나타내는 제약 조건이다.
        - 전체 참여 : 하나 또는 그 이상의 개체가 참여 (이중 실선)
        - 부분 참여 : 선택적인 참여 (한 개의 실선)
    
### 새발 표기법
<img src="./images/새발표기법.png" width="60%" height="60%">

---
참고  
[[DB이론] ER 모델( Entity Relation Model ) - 개념적 설계 :: victolee (tistory.com)](https://victorydntmd.tistory.com/126)
