# 서비스 거부 공격 (DoS, Denial of Service)

타겟 시스템의 가용성을 떨어트려 정상적인 서비스를 할 수 없게 만드는 공격입니다.

### 공격 유형

- 네트워크 대역폭(Bandwidth)을 소진시켜 네트워크 자원 소진시킵니다.
- CPU, 메모리, 디스크처럼 시스템 자원을 소진시킵니다.
- 디스크나 데이터, 시스템을 파괴시킵니다.

## 1. Ping of Death 공격

> 재조합에 부하를 많이 발생시켜서 타겟의 가용성을 떨어트린다!

ICMP 패킷을 정상적인 크기보다 아주 크게 만들어 전송합니다.

MTU에 따라 IP 단편화가 대량으로 발생하게 되어 타겟 시스템은 대량의 IP 프래그먼트를 수신하게 됩니다.

타겟 시스템은 수신한 패킷을 재조합하는 과정에서 부하가 생기므로 재조합 버퍼의 오버플로우가 발생하면 정상적인 서비스를 하지 못하게 됩니다.

```
📌 MTU (Maximum Transmission Unit)

- 네트워크 프로토콜의 Payload의 최대크기
- ex) 이더넷의 MTU : 1500byte
```

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/pingofdeath.png" width="700">
</p>

### 대응책

- 탐지 : 보통 ICMP 패킷은 분할하지 않으므로 분할이 일어난 패킷을 공격으로 의심합니다.
- 대응 : 일정 수 이상의 ICMP 패킷을 받으면 무시합니다.

## 2. Land Attack

> Src IP = Dst IP

스푸핑한 타겟의 IP 주소를 출발지 IP 주소와 목적지 IP 주소로 설정하여 패킷을 타겟에게 전송합니다.

수신한 타겟 시스템은 자신에게 응답을 보내면서 스스로 시스템 가용성을 침해합니다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/land_attack.png" width="700">
</p>

### 대응책

- 탐지 : Source IP 주소와 Destination IP 주소가 같은 패킷을 의심합니다.
- 대응 : 방화벽에서 Source IP 주소와 Destination IP 주소가 같은 패킷은 모두 Drop 합니다.

## 3. Smurf Attack🌟

> DRDos의 한 형태

타겟의 IP주소를 출발지 IP 주소로 스푸핑하고 목적지 IP 주소는 증폭 네트워크의 Broadcast IP로 설정합니다.

증폭 네트워크로 ICMP Echo Request를 브로드캐스트 하면 타겟은 다수의 ICMP Echo Reply를 받아 부하가 발생하게 됩니다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/smurf_attack.png" width="700">
</p>

### 대응책

- 탐지 : 단시간에 다수의 ICMP Echo Reply 패킷이 발생했을 때 공격으로 의심합니다.

- 대응 : 침입차단 시스템, 라우터, 시스템 관점에서 대응할 수 있습니다.

  - 침임차단 시스템에서 탐지되었을때 들어오는 패킷을 모두 drop 시킵니다.

  - 자신의  PC가 증폭 네트워크로 사용되는 것을 막기 위해 다른 네트워크로부터 자신의 네트워크로 들어오는 Directed Broadcast 패킷을 허용하지 않게 됩니다.
      - 라우터 명령어: `# no ip directed-broadcast`

  - 브로드캐스트로 전송된 ICMP Echo Request 메시지에 대해 응답하지 않도록 시스템 설정을 합니다.
      - 커널 파라미터 설정 : `sysctl -w net.ipv4.icmp_echo_ignore_broadcasts=1`

## 4. Teardrop  Attack

> offset 조작

IP 패킷의 offset값을 분할된 IP 패킷과 서로 중첩시켜 타겟 시스템에게 전송을 합니다.

이를 수신한 타겟 시스템은 재조합하는 과정에서 시스템 오류와 부하가 발생하게 됩니다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/teardrop_attack.png" width="500">
</p>

### 대응책

- 탐지 : 처음 IP 패킷 조각의 길이와 마지막 패킷의 길이와 offset정보를 비교해서 탐지합니다.

- 대응 : OS의 보안패치를 모두 설치하여 OS의 취약점을 해소합니다.
