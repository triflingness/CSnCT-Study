# Singleton

- 전역 변수를 사용하지 않고 **객체를 하나만 생성**하도록 하며, 생성된 객체를 **어디에서든지 참조 할 수 있도록 하는 디자인 패턴**
- **한 클래스에 한 객체만 존재**하도록 제한
- **하나의 인스턴스만을 생성**하는 책임이 있으며 `getInstance` 메서드를 통해 모든 클라이언트에게 **동일한 인스턴스를 반환**하는 작업을 수행

## 예제

- **static 메서드 / static 변수**
    - 구체적인 인스턴스에 속하는 영역이 아니고 **클래스 자체에 속함**
    - 클래스의 인스턴스를 통하지 않고서도 메서드를 실행할 수 있고 변수를 참조할 수 있음
- 만약 `new Printer()`가 호출되기 전이면 인스턴스 메서드인 `print()`메서드는 호출할 수 없음

```java
public class Printer {
  // 외부에 제공할 자기 자신의 인스턴스
  private static Printer printer = null;

  private Printer() { }  // private으로 선언: Printer 생성자를 외부에서 사용 불가

  // 자기 자신의 인스턴스를 외부에 제공
  public static Printer getPrinter(){
    if (printer == null) { // printer가 생성 되어있지 않으면 새로 생성
      // Printer 인스턴스 생성
      printer = new Printer();
    }
    return printer;
  }

  public void print(String str) {
    System.out.println(str);
  }
}
```

```java
//Client
public class User {
  private String name;
  public User(String name) { this.name = name; }
  public void print() {
    Printer printer = printer.getPrinter();
    printer.print(this.name + " print using " + printer.toString());
  }
}

public class Client {
  private static final int USER_NUM = 5;
  public static void main(String[] args) {
    User[] user = new User[USER_NUM];
    for (int i = 0; i < USER_NUM; i++) {
      // User 인스턴스 생성
      user[i] = new User((i+1))
      user[i].print();
    }
  }
}
```

## 문제점

> **다중 스레드**에서 Printer 클래스를 이용할 때 **인스턴스가 1개 이상 생성**되는 경우가 발생 가능

- **경합 조건(Race Condition)** 을 발생시키는 경우

    > **경합 조건**이란 메모리와 같은 **동일한 자원**을 2개 이상의 스레드가 이용하려고 경합하는 현상

    - Printer 인스턴스가 아직 생성되지 않았을 때 스레드 1이 `getPrinter` 메서드의 if문을 실행해 이미 인스턴스가 생성되었는지 확인. 현재 printer 변수는 null인 상태
    - 만약 스레드 1이 생성자를 호출해 인스턴스를 만들기 전 스레드 2가 if문을 실행해 printer 변수가 null인지 확인. 현재 printer 변수는 null이므로 인스턴스를 생성하는 생성자를 호출하는 코드를 실행
    - 스레드 1도 스레드 2와 마찬가지로 인스턴스를 생성하는 코드를 실행하게 되면 **결과적으로 Printer 클래스의 인스턴스가 2개 생성**

## 해결책

> 프린터 관리자(Lazy Initialization)는 사실 **다중 스레드 애플리케이션이 아닌 경우에는 아무런 문제가 되지 않음**

