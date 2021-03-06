# OAuth

> 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, **접근 위임을 위한 개방형 표준**

- 인증(Authentication)과 권한(Authorization)을 획득하는 것
- 인증은 시스템 접근을 확인하는 것 (로그인) -> 인증만 하는 것은 openID
- 권한은 행위의 권리를 검증하는 것

## OAuth 2.0

> 서비스간 인증정보 공유 > 하나의 인증 서비스로 여러 서비스의 인증을 지원

- API 호출 시 사용자에게 비밀번호를 요구하지 않아도 됨

### 구성

- **Client** (커뮤니티 서비스): 리소스에 접근하려고 하는 주체, 서비스 제공자에 있는 특정 정보에 접근하여 사용하고자 한다.
- **Resource** (유저 정보, 이메일, 이름): 서비스 제공자에 저장된 정보.
- **Resoure Owner** (커뮤니티 사용자): Client에 제공하는 정보를 가지고 있는 사람. 여기서는 이메일과 이름을 제공해서 편리하게 로그인하고 싶어 하는 커뮤니티 사용자.
- **Service Provider** (구글, 네이버): 리소스를 저장하고 있는 제3의 주체. Client가 여기에 저장된 정보에 접근하고자 한다. 보통 구글이나 페이스북같이 큰 기업이 많다.

### OAuth 2.0 인증과정

![OAuth 2.0 인증과정](./images/OAuth%202.0%20인증과정.png)

### OAuth 2.0 프로세스

![OAuth 2.0 프로세스](./images/OAuth%202.0%20프로세스.png)

1~5 단계는 Authorization Code 발급 요청 URL을 통해 진행할 수 있습니다.

7~8 단계는 서비스에서 callback URL 을 통해 전달받은 Authorization Code를 사용하여 Access Token 요청 API를 통해 진행할 수 있습니다.

8 단계에서 발급받은 Access Token은 서비스에서 자체적으로 저장, 관리해야 합니다.

10~11 사용자의 서비스 요청 시 회원정보가 필요하다면 Access Token을 사용해 API를 호출할 수 있습니다.

## OAuth 1.0과 차이

- **기능의 단순화, 기능과 규모의 확장성 등을 지원**하기 위해 만들어 짐
- 1.0a는 만들어진 다음 표준이 된 반면 **2.0은 처음부터 표준 프로세스로 만들어짐**
- **https가 필수**여서 간단해 졌다.
- **암호화는 https에 맡김**
- 1.0a는 인증방식이 한가지였지만 2는 **다양한 인증방식을 지원**한다.
- **api서버에서 인증서버를 분리** 할 수 있도록 해 놓았다.

##### 참고

- [https://gdtbgl93.tistory.com/180](https://gdtbgl93.tistory.com/180)
- https://gdtbgl93.tistory.com/181?category=905944
