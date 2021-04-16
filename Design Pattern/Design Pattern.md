# 디자인 패턴 Design Pattern

## 디자인 패턴이란?
소프트웨어 공학의 소프트웨어 설계에서 **공통으로 발생하는 문제에 대해 자주 쓰이는 설계 방법을 정리한 패턴**   
소프트웨어를 설계할 때 특정 맥락에서 자주 발생하는 고질적인 문제들이 또 발생했을 때 재사용할 할 수 있는 훌륭한 해결책   
“바퀴를 다시 발명하지 마라(Don’t reinvent the wheel)” → 이미 만들어진 것을 처음부터 다시 만들 필요가 없다는 의미
> 💡 디자인 패턴을 참고하여 개발할 경우 개발의 **효율성**과 **유지보수성**, **운용성**이 높아지며, **프로그램의 최적화에 도움**이 된다.

## 디자인 패턴 구조
1. **콘텍스트 Context**
    - 문제가 발생하는 여러 상황을 기술. 즉, 패턴이 적용될 수 있는 상황을 나타낸다.
    - 경우에 따라서는 패턴이 유용하지 못한 상황을 나타내기도 한다.
2. **문제 Problem**
    - 패턴이 적용되어 해결될 필요가 있는 여러 디자인 이슈들을 기술
    - 이때 여러 제약 사항과 영향력도 문제 해결을 위해 고려해야 한다.
3. **해결 Solution**
    - 문제를 해결하도록 설계를 구성하는 요소들과 그 요소들 사이의 관계, 책임, 협력 관계를 기술
    - 해결은 반드시 구체적인 구현 방법이나 언어에 의존적이지 않으며 다양한 상황에 적용할 수 있는 일종의 템플릿

## 디자인 패턴 유형
![디자인 패턴 유형](./images/디자인%20패턴%20유형.jpg)

## GoF 디자인 패턴(목적에 따른 디자인 패턴 종류)
**이 분야의 4인방(Gang of Four, GoF)** 이라 불리는 에리히 감마(Erich Gamma), 리차드 헬름(Richard Helm), 랄프 존슨(Ralph Johnson), 존 블리시데스(John Vlissides)가 고안한 디자인 패턴   
**23가지의 디자인 패턴**을 정리하고 각각의 디자인 패턴을 생성(Creational), 구조(Structural), 행위(Behavioral) 3가지로 분류

### [생성 패턴](https://github.com/triflingness/CSnCT-Study/blob/main/Design%20Pattern/Creational%20Pattern.md)
객체 생성에 관련된 패턴   
객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공함
1. Builder
2. Prototype
3. Factory Method
4. Abstract Factory
5. Singleton

### 구조 패턴
클래스나 객체를 조합해 더 큰 구조를 만드는 패턴   
예를 들어 서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스를 재공하거나 객체들을 서로 묶어 새로운 기능을 제공하는 패턴
1. Bridge
2. Decorator
3. Facade
4. Flyweight
5. Proxy
6. Composite
7. Adapter

### 행위 패턴
객체나 클래스 사이의 알고리즘이나 책임 분배에 관련된 패턴   
한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 또 그렇게 하면서도 객체 사이의 결합도를 최소화하는 것에 중점을 둠
1. Mediator
2. Interpreter
3. Iterator
4. Template Method
5. Observer
6. State
7. Visitor
8. Command
9. Strategy
10. Memento
11. Chain of Responsibility
