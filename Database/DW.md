## DW (데이터 웨어하우스)

> 데이터 웨어하우스, Data Warehouse

Data(데이터) + Warehouse(창고)

**의사결정에 도움을 주기 위해** 데이터베이스에 축적된 데이터를 공통의 형식으로 변환해서 관리하는 데이터베이스

- 각 데이터베이스에서 데이터를 추출 및 변환하여 과거부터 현재까지의 데이터를 축적하고 통합한다.
- 의사결정에 필요한 흩어진 데이터를 한 곳에 모아 분석하기 좋게 사용자에게 제공한다.
- 통계, 분석, 데이터마이닝, ai 등을 통해 분석한 결과를 리포팅한다.

### 특징

1. `주제 지향성(subject-orientation)` - 데이터를 주제별로 구성함으로써 최종 사용자(end user)와 전산에 약한 분석자라도 이해하기 쉬운 형태가 되는 것
2. `통합성(integration)` - 데이터가 데이터 웨어하우스에 들어갈 때는 일관적인 형태(데이터의 일관된 이름짓기, 일관된 변수 측정, 일관된 코드화 구조 등)로 변환되는 것
3. `시계열성(time-variancy)` - 데이터 웨어하우스의 데이터는 일정 기간 동안 정확성을 유지한다.
4. `비휘발성(nonvolatilization)` - 데이터 웨어하우스에 일단 데이터가 적재되면 일괄 처리(batch) 작업에 의한 갱신 이외에는 「Insert」나 「Delete」등의 변경이 수행되지 않는다. 

### 이점

- **통합 분석을 위한 데이터 체계**를 구축한다.
- 표준 지표 / 리포트를 제공한다.
- 사용자 중심의 분석 체계를 구축한다.
- 과거 데이터를 포함해 분석할 수 있다.
- 분석처리 프로세스와 트랜잭션 데이터베이스를 분리하여 성능 향상

### 데이터 웨어하우스 아키텍쳐

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Database/images/data%20warehouse%20archi.png">
</p>

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Database/images/data%20warehouse%20archi2.png">
</p>

- `ETL` - (extract, transform, load) 추출, 변환, 적재
- `데이터 마트` - DW환경에서 정의된 접근계층. 데이터 웨어하우스에서 사업단위의 데이터를 꺼내 사용자에게 제공하는 역할

---

[https://ko.wikipedia.org/wiki/데이터_웨어하우스](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0_%EC%9B%A8%EC%96%B4%ED%95%98%EC%9A%B0%EC%8A%A4)

[https://brunch.co.kr/@qqplot/46](https://brunch.co.kr/@qqplot/46)

[https://pearlluck.tistory.com/275](https://pearlluck.tistory.com/275)
