# 가상 사설망(VPN : Virtual Private Network)

> 공중망 내에서 마치 전용선을 사용하는 기술

- 공중망을 공유하기 때문에 비용이 낮다.
- 터널링 프로토콜과 보안과정을 거쳐 보안성이 우수하다.

### 터널링

> 송신자와 수신자 사이의 전송로에 외부로부터 침입을 막기 위해 일종의 파이프를 구성한 것

- 사설망과 같은 **보안 기능**을 지원한다.
- 데이터 암호화, 사용자 인증, 사용자 액세스 권한&제한, 라우터 체계 비공개
- 페이로드는 **캡슐화**되어 전송된다.

## 프로토콜 종류

### 1. PPTP(Point to Point Tunnel Protocol)

> 지원계층 : 2계층(Data link Layer)

- 마이크로 소프트사가 설계
- PPP(Point to Point Protocol)의 Packet을 **IP Packet으로 캡슐화**하여 전송한다.
- **일대일** 통신만 가능

### 2. L2F(Layer 2 Forwarding)

> 지원계층 : 2계층(Data link Layer)

- 시스코(Cisco Systems)사에서 제안
- 원격지 사용자의 home site에서 주소를 할당하며 home site의 게이트웨이에서 사용자 인증을 한다.
- **다자간 통신**을 지원
- RADIUS와 TACACS+를 이용해서 인증

### 3. L2TP(Layer 2 Tunneling Protocol)

> 지원계층 : 2계층(Data link Layer)

- 마이크로 소프트와 시스코에서 제안
- L2F 기반으로 설계되었고 PPTP와 호환성을 고려하여 개발
- X.24, ATM, FrameRelay와 같은 WAN 기술도 지원

### 4. IPsec(IP Security)

> 지원계층 : 3계층(Network Layer)

- IP망에서 안전한 전송을 위한 표준화된 3계층 터널링 프로토콜
- IETF에 의해 제안되어 VPN 구현에 가장 널리 사용되고 있음
- IP 데이터그램의 **인증**, **무결성**과 **기밀성**
- IP 계층에서 서비스를 직접 제공하기 때문에 상위 계층이 변경될 필요가 없음
- 암호화된 패킷은 IP패킷과 동일한 형태이기 때문에 쉽게 라우팅이 가능
