# Decorator Pattern

주어진 상황 및 용도에 따라 어떤 객체에 책임을 덧붙이는 패턴이다.

- 기능 확장이 필요할 때, 서브클래스를 생성하는 것보다 융통성 있는 방법을 제공한다.
- 상속과 합성을 사용하여 객체에 동적으로 책임을 추가할 수 있다.

→ 상속을 통한 서브클래스 생성 방법이 비효율적일 때 사용한다.

→ 런타임에서 유연하게 객체의 기능들을 수정하고 조합할 때 유용한 패턴이다.

### Decorator Pattern 구조

- **Component**
    - `ConcreteComponent` 와 `Decorator` 의 공통 기능을 정의하는 인터페이스이다.
    - 클라이언트는 `Component` 를 통해 실제 객체를 사용한다.
- **ConcreteComponent**
    - 기본적인 기능을 구현하는 클래스이다.
    - 기능 추가를 받을 기본적인 객체이다.
- **Decorator**
    - Decorate를 할 객체의 추상 클래스이다.
    - 기능 추가를 할 객체는 **Decorator** 를 상속받는다.
- **ConcreteDecorator**
    - Decorator를 상속받아 구현할 다양한 기능 객체이다.
    - Decorator의 하위 클래스로 기본 기능에 추가되는 개별적인 기능이다.

<img src="./images/a" width="70%" height="40%">

→ 추가 기능을 Decorator 클래스로 정의한 후 필요한 Decorator 객체를 조합한다.

### 사용 예시

**Component -** Christmass Tree 인터페이스(나무와 장식 추상화) 

```java
public interface ChristmasTree {
    String decorate();
}
```

**ConcreteComponent -** Christmass Tree 인터페이스 구현(나무 구현)

```java
public class ChristmasTreeImpl implements ChristmasTree {

    @Override
    public String decorate() {
        return "Christmas tree";
    }
}
```

**Decorator - 추상 TreeDecorator 클래스 (장식 추상화)**

```java
public abstract class TreeDecorator implements ChristmasTree {
    private ChristmasTree tree;
    
    // standard constructors
    @Override
    public String decorate() {
        return tree.decorate();  //장식 메서드 호출
    }
}
```

 

**ConcreteDecorator - 다양한 기능 객체들 구현 (장식 구현)**

```java
public class BubbleLights extends TreeDecorator {

    public BubbleLights(ChristmasTree tree) {
        super(tree);   // 중요
    }
    
    public String decorate() { //중요
        return super.decorate() + decorateWithBubbleLights();
    }
    
    private String decorateWithBubbleLights() {
        return " with Bubble Lights";
    }
}
```

Main

```java
@Test
public void whenDecoratorsInjectedAtRuntime_thenConfigSuccess() {
    ChristmasTree tree1 = new ChristmasTreeImpl();
    System.out.println(tree1.decorate());
     
    ChristmasTree tree2 = new BubbleLights(
      new Garland(new ChristmasTreeImpl()));
    System.out.println(tree2.decorate());
}
```

### 장점

- 객체에 기능 추가가 간단하다.

### 단점

- 다수의 데코레이터의 객체 생성으로 인해 필요이상으로 코드가 복잡해질 수 있다.

> JDK 에서 FileReader, BufferedReader 등 IO 클래스에 사용되는 패턴이다.

---

참조

[https://johngrib.github.io/wiki/decorator-pattern/](https://johngrib.github.io/wiki/decorator-pattern/)

[https://gmlwjd9405.github.io/2018/07/09/decorator-pattern.html](https://gmlwjd9405.github.io/2018/07/09/decorator-pattern.html)

[https://readystory.tistory.com/195](https://readystory.tistory.com/195)
