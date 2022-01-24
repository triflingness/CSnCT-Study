## MVVM

Model, View, View-Model의 컴포넌트를 사용하여 구현하는 아키텍처

### 각 컴포넌트의 역할

모델과 뷰는 MVC 패턴의 역할과 같습니다.

**Model**

데이터베이스 관련 기능을 담당하는 부분

**View**

시각적으로 표시되는 모든 부분

**View Model**

뷰가 사용할 데이터를 관리하는 부분

### MVVM 동작

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/MVVM.png">
</p>

1. 사용자의 Action들은 View를 통해 들어오게 됩니다.
2. View에 Action이 들어오면, Command 패턴으로 View Model에 Action을 전달합니다.
3. View Model은 Model에게 데이터를 요청합니다.
4. Model은 View Model에게 요청받은 데이터를 응답합니다.
5. View Model은 응답 받은 데이터를 가공하여 저장합니다.
6. View는 View Model과 Data Binding하여 화면을 나타냅니다.

### MVVM 장단점

**장점**

- View와 Model의 의존성이 없습니다.
- Command 패턴과 Data Binding을 사용하여 View와 View Model 사이의 의존성이 없습니다.
- 따라서 각 컴포넌트는 독립적이기 때문에 모듈화하여 개발할 수 있습니다.

**단점**

- View Model의 설계가 쉽지 않습니다.

---

[https://beomy.tistory.com/43](https://beomy.tistory.com/43)
