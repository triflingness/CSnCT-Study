# WEB과 WAS

### Web Server

웹 브라우저에서 요청받은 **정적 컨텐츠(html, css, js, 이미지 리소스 등)를 제공하기 위한 서버**

- 클라이언트의 HTTP request를 받아 서비스하는 기능
- ex) Apahce, Nginx, IIS(Windows 전용 Web) 서버, tMax, WebtoB

### WAS

> Web Application Server, 웹 애플리케이션 서버

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/was.png">
</p>

클라이언트 측에서 요청받은 정보를 가지고 연산을 수행한 뒤, **동적인 컨텐츠를 만들어 제공**하기 위한 서버

- asp, php, jsp 등 개발 언어를 처리하여 동적 컨텐츠, 웹 응용 프로그램 서비스를 처리하는 것
- `웹 서버 + 웹 컨테이너` 형태로 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)
    - `Web server` - 정적인 데이터를 처리하거나 동적 컨텐츠 요청(Request)을 전달한다.
    - `Web Container(= Servlet Container)` - JSP, Servlet을 실행시킬 수 있는 소프트웨어
- 주요 기능
    - 프로그램 실행 환경과 데이터베이스 접속
    - 여러 개의 트랜잭션 관리
    - 비지니스 로직 수행
- ex) Tomcat, JBoss, Jeus, Web Sphere

### Web server와 WAS를 구분하는 이유

- 웹 서버 기능을 분리하여 서버의 부하방지
    - 정적 컨텐츠는 Web Server가, 동적 컨텐츠는 WAS가 처리지연을 줄인다.
- 물리적으로 분리하여 보안 강화
- 여러대의 WAS를 연결 가능
    - 로드 밸런싱을 위해 Web Server를 사용
- 여러 웹 애플리케이션 서비스 가능

### Web Service Architecture

웹 서비스를 제공하기 위해 다양한 구조를 가질 수 있다.

1. Client - Web Server - DB
2. Client - WAS - DB
3. Client - Web Server - WAS - DB
    * 규모가 커지면 웹 서버와 WAS를 분리하여 부하를 분산시킨다.(분산처리)
    <p>
      <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/was2.png">
    </p>

---

[https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
