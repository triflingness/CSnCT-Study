# RESTful API
> Representational state transfer

HTTP 통신에서 자원에 대한 CRUD 요청을 Resource와 Method로 특정한 형태로 전달하는 방식입니다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/CRUD.png" width="700">
</p>

## 장단점

**장점**

- HTTP 프로토콜 인프라를 사용하므로 별도의 인프라를 구축할 필요가 없습니다.

- HTTP 표준을 따르는 모든  플랫폼에서 사용이 가능합니다.  
    → 따라서 멀티 플랫폼 지원이 가능합니다.
    
- 서버와 클라이언트의 역할을 명확하게 구분합니다.

**단점**

- 표준이 존재하지 않아 정의가 필요합니다.

## 특징

HTTP 통신을 사용하므로 HTTP의 특징을 부분 포함합니다.

1. Client-Server 구조
    - 서버와 클라이언트의 역할이 명확해져 의존성이 줄어듭니다.
    - `Server` : API 제공
    - `Client` : 사용자 인증, 컨텍스트(세션, 로그인 정보)등을 직접관리

2. Stateless 방식
    - 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않아 구현이 단순합니다.

3. Uniform (유니폼 인터페이스)
    - URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말합니다.

4. Cacheable (캐시 가능)
    - HTTP가 가진 캐시 사용이 가능합니다. 
    - `Last-Modified` 태그나 `E-Tag`를 이 용하여 캐싱 구현이 가능합니다.

5. Self-descriptiveness (자체 표현 구조)
    - REST API 메시지만 보고 쉽게 이해할 수 있는 구조입니다.

6. 계층형 구조
    - 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 유연성을 갖춥니다.
    - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있습니다.

## 구성 요소

**1. `자원(Resource)`**
* 자원을 구별하는 ID(URI)로 `/group/:group_id` 형태
* 서버에 존재합니다.

**2. `행위(Method)`**
* HTTP 프로토콜의 Method(요청하는 데이터의 특정 동작을 지정)
* GET, POST, PUT, DELETE와 같은 메서드
    - GET: 특정한 리소스를 가져오도록 **요청 (READ)**
    - POST: 새로운 데이터를 **생성 (CREATE)**
    - PUT: 특정한 리소스 **변경 (UPDATE)**
    - DELETE: 특정한 리소스 **제거 (DELETE)**

**3. `자원의 형태(Representation of Resource)`**
* 서버에서 보내는 자원의 형태
* JSON, XML, TEXT, RSS 등

---

[https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)
