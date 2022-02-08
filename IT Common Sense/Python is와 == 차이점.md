# Python is와 == 차이점
- `is` 와 `==` 은 조건문에서 두 개의 변수가 같은지 체크할 때 사용하지만 차이점이 있다.
</br>

### `is` 와 `==` 의 차이점

- `is` 는 변수의 Object(객체)가 같을 때 True를 리턴한다. → Value equality
- `==` 은 변수의 Value(값)이 같을 때 True를 리턴한다. → Reference equlity
</br>

### `is` 연산 예제

```python
a = []
b = []
c = a

a is b
>>> False # 값은 같지만 객체가 다르다.

a is c
>>> True # 서로 같은 객체이다.
```
</br>

### `==`  연산 예제

```python
a = []
b = []
c = a

a == b
>>> True # 서로 같은 값을 가진다.

a == c
>>> True # 서로 같은 값을 가진다.
```
</br>

---
출처 및 참고

[Python 값 비교 ==와 is 차이점 (tistory.com)](https://ponyozzang.tistory.com/292)

[[Python] is 와 == 의 차이 (tistory.com)](https://sohyunwriter.tistory.com/54?category=906375)
