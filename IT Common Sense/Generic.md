# 제네릭(Generic)
데이터 type에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입들을 가질 수 있도록 하는 방법

- **데이터 타입을** **클래스** 내부에서 지정하는 것이 아닌 **외부에서 지정되는 것을 의미**
- 특정(Specific) 타입을 미리 지정해주는 것이 아닌 **필요해 의해 지정할 수 있도록 하는 일반(Generic)타입**이다.
- 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일시 타입체크를 해주는 기능

## Generic의 장점

1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지
2. 클래스 외부에서 타입을 지정하기 때문에 타입을 체크하고 변환해줄 필요가 없음
3. 코드의 재사용성이 높아짐

## Generic 사용방법

### 타입 변수 (type variable)

아래 표는 자주 사용되는 데이터 타입을 대신하는 임의의 참조형 타입을 보여줍니다.

| 타입 | 설명 |
| --- | --- |
| < T > | Type |
| < E > | Element |
| < K > | Key |
| < V > | Value |
| < N > | Number |
- 표 외의 다른 문자를 사용해도 상관없습니다.
- 여러 개의 타입 변수는 쉼표(`,`)로 구분합니다.
- 타입 변수는 클래스, 메소드의 매개변수나 변환값으로 사용할수 있습니다.

### 1. 클래스 및 인터페이스 선언

```java
// 1. 클래스 및 인터페이스 선언
public class ClassName <T> {...}
public Interface InterfaceName <T, K> {...}
public class HashMap <K, V> {...}   // 대표적인 제네릭 타입을 두개 받는 컬렉션은 HashMap이 있다.

public class Student {...}

// 2. 객체 생성
// - 객체 생성할때는 구체적인 타입을 명시해주어야 한다.
// - 타입 파라미터는 primitive type이 아닌 참조 타입(Reference Type)만 올 수 있다.
public class Main {
	public static void main(String[] args) {
		HashMap<String, Integer> a = new HashMap<String, Integer>();
		ClassName<Student> std = new ClassName<Student>();   // 사용자 정의 클래스도 변수로 올 수 있다.
	}
}

```

### 2. 제네릭 클랙스 활용

```java
// 제네릭 클래스 정의
public class GenericC <E>{
	private E element;

	public void set(E element){ this.element = element;}
	public E get(){return element;}
}

class Main{
	public static void main(String[] args){
		GenericC<String> a = new GenericC<String>();
		GenericC<Integer> b = new GenericC<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		System.out.println("b E Type : " + b.get().getClass().getName());
	}

}

/*
~출력 결과~
a data : 10
a E type : java.lang.String

b data : 10
b E type : java.lang.Integer
*/
```

제네릭 변수를 사용한 클래스에서는 특정 변수를 지정해주지 않고 클래스 외부에서 변수의 타입을 지정해줬음을 볼 수 있습니다.
