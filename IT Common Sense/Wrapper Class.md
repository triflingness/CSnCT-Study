## 변수 타입과 박싱
- Primitive type(원시 변수)
    - 변수에 값 자체를 저장하는 변수 (정수형, 실수형, 문자형, 논리형)
    - stack에 저장
- Reference type(참조 변수)
    - 메모리상에 객체가 있는 위치(주소)를 저장하는 변수 (class, interface, array 등)
- Boxing(박싱)
    - 원시 타입을 참조 타입으로 변환시키는 것
- Unboxing(언박싱)
    - 참조 타입을 원시 타입으로 변환시키는 것

## 자바의 Wrapper Class

원시 타입을 객체로 감싸서 다룰 수 있게 해준다.

기본형 변수를 객체화할 필요가 있을 때 객체로 다룰 수 있게 해준다.

| Primitive type | Wrapper Class |
| --- | --- |
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| boolean | Boolean |
| char | Character |

## Auto Boxing / Unboxing

- 명시적으로 원시타입을 참조타입으로 감싸주지 않아도 자동으로 boxing / unboxing 하는 기능
- JDK 1.5부터 지원
- 하지만 Auto Boxing / Unboxing 은 메모리 누수의 원인이 될 수 있다.

```java
public static void main(String[] args){
	char ch = 'j';
	autoBoxing(ch);
}

public static void autoBoxing(Character chr)(
	System.out.println("test result : "+ chr);
}

// [실행 결과]
// test result : j
```

```java
Integer num = new Integer(2);  // boxing
int n = num.intValue();      // Unboxing

Character ch = 'H';  // Auto boxing : Character ch = new Character('H');
char c = ch;    // Auto unboxing : char c = ch.charValue();
```

---

[https://velog.io/@gillog/원시타입-참조타입Primitive-Type-Reference-Type](https://velog.io/@gillog/%EC%9B%90%EC%8B%9C%ED%83%80%EC%9E%85-%EC%B0%B8%EC%A1%B0%ED%83%80%EC%9E%85Primitive-Type-Reference-Type)

[https://preamtree.tistory.com/15](https://preamtree.tistory.com/15)

[https://jamesdreaming.tistory.com/154](https://jamesdreaming.tistory.com/154)
