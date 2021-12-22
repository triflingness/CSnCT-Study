# DDD
> Domain Driven Design, 도메인 기반 디자인


 애플리케이션을 **비지니스 도메인을 중심으로 나누어 설계하는 방법**입니다.

- 도메인은 실세계에서 사건이 발생하는 집합으로 도메인이 서로 상호작용할 수 있도록 설계합니다.
    - 마케팅, 구매, 연구, 영업,... 등이 예시가 됩니다.
- 서비스별로 도메인이 분리한후, MSA(MicroService Architecture)를 적용하여 설계할 수 있습니다.
- 문맥 `Context(사용자, 상황)`에 따라서 **객체의 역할이 바뀝니다.**
- 같은 객체가 여러 역할을 가질 수 있습니다.
- **핵심 목표 :** 애플리케이션 또는 모듈간의 **의존성은 최소화**하고, **응집성은 최대화**하는 것

## 예시

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/DDD.png" width="700">
</p>

옷 쇼핑몰로 예를 들면, 소비자가 물건을 주문하는 Order Domain이 있고 점주입장에서는 물건을 관리하는 Manage Domain이 있을 수 있습니다.

- `Order Domain` 에서 물건은 소비자 입장에서 필요한  `name, price, color,...`와 같은 정보를
- `Manage Domain` 에서 물건은 관리를 위한 `madeTime, size, madeCountry, ...` 와 같은 정보를 담고 있습니다.

---

[https://happycloud-lee.tistory.com/94](https://happycloud-lee.tistory.com/94)

[https://huisam.tistory.com/entry/DDD](https://huisam.tistory.com/entry/DDD)
