# MPA

> Multi Page Application, 멀티 페이지 애플리케이션

전통적인 웹 애플리케이션 개발방식으로 **서버로부터 완전한 페이지를 받아** 사용자에게 보여주는 웹 애플리케이션이나 웹 사이트

- 특정 페이지에 대한 요청을 하면 서버로부터 정적인 전체 페이지를 데이터로 받는다.
- 전체 페이지를 받으면서 화면이 깜빡이게 된다.
    - 데이터가 많을 경우, 화면에 그려지는 동안 사용자는 기다려야하기 때문에 UX에 좋지 못하다.
    - 비동기 통신으로 어느정도 해소할 수 있었지만, 근본적인 문제는 해결되지 못했다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MPA.jpeg">
</p>

### MPA 특징

1. 페이지 새로고침
    
    특정 페이지가 전환될 때마다 새로운 전체 페이지를 받아 웹 브라우저가 응답한다.
    
<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MPA_rendering.png" width="600">
</p>
    

### MPA 장점

- 검색엔진 최적화(Search Engine Optimization, SEO)에 최적화
    - html에 모든 정보가 다 담아져있기 때문
    - 검색 사이트에 노출이 중요한 사이트는 MPA 구조로 개발하는 것이 좋다.
- 처음 로딩이 짧음
    - 서버가 미리 랜더링하여 전달해준다.

### MPA 단점

- 응답에 대한 페이지 새로고침(깜박임 O)
- 서버 렌더링에 대한 부하
- 프론트엔드와 백엔드가 결합되어 있기 때문에 복잡해지기 쉽고 관리가 어려움

---

[https://seunghyun90.tistory.com/92](https://seunghyun90.tistory.com/92)
