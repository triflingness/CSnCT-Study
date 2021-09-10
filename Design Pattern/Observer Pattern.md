# Observer Pattern

객체 사이에 1 대 N의 의존 관계를 정의하여, 어떤 객체의 상태가 변할 때 그 객체에 의존성을 가진 다른 객체들이 그 변화를 통지 받고 자동으로 갱신될 수 있게 만든다.

- 관찰자(observer), 종속자(dependent), 게시- 구독(publish-subscribe) 패턴과 같이 불린다.
- 주제자는 옵저버에 대한 정보가 없어 옵저버가 무슨 동작을 하는지 모른다.
- **느슨한 결합(Loose coupling)** : 두 객체가 느슨하게 결합된 것은 그들이 상호작용을 하지만 서로에 대해 잘 모르는 것을 의미한다.
    - 느슨한 결합의 장점
        - 옵저버를 언제든 새로 추가, 제거할 수 있다.
        - 새로운 형식의 옵저버라 할 지라도 주제를 전혀 변경할 필요가 없다.
        - 주제와 옵저버는 서로 독립적으로 재사용할 수 있다.
        - 주제나 옵저버가 바뀌더라도 서로에게 영향을 미치지 않는다.

### Observer Pattern 구조

- **Subject**
    - 주제를 나타내는 인터페이스
    - 관찰자를 등록하거나 목찰자 목록에서 제거할 때 해당 인터페이스의 메서드를 사용한다.
- **ConcreteSubject**
    - 주제를 구현하는 클래스
    - 관찰자 등록, 제거 메서드와 주제의 상태 변경을 모든 관찰자에게 알리는 메서드가 있다.
- **Observer**
    - 변경을 알림 받는 인터페이스
    - 주제의 상태가 변경될 때마다 해당 인터페이스의 `update` 메서드를 사용한다.
- **ConcreteObserver**
    - Observer 인터페이스를 구현하는 클래스

→ Subject와 Observer가 느슨한 결합을 가진다.

→ Subject에 여러 Observer를 등록해두고, Notify를 하면 루프를 돌면서 각 Observer를 Update하는 패턴이다.

### 사용 예시

**Subject Interface**

```java
public interface Subject {
    void registerOb(Observer o);
    void removeOb(Observer o);
    void notifyOb();
}
```

**Observer Interface**

```java
public interface Observer {
    void update(String newsTitle);
}
```

**ConcreteSubject Class**

```java
public class Press implements Subject {
    private String newsTitle;
    private List<Observer> observers;

    public Press() {
        this.observers = new ArrayList<>();
    }

    @Override
    public void registerOb(Observer o) {
        observers.add(o);
    }

    @Override
    public void removeOb(Observer o) {
        int index = observers.indexOf(o);
        if (index >= 0) {
            observers.remove(index);
        }
    }

    @Override
    public void notifyOb() {
        for (Observer o : observers) {
            o.update(newsTitle);
        }
    }

    public void setNewNewsTitle(String newsTitle) {
        this.newsTitle = newsTitle;
        notifyOb();
    }
}
```

**ConcreteObserver Class**

```java
public class NewsSubscriber implements Observer {

    Subject subject;

    public NewsSubscriber(Subject subject) {
        this.subject = subject;
        subject.registerOb(this);
    }

    @Override
    public void update(String newsTitle) {
        System.out.println("새로운 일반 기사 제목: " + newsTitle);
        System.out.println("업데이트 끝.");
    }

    public void unsubscribe() {
        subject.removeOb(this);
    }
}
```

TEST

```java
public class ObserverPatternTester {

    public static void main(String[] args) {
        ConcreteSubject concretesubject = new ConcreteSubject ();

        NewsSubscriber newsSubscriber = new NewsSubscriber(concretesubject);
        concretesubject .setNewNewsTitle("오늘 날씨는 매우 따뜻합니다.");
        newsSubscriber.unsubscribe();
    }

```

→ 해당 예시는 주제가 관찰자에게 변경 시마다 데이터를 건네는 push 방식이다.

관찰자가 데이터를 가져가는 pull 방식도 있다.

### 장점

- 실시간으로 한 객체의 변경 사항을 다른 객체에 전파할 수 있다.
- 느슨한 결합으로 시스템이 유연하고 객체 간의 의존성을 제거할 수 있다.

### 단점

- 너무 많은 사용은 상태 관리가 힘들 수 있다.
- 데이터 배분에 문제가 생기면 큰 문제로 이어질 수 있다.



> 내장 옵저버 단점  
> 1. 내장 옵저버인 Observable은 인터페이스가 아니라 클래스이다.  
> 재사용성이 제약되어 디자인 패턴의 사용 목적을 상실한다.  
> 2. Observable의 핵심 메서드를 외부에서 호출할 수 없다.  
> setChanged 메서드가 protected로 선언되어, 서브 클래스가 아닌 인스턴스 변수로 사용할 수 없다.  
> -> java.util.Observable을 상속하여 사용할 수 있을 때는 사용해도 괜찮지만, 직접 옵저버를 구현해야 될 수도 있다.



----
참고

[https://coding-factory.tistory.com/710](https://coding-factory.tistory.com/710)

[https://luckygg.tistory.com/181](https://luckygg.tistory.com/181)

[https://velog.io/@hanna2100/디자인패턴-2.-옵저버-패턴-개념과-예제-observer-pattern](https://velog.io/@hanna2100/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4-2.-%EC%98%B5%EC%A0%80%EB%B2%84-%ED%8C%A8%ED%84%B4-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%98%88%EC%A0%9C-observer-pattern)

[https://madplay.github.io/post/observer-pattern](https://madplay.github.io/post/observer-pattern)
[https://2dongdong.tistory.com/47](https://2dongdong.tistory.com/47)
