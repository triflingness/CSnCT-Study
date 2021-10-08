# TCP Wrapper

> 서비스별 접근 제어

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/0287c4b271552db2a15d9881e8b617b27399d383/Linux/imgs/tcpwrapper.png" width="700">
</p>

외부 클라이언트의 정보를 기반으로 서비스의 접근 허용, 차단을 한다.

- 클라이언트의 host명, IP주소를 확인하여 허용된 호스트만 서비스를 허용하기 때문에 외부의 침입으로부터 시스템을 보호할 수 있다.
- 사용할 서비스는 `/etc/inetd.conf` 파일에 서비스 실행경로를 `/usr/sbin/tcpd` 로 바꿔준다.
    
  <p>
    <img src="https://github.com/triflingness/CSnCT-Study/blob/0287c4b271552db2a15d9881e8b617b27399d383/Linux/imgs/inetd.conf_tcpd.png" width="700">
  </p>
    

✔️ 다음과 같은 파일을 판단의 우선순위로 둔다.

1. `/etc/hosts.allow` 
2. `/etc/hosts.deny` 
3. default action : 모두를 허용한다.

`hosts.allow` 에 정보가 없다면 `hosts.deny` 파일을 참조하고 해당정보가 없다면 default로 모든 접근을 허용한다.

## hosts.allow와 hosts.deny

### 파일 구문 형식

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/0287c4b271552db2a15d9881e8b617b27399d383/Linux/imgs/Syntax_hosts.allow_deny%20.png" width="700">
</p>

✔️ **예약어**

- ALL : 모든 호스트 or 모든 서비스
- LOCAL : 같은 네트워크에 있는 모든 호스트
- B EXCEPT A : 리스트 B에서 A를 제외한 모든 B

✔️ **shell_command**

- 접근 통제 리스트(ACL)에 일치하는 것이 있으면 실행하는 명령
- 주로 hosts.deny 파일에 설정해서 차단된 호스트에게 통보나 경고 메시지를 보낼 때 사용한다.
- 2가지 종류
    - `twist` : 명령의 결과를 클라이언트에게 전달한다.
    - `spawn` : 명령의 결과를 클라이언트에게 전달하지 않는다.

✔️ **예시(hosts.deny)**

- `in.telentd : 192.168.0.104 : twist /bin/echo "192.168.0.104 연결이 거부되었습니다!!"`
    - `192.168.0.104` 클라이언트의 Telent 서비스를 거부하고 클라이언트에게 `192.168.0.104 연결이 거부되었습니다!!` 메시지를 전송한다.
- `in.telentd : 192.168.0.104 : spawn /bin/mail -s "192.168.0.104 연결이 거부되었습니다!!" root`
    - `192.168.0.104` 클라이언트의 Telent 서비스를 거부하고 root에게 `192.168.0.104 연결이 거부되었습니다!!` 내용의 메일을 전송한다.

### 예시

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/0287c4b271552db2a15d9881e8b617b27399d383/Linux/imgs/hosts.allow_example.png" width="700">
</p>
