# Strategy Pattern

객체가 할 수 있는 행위를 각각의 알고리즘으로 정의하고, 각 알고리즘들을 캡술화하여 별도의 클래스에 넣고, 해당 알고리즘들을 교환할 수 있도록 하는 패턴이다.

- 전략 패턴을 사용하면 알고리즘을 사용하는 클라이언트와 독립적으로 알고리즘을 변경할 수 있다.
- 객체의 행위를 동적으로 바꿀 때, 행위를 직접 수정하지 않고, 전략을 상호 교체하여 바꿀 수 있다.

✔ 전략 패턴은 **특정한 계열의 알고리즘들을 정의**하고, **각 알고리즘을 캡슐화**하며, **이 알고리즘들을 해당 계열 안에서 상호 교체가 가능**하게 만든다.



### Strategy Pattern 구조

<img src="./images/strategy_structure.png" width="50%" height="30%">

- **Context**
    - `ConcreteStrategy` 중 하나에 대한 참조를 유지하고 `Strategy` 를 통해서 해당 객체와 통신한다.
    - 알고리즘을 실행할 때마다 연결된 `Strategy`의 실행 메서드를 호출한다.
    - `Context` 는 어떤 전략(알고리즘)이 실행되는지 모른다.
    - `Context` 는 런타임 중 `Client` 가 `Context` 와 관련된 `Stategy` 를 교체할 수 있는 `setter` 메서드를 노출한다.
- **Strategy**
    - 모든 `ConcreteStrategy` 의 공통적인 인터페이스나 추상 클래스이다.
    - `Context` 가 전략(알고리즘)을 호출하는 방법을 선언한다.
- **ConcreteStrategy**
    - `Strategy` 에 명시된 알고리즘을 구현하는 클래스이다.
    - `Context` 가 사용하는 알고리즘의 다양한 변형을 구현한다.



### 사용 예시

📌 **Strategy**

```java
public interface Strategy {
   public int doOperation(int num1, int num2);
}
```

📌 **ConcreteStrategy**

```java
public class OperationAdd implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 + num2;
   }
}

public class OperationSubstract implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 - num2;
   }
}

public class OperationMultiply implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 * num2;
   }
}
```

📌 **Context**

```java
public class Context {
   private Strategy strategy;

   public Context(Strategy strategy){
      this.strategy = strategy;
   }

	// setter
   public int executeStrategy(int num1, int num2){
      return strategy.doOperation(num1, num2);
   }
}
```

📌 **Client**

```java
public class StrategyPatternDemo {
   public static void main(String[] args) {
      Context context = new Context(new OperationAdd());		
      System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationSubstract());		
      System.out.println("10 - 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationMultiply());		
      System.out.println("10 * 5 = " + context.executeStrategy(10, 5));
   }
}
```




### 장점

- 런타임 중 개체 내부에서 사용되는 알고리즘을 교환할 수 있다.
- 요구 사항이 변경되었을 때 코드의 변경 없이 새로운 전략을 추가할 수 있다.
- 조건문을 없앨 수 있다.
- 상속 클래스를 만들지 않고 구성으로 대체할 수 있다.

### 단점

- 메모리를 많이 사용할 수 있다.
- Strategy 객체와 Context 객체 사이에 통신 오버헤드가 클 수 있다.
- 사용자는 객체와 전략 클래스를 알아야 한다.

### 사용 이유

- 객체 내에서 다양한 알고리즘 변형을 사용하고 런타임 중에 한 알고리즘에서 다른 알고리즘으로 전환할 수 있도록 하려는 경우
- 일부 동작을 실행하는 방식만 다른 유사한 클래스가 많이 있는 경우




----------

참고

[https://sourcemaking.com/design_patterns/strategy](https://sourcemaking.com/design_patterns/strategy)

[https://refactoring.guru/design-patterns/strategy](https://refactoring.guru/design-patterns/strategy)

[https://gmlwjd9405.github.io/2018/07/06/strategy-pattern.html](https://gmlwjd9405.github.io/2018/07/06/strategy-pattern.html)

[https://velog.io/@kyle/디자인-패턴-전략패턴이란](https://velog.io/@kyle/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EC%A0%84%EB%9E%B5%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80)

[https://www.tutorialspoint.com/design_pattern/strategy_pattern.htm](https://www.tutorialspoint.com/design_pattern/strategy_pattern.htm)
