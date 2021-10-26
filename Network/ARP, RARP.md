## ARP

> Address Resolution Protocol

상대방의 논리적 IP주소를 물리적인 MAC주소로 변환시켜주는 프로토콜

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/07692e4305637df9f971ec8f0e0f40facd84f718/Network/imgs/arp.png" width="500">
</p>

- ARP 요청 : 해당 IP주소의 MAC주소를 모르기 때문에 broadcast로 전송한다.
  
- ARP 응답 : 타겟 호스트는 요청자의 MAC주소를 알고 있으므료 unicast로 전송한다.
    
    → 타겟 호스트가 아닌 호스트는 수신한 broadcast 메시지를 폐기한다.
    

### 왜 필요하지?

네트워크 계층에서 노드간에 전송을 하기 위해선 물리적인 주소가 필요하고

물리적인 주소를 알기 위해 사용하는 프로토콜이다.

## RARP

> Reverse ARP

물리적인 MAC 주소를 논리적 IP주소로 변환해주는 프로토콜

자신의 IP주소를 모를때 MAC주소에 대한 IP 주소를 관리하는 **RARP 서버**에게 메시지를 보내어 정보를 얻는다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/07692e4305637df9f971ec8f0e0f40facd84f718/Network/imgs/rarp.png" width="500">
</p>

- RARP 요청 : 자신의 MAC주소만 아는 상태에서 RARP서버의 IP주소 또한 모르기 때문에 broadcast로 전송한다.

- RARP 응답 : RARP Server는 요청자의 IP주소를 담은 메시지를 만들어 요청자의 MAC주소로 unicast한다.

## ARP cache table

시스템은 ARP를 통해 알아낸 IP주소와 MAC주소를 매핑시켜 몇 분 정도 캐시 메모리에 저장한다.

```
[Type 필드]
- dynamic : arp에 의해 동적으로 ip주소가 설정되었으므로 일정 시간 이후 사라진다.  
- static : 관리자에 의해 ip주소가 정적으로 설정된 것으로 시스템을 재부팅하기 전까지 정보가 유지된다.
```  

- `arp -a` : 캐시 테이블 내용 보기
  
- `arp -d` : 캐시 테이블 데이터 완전 삭제
    
    <p>
      <img src="https://github.com/triflingness/CSnCT-Study/blob/07692e4305637df9f971ec8f0e0f40facd84f718/Network/imgs/arp%20-d.png" width="500">
    </p>
    
- `arp -s [IP 주소] [MAC 주소]` : IP주소를 정적(static)으로 설정
    
    <p>
      <img src="https://github.com/triflingness/CSnCT-Study/blob/07692e4305637df9f971ec8f0e0f40facd84f718/Network/imgs/arp%20-s.png" width="500">
    </p>
