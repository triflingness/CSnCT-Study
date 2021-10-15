# PAM

> 장착형 인증 모듈, Pluggable Authentication Module

**각종 어플리케이션의 인증**을 위해 **다양한 인증 라이브러리**의 모임

- 일반적으로 `/lib/security` 또는 `/usr/lib/security` 에 해당 라이브러리가 저장되어 있다.
- 플러그인 방식으로 기존 응용 프로그램을 수정할 필요없이 새로운 인증 서비스 모듈을 추가하거나 사용할 수 있다.
- (장점) 플러그인 방식의 PAM을 사용함으로써 **인증 방식 및 정책의 유연성과 중앙통제가 가능**하다.

## PAM 라이브러리 관련 경로

- `/etc/pam.d` : PAM을 이용하려는 각  **애플리케이션의 PAM 설정 파일들**이 위치한다.
- `/lib/security` : PAM이 제공하는 **인증 모듈 라이브러리**가 담겨있다.
- `/etc/security` : PAM 모듈 실행에 필요한 **추가 설정 파일**이 담겨있다.

### /etc/pam.d 속성

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/4bbfe5ca21587d1fa3d59e386f291f06a5173280/Linux/imgs/pamd.png" width="600">
</p>

**type** | **control** | **module-path** | **module-arguments**

- `type` : (**PAM 모듈 종류**) account | auth | password | session
    - `account`(계정) : 계정의 유효성을 검증하는 유형
    - `auth`(인증) : 계정의 패스워드, 다른 인증 모듈과의 연동으로 신원확인을 한다.
    - `password` : 계정의 비밀번호를 지정하는 유형
    - `session` : 계정 인증처리 전후에 수행할 작업을 지정하는 유형.

- `control` : (**모듈 성공, 실패에 따른 행동**) requisite | required | sufficient | optional
    - `requisite` : 인증 실패시 즉시 인증 거부
    - `required` : 인증에 실패하더라도 다음 라인의 모듈을 실행한다. 하지만 required에 하나라도 실패한다면 인증 결과는 실패한 것이다.
    - `sufficient` : 이전에 요청된 모듈이 실패하더라도 sufficient 인증에서 성공하면 PAM 인증 결과는 성공이다. 단, 이전의 sufficient가 모두 성공했어야 한다.
    - `optional` : 모듈의 성공, 실패 결과는 모두 무시된다.

- `module-path` : (모듈파일 경로) 모듈이름만 명시할 경우, PAM 모듈 디렉터리(/lib/security)에서 찾는다.

- `module-arguments` : (인수) 모듈에게 전달되는 인수
