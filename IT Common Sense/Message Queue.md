# Message Queue(MQ)
> 메시지 큐
> 프로세스 또는 프로그램 인스턴트가 데이터를 주고 받을 때 사용하는 통신 방법


자료구조 Queue를 사용하여 프로세스 또는 프로그램 간에 데이터의 단위인 메시지를 비동기적으로 주고받을 때 사용하는 통신 방법입니다.

메시지 지향 미들웨어(Message-oriented middleware, MOM)를 구현한 시스템입니다.

```
📌 메시지 지향 미들웨어(Message-oriented middleware, MOM)
: 비동기 메시지를 사용하여 응용 프로그램 간 데이터를 송수신하는 시스템
```

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MQ.png">
</p>

MQ는 Producer, Consumer와 Queue가 존재합니다.

비동기로 요청을 처리하고 메시지를 queue에 저장합니다.

- `데이터 전송` : 생산자(Producer)역할의 컴포넌트는 메시지 큐에 message를 추가합니다.
- `데이터 수신` :소비자(Consumer)역할의 컴포넌트는 메시지 큐에서 메시지를 처리합니다.

## MQ 활용

- **IPC(Inter-Process Communication) 도구로 시스템 프로그래밍에서 사용됩니다.**
- **분산 메시징 시스템에 활용됩니다.**

모니터링, 로그, 이벤트 메시지 등 많은 양의 데이터를 다룰 때 사용되기도 합니다.
Producer와 Consumer간의 속도가 다를 때,  둘 중 한 컴포너트가 장애가 발생했을때 사용하여 장애전파를 막을 수 있습니다.
- 이메일 전송에 활용됩니다.
- 블로그 포스팅에 활용됩니다.

## Message Queue 장점

MQ의 장점으로는 비동기, 낮은 결합도, 확장성, 탄력성, 보장성이 있고 소비자 컴포넌트의 병목을 해소해준다는 점이 있습니다.

### 1. 비동기

MQ는 요청을 비동기적으로 처리하여 consumer에서 일어날 병목현상을 해소 할 수 있습니다.

생산된 메시지는 큐에 넣어 보관되기 때문에 나중에 처리할 수 있다.

### 2. 낮은 결합도

생산자 서비스와 소비자 서비스가 독립적으로 수행되므로 서비스간에 결합도가 낮아집니다.

### 3. 확장성

서비스간 결합도가 낮으므로 생산자, 소비자 서비스는 원하는 대로 확장할 수 있습니다.

### 4. 탄력성

소비자 서비스가 중단이 되거나 장애가 오더라도 전체 서비스는 중단되지 않습니다. 요청된 메시지는 메시지 큐에 남아있고 소비자 서비스가 다시 시작될 때 메시지큐를 이용해 남은 메시지를 처리할 수 있습니다.

### 5. 보장성

메시지큐에 저장된 메시지는 소비자 서비스에게 반드시 전달된다는 보장을 제공합니다.

## OSS Message Queue

MQ의 오픈소스 시스템은 RabbitMQ, ActiveMQ, Kafka가 있습니다.

---

메시지 큐 - [https://tecoble.techcourse.co.kr/post/2021-09-19-message-queue/](https://tecoble.techcourse.co.kr/post/2021-09-19-message-queue/)

메시지 큐 종류 - [https://err0rcode7.github.io/backend/2021/06/19/메시지-큐와-종류-그리고-비교.html](https://err0rcode7.github.io/backend/2021/06/19/%EB%A9%94%EC%8B%9C%EC%A7%80-%ED%81%90%EC%99%80-%EC%A2%85%EB%A5%98-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EB%B9%84%EA%B5%90.html)
