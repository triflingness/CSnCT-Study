# SPA

> Single Page Application, 싱글 페이지 애플리케이션
> 

서버로부터 완전한 새로운 페이지를 불러오지 않고 **현재의 페이지를 동적으로 다시 렌더링**함으로써 사용자와 소통하는 웹 애플리케이션이나 웹 사이트

- 서버로부터 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한번만 받는다.
- HTML, 자바스크립트, CSS 등 페이지에 필요한 모든 코드를 하나의 페이지로 불러오거나, 동적으로 해당 이벤트에 대한 자원을 불러들여 문서에 추가하는 방식
- 전통적인 웹 애플리케이션 방식은 전체 페이지를 다시 렌더링하는 방식으로 변경이 필요없는 부분까지 갱신해야하므로 비효율적이다.

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/best-single-page-applications.jpeg" >
</p>

### SPA 특징

1. 라우팅(Routing)
    - 애플리케이션에서 라우팅이란, 사용자가 태스크를 수행하기 위해 어떤 화면(view)에서 다른 화면으로 전환하는 내비게이션을 관리하는 것
    - SPA에서 라우팅은 서버가 아닌 브라우저 단에서 구현해야한다.
    - 요청 URI에 따라 브라우저에서 돔(DOM)을 변경하는 방식
        - 요청 경로에 따라 동적으로 렌더링 되도록 만들면 라우팅에 따라 다른 화면을 구현할 수 있다.
2. 컴포넌트(Component)
    - 특정 부분만 데이터를 바인딩하는 개념
<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/component.png" width="700">
</p>
  
        
    

### SPA 장점

- 단일 페이지로 구성되며 기존의 서버 렌더링과 달리 배포가 간단하며 네이티브 앱과유사한 UX를 제공
- 최초 페이지를 받은 후, 새로운 페이지 요청시, 갱신에 필요한 데이터만 받아 전체적인 트래픽이 감소
- 전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하므로 새로고침이 발생하지 않아 네이티브 앱과 유사한 UX를 제공

### SPA 단점

- 최초 페이지 요청시, 웹페이지에 필요한 모든 정적 리소스를 한번에 받기 때문에 초기 구동 속도가 상대적으로 느리다.
- 서버 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델(Client 렌더린 방식)이기 때문에 검색엔진 최적화(Search Engine Optimization, SEO) 이슈가 있다.

SPA의 핵심 가치는 사용자 경험 향상에 있으며 모바일 퍼스트 전략에 부합하다.

---

[https://ko.wikipedia.org/wiki/싱글_페이지_애플리케이션](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80_%ED%8E%98%EC%9D%B4%EC%A7%80_%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98)
