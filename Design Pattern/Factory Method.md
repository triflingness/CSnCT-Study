# Factory Method

- **상위 클래스에서 객체를 생성하는 인터페이스를 정의하고, 하위 클래스에서 인스턴스를 생성하도록 하는 방식**으로, 상위 클래스에서는 인스턴스를 만드는 방법만 결정하고, 하위 클래스에서 그 데이터의 생성을 책임지고 조작하는 함수들을 오버라이딩하여 **인터페이스와 실제 객체를 생성하는 클래스를 분리할 수 있는 특성**을 갖는 디자인 패턴
- 생성할 객체의 클래스를 국한하지 않고 객체를 생성

## 사용이유

- 객체 생성 하는 코드를 분리하여 클라이언트 코드와 결합도(의존성)를 낮추어 코드를 건드리는 횟수를 최소화 하기 위해서

```java
public abstract class Type {
}
```

```java
public class TypeA extends Type{
    public TypeA(){
        System.out.println("Type A 생성");
    }
}
```

```java
public class TypeB extends Type{
    public TypeB(){
        System.out.println("Type B 생성");
    }
}
```

```java
public class TypeC extends Type{
    public TypeC(){
        System.out.println("Type C 생성");
    }
}
```

- 분기처리하여 객체를 생성하는 코드가 여러 클래스에서 사용하는 경우 다음과 같은 **중복된 코드가 발생**
- 또한, 객체를 생성하는 일은 **객체간의 결합도를 강하게** 만드는 일이고, 객체간 결합도가 강하면 유지보수가 어려워짐

→ **팩토리 메서드 패턴을 사용**하여, 다른 객체 생성하는 부분을 자신이 하지 않고 **팩토리 클래스를 만들어서 팩토리 클래스에서 하도록 함**

```java
class ClassA {
    public Type createType(String type){
        Type returnType = null;
        switch (type){
            case "A":
                returnType = new TypeA();
                break;

            case "B":
                returnType = new TypeB();
                break;

            case "C":
                returnType = new TypeC();
                break;
        }

        return returnType;
    }
}
```

```java
class ClassB {
    public Type createType(String type){
        Type returnType = null;
        switch (type){
            case "A":
                returnType = new TypeA();
                break;

            case "B":
                returnType = new TypeB();
                break;

            case "C":
                returnType = new TypeC();
                break;
        }

        return returnType;
    }
}
```

```java
class ClassC {
    public Type createType(String type){
        Type returnType = null;
        switch (type){
            case "A":
                returnType = new TypeA();
                break;

            case "B":
                returnType = new TypeB();
                break;

            case "C":
                returnType = new TypeC();
                break;
        }

        return returnType;
    }
}
```

```java
// Client 코드: 분리시킨 객체 생성 코드를 호출하는 쪽
public class Client {
    public static void main(String args[]){
        ClassA classA = new ClassA();
        classA.createType("A");
        classA.createType("C");
    }
}
```

## 예제

### 방법

1. 팩토리 클래스 정의
2. 객체 생성이 필요한 클래스(ClassA)에서 팩토리 객체를 생성하여 분기에 따른 객체 생성 메서드를 호출 → Type, TypeA, TypeB, TypeC, Client 클래스의 코드는 동일

```java
// 패턴을 적용하기 전 ClassA가 할 일을 TypeFactory 클래스에서 정의
public class TypeFactory {
    public Type createType(String type){
        Type returnType = null;
        switch (type){
            case "A":
                returnType = new TypeA();
                break;

            case "B":
                returnType = new TypeB();
                break;

            case "C":
                returnType = new TypeC();
                break;
        }

        return returnType;
    }
}
```

```java
// TypeFactory 클래스를 사용하여 객체를 생성
public class ClassA {
    public Type createType(String type){
        TypeFactory factory = new TypeFactory();
        Type returnType = factory.createType(type);

        return returnType;
    }
}
```

**조건에 따른 객체 생성 부분**을 자신이 직접하지 않고 **팩토리 클래스에 위임**하여 객체를 생성하도록 하는 방법

### 고려사항

- 새로운 객체를 사용하고 싶다면 재사용보단 계속해서 확장해야 할 수 있음→ 구현해야 하는 클래스의 개수 증가

##### 참고

- [https://victorydntmd.tistory.com/299](https://victorydntmd.tistory.com/299)
- [https://biggwang.github.io/2019/06/28/Design Patterns/[Design Patterns] 팩토리 패턴, 도대체 왜 쓰는거야-기본 이론편/](https://biggwang.github.io/2019/06/28/Design%20Patterns/%5BDesign%20Patterns%5D%20%ED%8C%A9%ED%86%A0%EB%A6%AC%20%ED%8C%A8%ED%84%B4,%20%EB%8F%84%EB%8C%80%EC%B2%B4%20%EC%99%9C%20%EC%93%B0%EB%8A%94%EA%B1%B0%EC%95%BC-%EA%B8%B0%EB%B3%B8%20%EC%9D%B4%EB%A1%A0%ED%8E%B8/)
