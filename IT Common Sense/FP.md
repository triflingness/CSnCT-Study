# FP
> 함수형 프로그래밍, Functional Programming


함수형 프로그래밍은 순수 함수로 조합되고 명령형이 아닌 선언형 프로그래밍을 기반으로 한 패러다임입니다.

- 명령형 프로그래밍 : 무엇(What)을 할 것인지 나타내기보다 어떻게(How) 할 건지를 설명하는 방식
    - `for문`, `if문`을 사용해 로직과 기능의 메서드를 호출(명령)하는 형식
    - 절차지향 프로그래밍, 객체지향 프로그래밍
- 선언형 프로그래밍 : 어떻게 할건지(How)를 나타내기보다 무엇(What)을 할 건지를 설명하는 방식
    - 데이터를 다루는 과정(흐름)을 정의하는 형식
    - 함수형 프로그래밍

### 1급 객체(First object)

다음과 같은 조건을 만족하는 객체입니다. 함수형 프로그래밍의 조건이 될 수 있습니다.

- 변수나 데이터 구조 안에 넣을 수 있다.
- 파라미터로 전달할 수 있다.
- 동적으로 프로퍼티 할당이 가능하다.
- 리턴값으로 사용할 수 있다.

FP는 함수를 1급 객체로 취급하기 때문에 파라미터로 넘기는 작업이 가능한 것이다.

## 함수형 프로그래밍 조건

### 1. 순수 함수(Pure function)

부작용(side-effect)가 없는 함수입니다.

- 함수의 실행이 시스템 상태에 영향을 받지 않는 함수를 말합니다.
- 같은 입력에 대해 같은 출력을 반환하는 함수입니다.
- 여러 스레드가 동시에 접근해도 안전하고 병렬 계산도 가능합니다.

### 2. 익명 함수(**Anonymous function)**

이름이 없는 함수로 람다식으로 표현되는 함수입니다.

**기존**(c)

```c
int square(int x){return x*x;}
```

**익명 함수 적용**(c++)

```cpp
[](int x) -> int {return x*x;}
```

### 3. 고차 함수(High-order functon)

함수를 다루는 함수를 말합니다.

함수형 언어에서는 함수도 ‘값(value)’ 취급합니다.

- 함수의 인자로 함수를 전달할 수 있다.
- 함수의 리턴값으로 함수를 사용할 수 있다.

**기존**

```jsx
const arr1 = [1, 2, 3];
const arr2 = [];

for(let i=0; i<arr1.length; i++) {
  arr2.push(arr1[i] * 2);
}

// prints [2, 4, 6]
console.log(arr2);
```

**고차 함수 적용**

```jsx
const arr1 = [1, 2, 3];

const arr2 = arr1.map(function(item) {
  return item * 2;
});
// const arr2 = arr1.map(item => item * 2);

console.log(arr2);
```