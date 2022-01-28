# MVP
> Model, View, Presenter의 컴포넌트를 사용하여 구현하는 아키텍처

- MVC의 뷰와 모델의 의존성을 해결하기 위해 **View와 Model이 완전히 분리**해서 사용한다.
    - 테스트 코드 짜기가 용이해진다.
- 뷰와 액티비티가 자연스럽게 결합되도록 한다.

### 각 컴포넌트의 역할

View와 Model은 Presenter를 통해서만 데이터를 주고 받을 수 있다.

**Model**

- 데이터베이스 관련 기능을 담당하는 부분

**View**

- 화면에 직접적인 접근을 담당하는 부분
- View에서 발생하는 이벤트가 들어오면 Presenter에게 전달한다.
- (안드로이드) 화면 UI 부분과 액티비티/프래그먼트를 담당하는 부분

**Presenter(프리젠터)**

- 뷰와 모델 사이의 데이터 전달 역할
- MVC의 컨트롤러와 같은 역할이지만, 뷰와는 인터페이스로 연결이 된다.

### MVP 동작

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MVP.png">
</p>

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MVP2.png" width="700">
</p>

1. 사용자의 Action은 View를 통해서 들어오게 된다.
2. View는 데이터를 Presenter에 전달하고 행위를 요청한다.
3. Presenter는 이벤트에 따라서 Model에게 데이터를 요청한다.
4. Model은 요청받은 데이터를 Presenter에게 전달한다.
5. Presenter는 필요에 따라 가공한 후, View에게 전달한다.
6. View는 Presenter가 응답한 결과를 반영하여 UI를 갱신한다.

### MVP 장단점

**장점**

- **View와 Model의 의존성이 없다.**
    - View는 Presenter를 통해서 데이터를 받는다.
    - 뷰와 모델이 분리되어 있어 View와 비지니스 로직이 분리되어 **테스트가 용이**해진다.

**단점**

- **View와 Presenter는 높은 의존성**을 가지게 된다.
- Presenter에 추가적인 비지니스 로직이 추가되어 **유지보수가 힘들다.**

---

**[참고]**

[https://academy.realm.io/kr/posts/eric-maxwell-mvc-mvp-and-mvvm-on-android/](https://academy.realm.io/kr/posts/eric-maxwell-mvc-mvp-and-mvvm-on-android/)

[https://salix97.tistory.com/205](https://salix97.tistory.com/205)

[https://faith-developer.tistory.com/71](https://faith-developer.tistory.com/71)
