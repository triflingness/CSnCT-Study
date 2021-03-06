# JVM, JRE, JDK

![JVM, JRE, JDK](./images/JVM,%20JRE,%20JDK.png)

## 자바 가상 머신 (JVM, Java Virtual Machine)

> 자바 프로그램을 컴파일해서 나온 결과인 **바이트코드를 실행**시켜주는 가상 머신

### 특징

1. 자바 프로그램이 **어느 기기, 어느 운영체제 상에서도 실행**될 수 있게 만들어 줌
    - 윈도우와 리눅스/맥 등 **다양한 환경에서 언제나 동일하게 실행**되도록 할 수 있음
    - 각 운영체제별 JVM은 자바측에서 개발하여 배포하므로, 프로그래머는 운영체제에 관계없이 프로그램을 개발할 수 있어, **한번 컴파일 됐으면 운영체제에 따라 다시 컴파일할 필요가 없음** → WORA

        > WORA: 한 번 쓰고 모든 곳에서 실행한다는 Java의 원칙 (Write Once, Run Anywhere)

2. 자바 프로그램의 **메모리를 효율적으로 관리 & 최적화**
    - **가비지 컬렉션(Garbage Collection)**: JVM이 **메모리를 관리하는 프로세스**를 지칭하는 용어. 자바 프로그램 상에서 사용하지 않은 메모리를 지속적으로 찾아 제거함으로써 효율적인 메모리 관리 가능
    - **자바 메모리 구성**
        1. **힙**: 자바가 변수 내용을 저장하는 장소
        2. **스택**: 자바가 함수 실행 및 변수 참조를 저장하는 장소
        3. **메타 스페이스**(과거 펌젠): 자바가 클래스 정의와 같이 프로그램에서 변화하지 않는 정보를 저장하는 장소

## 자바 런타임 환경 (JRE, Java Runtime Environment)

> JVM을 동작하는데에 필요한 각종 자바 라이브러리를 담고 있는 **자바 실행 환경**

- 클래스 로더, 클래스 라이브러리를 통해 **작성한 자바 코드를 라이브러리와 결합**한 후 JVM에 넘겨 실행시킴
- 그 자체로 특별한 기능을 한다기보다는 **JVM이 원활하게 잘 작동할 수 있도록 환경을 맞춰주는 역할**

### 구성요소

1. 자바 클래스 로더(Java class loader)
2. 자바 클래스 라이브러리(Java class libraries)
3. 자바 가상 머신(JVM)

## 자바 개발 키트 (JDK, Java Development Kit)

> JRE와 javac 등의 컴파일러, 디버거등을 포함하는 프로그램

- 오라클사에서 제공하는 오라클 JDK와 오픈소스로 개발된 OpenJDK가 있으나, 일반적으로 사용되는것은 오라클 JDK
- JDK를 설치하면 JRE, JVM이 자동으로 설치(**JDK ⊃ JRE ⊃ JVM**)
- JRE에는 없는 **자바 컴파일러(javac, java compiler)** 를 포함
