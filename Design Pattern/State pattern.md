# State Pattern

객체가 특정 상태에 따라 행위를 달리하는 상황에서, 자신이 직접 상태를 체크하여 상태에 따라 행위를 호출하지 않고, 상태를 객체화하여 상태가 행동을 할 수 있도록 위임하는 패턴이다.

- 상태에 따라 동일한 작업이 다른 방식으로 실행될 때 해당 상태가 작업을 수행하도록 위임하는 패턴이다.
- 객체의 특정 상태를 클래스로 선언하고, 클래스에서는 해당 상태에서 할 수 있는 행위를 메서드로 정의한다. 이러한 각 상태 클래스들을 인터페이스로 캡슐화하여, 클라이언트에서 인터페이스를 호출하는 방식이다.

→ 동일 계열의 상태에 따른 조건문이 많아지고, 이러한 코드가 여러 클래스에서 자주 쓰일 때 사용한다.

### State Pattern 구조

<img src="./images/state_pattern_structure.png" width="70%" height="40%">

- **Context**
    - Client가 접근하고, State를 이용하는 인터페이스
    - 현재 상태를 정의하는 ConcresteState 하위 클래스의 인스턴스를 유지한다.
    - setState() 메서드로 각 상태 클래스에서 상태 변경을 요청해 상태를 바꾼다.
    - reqest() 메서드로 실제 행위를 실행하는 대신 해당 상태 객체에 행위 실행을 위임한다.
- **State**
    - 상태를 나타내는 추상 클래스
    - 각 상태에 따른 메서드 인터페이스를 정의한다. (handle()로 표현)
- **ConcreteState**
    - State를 상속 받아 구체적인 상태를 구현하는 클래스

→ 내부 상태 객체들이 캡슐화되어 외부에서 알 수 없다.

### 사용 예시

*디자인 패턴 적용 전*

```java
class Chain {
    private int state;

    public Chain() {
        state = 0;
    }

    public void pull() {
        if (state == 0) {
            state = 1;
            System.out.println( "   low speed" );
        } else if (state == 1) {
            state = 2;
            System.out.println( "   medium speed" );
        } else if (state == 2) {
            state = 3;
            System.out.println( "   high speed" );
        } else {
            state = 0;
            System.out.println( "   turning off" );
        }
    }
}

public class StateDemo {
    public static void main( String[] args ) throws IOException {
        InputStreamReader is = new InputStreamReader( System.in );
        Chain chain = new Chain();
        while (true) {
            System.out.print( "Press 'Enter'" );
            is.read();
            chain.pull();
        }
    }
}
```

**상태 패턴 적용 후**

```java
abstract class State {
    public void pull(Chain wrapper) {
        wrapper.setState(new Off());
        System.out.println("   turning off");
    }
}

// context
class Chain {
    private State current; 

    public Chain() {
        current = new Off();
    }

    public void setState(State state) {
        current = state;
    }

    public void pull() {
        current.pull(this);
    }
}

// concrete state
class Off extends State {
    public void pull(Chain wrapper) {
        wrapper.setState(new Low());
        System.out.println( "   low speed" );
    }
}
// concrete state
class Low extends State {
    public void pull(Chain wrapper) {
        wrapper.setState(new Medium());
        System.out.println("   medium speed");
    }
}
// concrete state
class Medium extends State {
    public void pull(Chain wrapper) {
        wrapper.setState(new High());
        System.out.println("   high speed");
    }
}

class High extends State { }

// client
public class StateDemo {
    public static void main( String[] args ) throws IOException {
        InputStreamReader is = new InputStreamReader( System.in );
        Chain chain = new Chain();
        while (true) {
            System.out.print( "Press 'Enter'" );
            is.read();
            chain.pull();
        }
    }
}
```

### 장점

- 상태 종류 증가에 따른 길어지는 조건문을 제거하고, 가독성 좋게 코드를 짤 수 있다.
- 상태-행위를 묶기 때문에, 클래스 자체는 상태에 따른 행동 구현과 분리된다.

### 단점

- 상태 종류에 따라 클래스가 늘어난다.
- 상태와 행동에 강력한 결합이 생긴다.

---

참고

[https://beomseok95.tistory.com/291](https://beomseok95.tistory.com/291)

[https://dailyheumsi.tistory.com/212](https://dailyheumsi.tistory.com/212)

[https://walbatrossw.github.io/oop/2018/08/28/design-pattern-03-state-patterns.html](https://walbatrossw.github.io/oop/2018/08/28/design-pattern-03-state-patterns.html)

[https://sourcemaking.com/design_patterns/state](https://sourcemaking.com/design_patterns/state)

[https://sourcemaking.com/design_patterns/state/java/3](https://sourcemaking.com/design_patterns/state/java/3)
