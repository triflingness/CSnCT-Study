# SSL/TLS

TCP 기반 Application에 대한 **End-to-End 보안 서비스**를 제공하는 전송계층 보안 프로토콜입니다.

IPv4는 기밀성을 유지하지 못한다는 단점을 보완하기 위해 개발되었습니다.

SSL/TLS는 IPsec에 기본으로 들어가는 layer이기에 IPv6는 SSL/TLS를 기본적으로 포함합니다.

Client-Server 구조에서 서버와 클라이언트 사이에 기밀성을 유지하기 위해 사용되는 전송계층 보안 프로토콜

```
📌 용어 정리

- SSL(Secure Socket Layer) : 1994년 넷스케이프사에서 처음으로 개발하였습니다.

- TLS(Transport Layer Security) : SSL 3.0버전을 기반으로 표준화된 TLS 1.0버전이 탄생하였고 2018년 TLS 1.3버전까지 발표되었습니다.
```

## 서비스

- 기밀성(Confidentiality) : `대칭암호`를 이용하여 송수신 메시지를 암호화합니다.
- 무결성(Integrity) : `메시지 인증 코드(MAC)`를 이용하여 송수신 메시지의 위변조 여부를 알 수 있습니다.
- 인증(Authentication) : `공개키 인증서`를 이용하여 종단간 상호 인증을 할 수 있습니다.

## 프로토콜 구조

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/TLS%20structure.png" width="700">
</p>

- SSL/TLS 층은 2개의 층, 제어 프로토콜과 레코드 프로토콜로 나눠집니다.
- 제어 프로토콜은 SSL 동작에 대한 관리를 하기 위한 프로토콜이고 레코드 프로토콜은 실제 데이터가 메시지를 송수신하는 프로토콜입니다.
- 제어 프로토콜
    - `Handshake 프로토콜` : 보안 파라미터(암호 알고리즘, key분배) 를 협상하기 위한 프로토콜
    - `Change Cipher Spec 프로토콜` : 협상한 암호 스펙을 이후부터 적용함을 알리기 위한 프로토콜
    - `Alert 프로토콜` : 통신 과정에서 발생하는 오류를 알려주기 위한 프로토콜
    - `Application Data 프로토콜` : Application 계층의 데이터를 전달하기 위한 프로토콜
- 레코드 프로토콜
    - `Record 프로토콜` : 실질적인 데이터의 송수신 기능을 하는 프로토콜(암호화/복호화, 무결성 보호, 압축/압축해제 기능을 수행)
