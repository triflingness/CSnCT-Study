# TCP 3way & 4way handshaking
TCP의 연결을 성립하고 해제하는 과정을 말합니다.

## 3 way handshaking - 연결 설정

3-way handshaking은 논리적인 접속을 성립하기 위해 세션을 수립하여 정확한 전송을 보장해줍니다.

상대편에 대한 초기 순차일련번호를 얻어 신뢰성 있는 전송을 위한 준비과정입니다.

> **SYN - SYN/ACK - ACK**

<p >
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/3way-handshaking.png" width="700">
</p>

1. 클라이언트가 서버에게 `SYN` 패킷을 보내어 서버 접속을 요청한다. (# SEQ : x)
    - 상태) 클라이언트는 서버에게 `SYN/ACK` 패킷을 기다리는 `SYN_SENT` 상태가 된다.

2. 서버는 `SYN` 요청을 받고 클라이언트에게 `SYN/ACK` 패킷을 보내어 요청을 수락한다. (#SEQ : y, #ACK : x+1)
    - 상태) 서버는 요청을 수락한 `SYN_RECEIVED` 상태가 된다.

3. 클라이언트는 서버에게 `ACK` 패킷을 보내어 수락을 확인했다고 알린다. (#ACK : y+1)
    - 서버와 클라이언트는 `ESTABLISHED` 상태로 연결이 성립되고 이후 데이터 통신을 한다.
    

3번의 과정을 통해 세션이 성립이 되고 신뢰성 있는 연결을 보장해줍니다.

## 4 way handshaking - 연결 해제

4-way handshaking은 세션을 종료하기 위해 수행되는 절차입니다.

> **FIN - ACK - FIN - ACK**

<p >
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/Network/imgs/4way-handshaking.png" width="700">
</p>

1. 클라이언트가 서버에게 연결을 종료한다는 `FIN` 패킷을 보낸다.

2. 서버는 확인했다는 `ACK` 패킷을 보낸다.
    - 이때 서버는 `CLOSE_WAIT` 상태가 되어 자신의 통신이 끝날때까지 기다린다.

3. 서버는 통신이 끝나면 클라이언트에게 연결이 종료되었다고 `FIN` 패킷을 보낸다.

4. 클라이언트는 `FIN` 패킷을 받고 서버에게 확인했다는 `ACK` 패킷을 보낸다.
    - 서버로부터 받지 못한 데이터가 있을 수 있으므로 `TIME_WAIT` 과정을 통해 기다린다.
    - 서버는 `ACK` 패킷을 받은 후 소켓을 닫는다. (`Closed`)
    - 클라이언트는 `TIME_WAIT` 시간이 끝나면 소켓을 닫는다. (`Closed`)

4번의 과정을 통해 통신이 완료되면 TCP 세션 연결이 해제됩니다.