- 다중 스레드 애플리케이션에서 발생하는 문제를 해결하는 방법
    1. **정적 변수**에 인스턴스를 만들어 바로 초기화하는 방법 (Eager Initialization)

        ```java
        public class Printer {
           // static 변수에 외부에 제공할 자기 자신의 인스턴스를 만들어 초기화
           private static Printer printer = new Printer();
           private Printer() { }
           // 자기 자신의 인스턴스를 외부에 제공
           public static Printer getPrinter(){
             return printer;
           }
           public void print(String str) {
             System.out.println(str);
           }
        }
        ```

        - **static 변수**
            - 객체가 생성되기 전 클래스가 메모리에 로딩될 때 만들어져 **초기화가 한 번만 실행**
            - 프로그램 시작~종료까지 없어지지 않고 **메모리에 계속 상주**하며 클래스에서 생성된 모든 객체에서 참조 가능
    2. 인스턴스를 만드는 **메서드에 동기화**하는 방법 (Thread-Safe Initialization)

        ```java
        public class Printer {
           // 외부에 제공할 자기 자신의 인스턴스
           private static Printer printer = null;
           private int counter = 0;
           private Printer() { }
           // 인스턴스를 만드는 메서드 동기화 (임계 구역)
           public synchronized static Printer getPrinter(){
             if (printer == null) {
               printer = new Printer(); // Printer 인스턴스 생성
             }
             return printer;
           }
           public void print(String str) {
             // 오직 하나의 스레드만 접근을 허용함 (임계 구역)
             // 성능을 위해 필요한 부분만을 임계 구역으로 설정한다.
             synchronized(this) {
               counter++;
               System.out.println(str + counter);
             }
           }
        }
        ```

        - **인스턴스를 만드는 메서드**를 임계 구역으로 변경
            - 다중 스레드 환경에서 동시에 여러 스레드가 `getPrinter`메서드를 소유하는 객체에 접근하는 것을 방지
        - **공유 변수에 접근하는 부분**을 임계 구역으로 변경
            - 여러 개의 스레드가 하나뿐인 counter 변수 값에 동시에 접근해 갱신하는 것을 방지
        - `getInstance()`에 Lock을 하는 방식이라 **속도가 느림**

## 정적 클래스

> 정적 메서드로만 이루어진 정적 클래스를 사용하면 싱글턴과 동일한 효과를 얻을 수 있다.

```java
public class Printer {
      private static int counter = 0;
      // 메서드 동기화 (임계 구역)
      public synchronized static void print(String str) {
        counter++;
        System.out.println(str + counter);
      }
}
```

```java
public class UserThread extends Thread{
    // 스레드 생성
    public UserThread(String name) { super(name); }
    // 현재 스레드 이름 출력
    public void run() {
      Printer.print(Thread.currentThread().getName());
    }
}
public class Client {
    private static final int THREAD_NUM = 5;
    public static void main(String[] args) {
      UserThread[] user = new UserThread[THREAD_NUM];
      for (int i = 0; i < THREAD_NUM; i++) {
        // UserThread 인스턴스 생성
        user[i] = new UserThread((i+1));
        user[i].start();
      }
    }
}
```

- 차이점
    - 정적 클래스를 이용하면 **객체를 전혀 생성하지 않고 메서드를 사용**
    - 정적 메서드를 사용하므로 일반적으로 실행할 때 바인딩되는(컴파일 타임에 바인딩되는) 인스턴스 메서드를 사용하는 것보다 **성능 면에서 우수**
- **인터페이스를 구현해야 하는 경우**, 정적 메서드는 인터페이스에서 **사용 불가**
    - **대체 구현이 필요한 경우**, 인터페이스를 사용 ex. Mock 객체를 사용해 단위 테스트를 수행하는 경우

## Enum 클래스

```java
public enum SingletonTest {
	INSTANCE;

	public static SingletonTest getInstance() {
		return INSTANCE;
	}
}
```

- Thread-safety와 Serialization이 보장된다.

    > **스레드 안전(thread safety)** 은 멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻함

    > **직렬화(serialization)** 은 컴퓨터 과학의 데이터 스토리지 문맥에서 데이터 구조나 오브젝트 상태를 동일하거나 다른 컴퓨터 환경에 저장(이를테면 파일이나 메모리 버퍼에서, 또는 네트워크 연결 링크 간 전송)하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정

- Reflection을 통한 공격에도 안전하다.

    > **반영(reflection)** 은 컴퓨터 프로그램에서 런타임 시점에 사용되는 자신의 구조와 행위를 관리(type introspection)하고 수정할 수 있는 프로세스를 의미

- 따라서 Enum을 이용해서 Singleton을 구현하는 것이 가장 좋은 방법
