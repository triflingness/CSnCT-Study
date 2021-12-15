# OOP
> 객체 지향 프로그래밍, Object-Oriented Programming

절차 지향 언어인 C언어와 달리 객체의 관점에서 프로그래밍을 하는 패러다임

- 절차 지향 언어는 실행 순서, 절차에 집중되어있고 OOP는 객체의 종류, 속성에 더 집중되어 있습니다.
- 프로그램의 요소를 객체로 보고 이들의 상호작용을 연결하여 프로그래밍을 합니다.


> 📌 **절차 지향 언어(POP, Procedure Oriented Programming)**
>
> 프로세스 호출의 개념 바탕으로 실행 순서가 중점이 됩니다.
> 함수 단위로 프로그래밍을 합니다.


## OOP 특징

### 1. 캡슐화 (Encapsulation)

객체가 필요한 변수나 메소드를 하나로 묶는 것을 말합니다.

- `Class` 를 통해서 구현이 됩니다.

- `정보은닉` : `Class` 외부에서는 객체의 변수의 메소드가 어떻게 구현되어 있는 지, 변수를 알 수 없게 할 수 있습니다. 따라서 노출이 불필요한 정보를 감출 수 있습니다. 3가지의 접근제한 종류를 사용합니다.
    - `public` : 클래스 외부에서 사용할 수 있습니다.
    - `protected` : 다른 클래스에서 노출되지 않지만, 자식 클래스에게는 노출됩니다.
    - `private` : 클래스 외부에 노출되지 않고 클래스 내부에서만 사용가능합니다.

> 📌 **캡슐화 ≠ 정보은닉**
> 
> 정보은닉은 캡슐화의 특성으로 나온 개념이므로 캡슐화를 이용해 정보은닉을 할 수 있다는 이해가 더 타당합니다.

### 2. 추상화 (Abstraction)

부가적인 부분을 제거하고 필요한 부분만 표현하기 위한 개념을 말합니다.

- `인터페이스` 와 `추상클래스` 는 객체들의 공통적인 기능, 필수적인 기능을 추출하여 만들어진 큰 틀의 클래스입니다.
- 추상화 과정으로 코드의 재사용성이 향상되고 생산성이 증가되어 유지보수 시간이 단축됩니다.

### 3. 상속 (Inheritance)

상위 클래스(부모 클래스)의 메소드나 변수를 물려받아 하위 클래스(자식 클래스)가 사용할 수 있는 것을 말합니다.

- 자식 클래스는 필요에 따라 상속받은 부모 클래스의 기능을 재정의할 수 있습니다.(`Overriding`)
- 상속을 통해 코드의 중복을 줄여 클래스의 재사용이 용이해집니다.

### 4. 다형성 (Polymorphism)

변수나 메서드가 상황에 따라 다른 타입을 가질 수 있는 것을 말합니다.

- `method overriding`, `method overloading` 으로 다형성을 실현시킵니다.
- 메서드 이름이 같아도 사용하는 객체에 따라, 매개변수에 따라 다른 기능을 합니다.
- 다형성으로 메서드 이름을 낭비하지 않고 인터페이스를 유지할 수 있습니다.

---

OOP vs POP 비교 - [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=hirit808&logNo=221457311265#](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=hirit808&logNo=221457311265#)

OOP 특징 - [https://velog.io/@hkoo9329/OOPObject-Oriented-Programming-객체-지향-프로그래밍-이란](https://velog.io/@hkoo9329/OOPObject-Oriented-Programming-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9D%B4%EB%9E%80)
