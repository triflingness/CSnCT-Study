# inetd 데몬
> 슈퍼 데몬

## 탄생 배경

네트워크 Client-Server구조의 서비스는 실제 서비스를 제공하는 **서비스 프로세스**와 공통적으로 Client의 요청을 기다리는 **리스닝 프로세스**로 이루어져 있다.
다수의 서비스가 만들어지면 같은 리스닝 프로세스가 만들어져 서버의 자원을 불필요하게 많이 차지한다.

이를 해결하기 위해 슈퍼데몬을 두어 공통적인 기능을 수행한다.
슈퍼데몬은 client의 request를 받아 개별 서비스를 호출해주는 방식으로 동작한다.

- Stand-Alone 방식 : 개별 서비스마다 서버 프로세스(데몬)가 동작하는 방식
    - (장점) 속도가 빠름. (단점) 서버 리소스를 많이 점유한다.

- inetd(xinetd) 방식 : 슈퍼데몬(inetd 데몬)을 이용하여 개별 서비스를 동작하는 방식
    - (장점) 서버 리소스를 절약. (단점) 상대적으로 속도가 느림.

## inetd 데몬

여러개의 개별 서버를 하나로 통합하여 client의 request가 올 때마다 서비스의 해당 모듈을 실행시킨다.

- `/etc/inetd.conf` 파일을 참고하여 최초 실행 시 서비스할 프로그램들에 대한 정보를 얻는다.  

    → **inetd.conf 파일이 수정되었을 시 inetd데몬을 껐다가 재시작해줘야한다.**
    
- **TCP Wrapper 서비스(tcpd)** 와 연동하여 서비스별 호스트 접근 제어를 할 수 있다.

- 리눅스의 경우, xinetd 데몬을 주로 사용한다. xinetd는 inetd에서 보안과 리소스 관리 등을 향상시킨 것. 주 기능에는 큰 차이 없다.

## /etc/inetd.conf 파일

```
ftp    stream tcp   nowait   root   /usr/sbin/in.ftpd     in.ftpd    -l -a
telnet stream tcp   nowait   root   /usr/sbin/in.telnetd  in.telnetd
```

(서비스명) (소켓타입) (프로토콜) (플래그) (사용할 사용자 계정) (실행 경로명) (실행 인수)

- `서비스명` : 서비스명을 참고하여 `/etc/services` 파일에 등록된 포트번호를 결정한다.
- `소켓타입` : TCP 기반은 stream을, UDP기반은 dgram을 명시한다.
- `프로토콜` : `/etc/protocols` 파일에 주어진 프로토콜을 설정한다. /etc/services 파일에 명시된 프로토콜과 일치해야한다.
- `플래그` : nowait(요청을 받은 즉시 처리함-TCP) / wait(이전 요청처리가 완료되고 다음 요청을 처리함-UDP)
- `사용할 사용자 계정` : 프로그램을 실행시킬 사용자를 설정한다.
- `실행 경로명` : 실행 모듈의 **절대경로**
- `실행 인수` : 프로그램의 인수를 설정. 첫 번째 실행인자는 응용 프로그램 자신의 이름이 된다.



## 📌 불필요하고 취약한 서비스는 비활성화해야한다.

### 비활성화해야하는 서비스 리스트

- Dos 공격에 취약한 Simple TCP 서비스
    - echo(7/tcp)
    - discard(9/tcp)
    - daytime(13/tcp)
    - chargen(19/tcp)

- r 계열 서비스
    - rlogin, rsh, rexec, ....
    - **인증없이 관리자의 원격접속을 가능**하게 하는 명령어들

- rpc 서비스 (remote procedure call)
    - 분산환경에서 서버 애플리케이션에 접근하여 작업 호출을 할 수 있는 서비스
    - 버퍼 오버플로우 등 취약점이 존재함

- finger, tftp, talk 등의 서비스

### 비활성화 방법

1. `/etc/inetd.conf` 에서 취약 서비스를 주석처리(#)하거나 제거한다.
2. 변경된 inetd.conf 파일을 적용하기 위해 inetd 데몬을 재시작한다.

```
#echo    stream tcp   nowait   root   internal
#discard stream tcp   nowait   root   internal
...
```
