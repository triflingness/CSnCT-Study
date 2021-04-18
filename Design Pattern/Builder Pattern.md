# Builder
객체를 사용할 때, 아래의 코드와 같이 흔히 사용되는 패턴으로 Effective Java와 Gof의 **두가지 관점의 빌더 패턴**이 있음
```java
Member customer = Member.build()
    .name("홍길동")
    .age(30)
    .build();
```
<br/>

## Effective Java(2001)
조슈아 블로크 (Joshua Bloch)가 쓴 책인 Effective JAVA에서 소개되는 **객체 생성을 깔끔하고 유연하게 하기 위한 기법**
### 객체 생성을 깔끔하게 하기 위한 방법

#### 점층적 생성자 패턴(telescoping constructor pattern)

1. 필수 인자를 받는 필수 생성자를 하나 만든다.
2. 1 개의 선택적 인자를 받는 생성자를 추가한다.
3. 2 개의 선택적 인자를 받는 생성자를 추가한다.
4. 반복
5. 모든 선택적 인자를 다 받는 생성자를 추가한다.

```java
// 점층적 생성자 패턴 코드의 예 : 회원가입 관련 코드
public class Member {

    private final String name;      // 필수 인자
    private final String location;  // 선택적 인자
    private final String hobby;     // 선택적 인자

    // 필수 생성자
    public Member(String name) {
        this(name, "출신지역 비공개", "취미 비공개");
    }

    // 1 개의 선택적 인자를 받는 생성자
    public Member(String name, String location) {
        this(name, location, "취미 비공개");
    }

    // 모든 선택적 인자를 다 받는 생성자
    public Member(String name, String location, String hobby) {
        this.name = name;
        this.location = location;
        this.hobby = hobby;
    }
}
```
- 장점:  `new Member("홍길동", "출신지역 비공개", "취미 비공개")` 같은 호출이 빈번하게 일어난다면, `new Member("홍길동")`로 대체할 수 있다.
- 단점: 다른 생성자를 호출하는 생성자가 많으므로, 인자가 추가되는 일이 발생하면 코드를 수정하기 어려우며 코드 가독성이 떨어진다.
```java
// 호출 코드만으로는 각 인자의 의미를 알기 어렵다.
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 3, 35, 27);
NutritionFacts pepsiCola = new NutritionFacts(220, 10, 110, 4, 30);
NutritionFacts mountainDew = new NutritionFacts(230, 10);
```

#### 점층적 생성자 패턴의 대안, 자바빈 패턴(JavaBeans pattern)
`setter` 메서드를 이용해 생성 코드를 읽기 좋게 만드는 것
```java
NutritionFacts cocaCola = new NutritionFacts();
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohdydrate(27);
```
- 장점: 복잡하게 여러 개의 생성자를 만들지 않아도 되며, 각 인자를 파악하기 쉬움
- 단점
    - 객체 일관성(consistency)이 깨짐   
    → 한번의 호출로 객체가 생성되지 않고 생성한 객체에 값을 입력해야 함
    - `setter` 메서드가 있으므로 변경 불가능(immutable) 클래스를 만들 수가 없음   
    → 스레드 안전성을 확보하려면 점층적 생성자 패턴보다 많은 일을 해야 함   
        > **스레드 안전성**이란?   
        > 스레드에 안전한 코드를 작성하는 것은, 근본적으로는 **상태에 대한 접근을 관리**하는 것   
        > 여러 스레드가 클래스에 접근할 때, 실행 환경이 해당 스레드들의 실행을 어떻게 스케줄하든 어디에 끼워 넣든, 호출하는 측에서 동기화나 다른 조율 없이도 정확하게 동작하면 해당 클래스는 스레드 안전하다고 말한다.

#### 💡 자바빈 패턴의 대안, 빌더 패턴(Builder Pattern)

```java
// Effective Java의 Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // Required parameters(필수 인자)
        private final int servingSize;
        private final int servings;

        // Optional parameters - initialized to default values(선택적 인자는 기본값으로 초기화)
        private int calories      = 0;
        private int fat           = 0;
        private int carbohydrate  = 0;
        private int sodium        = 0;

        // 생성자
        public Builder(int servingSize, int servings) { 
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val) {
            calories = val;
            return this;    // 이렇게 하면 . 으로 체인을 이어갈 수 있다.
        }
        public Builder fat(int val) {
            fat = val;
            return this;
        }
        public Builder carbohydrate(int val) {
            carbohydrate = val;
            return this;
        }
        public Builder sodium(int val) {
            sodium = val;
            return this;
        }
        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}
```

```java
// 객체 생성 방법1
NutritionFacts.Builder builder = new NutritionFacts.Builder(240, 8);
builder.calories(100);
builder.sodium(35);
builder.carbohydrate(27);
NutritionFacts cocaCola = builder.build();

// 객체 생성 방법2
// 각 줄마다 builder를 타이핑하지 않아도 되어 편리하다.
NutritionFacts cocaCola = new NutritionFacts
    .Builder(240, 8)    // 필수값 입력
    .calories(100)
    .sodium(35)
    .carbohydrate(27)
    .build();           // build() 가 객체를 생성해 돌려준다.
```

- 장점
    - 각 인자가 어떤 의미인지 알기 쉽다.
    - `setter` 메소드가 없으므로 변경 불가능 객체를 만들 수 있다.
    - 한 번에 객체를 생성하므로 객체 일관성이 깨지지 않는다.
    - `build()` 함수가 잘못된 값이 입력되었는지 검증하게 할 수도 있다.

#### Lombok의 `@Builder` 애테이션 사용
Effective Java의 Builder Pattern은 클래스 또는 생성자에 **롬복의 `@Builder` 애너터이션을 붙이면 쉽게 사용 가능**
객체 생성 방법은 동일함
```java
@Builder
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;
}
```

### 객체 생성을 유연하게 하기 위한 방법
빌더 패턴을 사용하면 하나의 빌더 객체로 여러 객체를 만드는 것이 가능
> 인자가 설정된 빌더는 훌륭한 추상적 팩토리다.
```java
public interface Builder<T> {
    public T build();
}
```
위와 같은 인터페이스를 만들고, 빌더 클래스가 implements 하게 하면 됨   
<br/>

## GoF Design Pattern(1994)
- 복잡한 인스턴스를 조립하여 만드는 구조로, **복합 객체를 생성할 때 객체를 생성하는 방법(과정)과 객체를 구현(표현)하는 방법을 분리**함으로써 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있는 디자인 패턴
- 생성과 표기를 분리해서 복잡한 객체를 생성
- 구성 객체
    - **Builder**: 빌더 인터페이스
    - **ConcreteBuilder**: 빌더 인터페이스 구현체로 부품을 합성하는 방식에 따라 여러 구현체 생성
    - **Director**: Builder를 사용해 객체를 생성
    - **Product**: Director가 Builder로 만들어낸 결과물
    > builder 는 부품을 만들고, director 는 builder가 만든 부품을 조합해 제품을 만든다고 할 수 있다.

### Builder 인터페이스
```cpp
/* Builder 인터페이스 */
class MazeBuilder {
    public :
        virtual void BuildMaze() { }
        virtual void BuildRoom(int room) { }
        virtual void BuildDoor(int roomFrom, int roomTo) { }
        virtual Maze* GetMaze() { return 0; }
    protected :
        MazeBuilder();
}
```

### Builder 구현체
- 빌더 구현체는 방과 문, 미로를 만든다.
- 방과 문을 몇 개를 만들고 어떤 순서로 조합하는지를 아는 것은 디렉터의 일이다.
- 다음과 같이 목적에 따라 여러 가지로 만들 수 있다.

```cpp
/* 표준적인 방, 문, 미로를 만드는 Builder 구현체 */
class StandardMazeBuilder : public MazeBuilder {
    public :
        StandardMazeBuilder();
        virtual void BuildMaze();
        virtual void BuildRoom(int);
        virtual void BuildDoor(int, int);

        Virtual Maze* GetMaze();
    private :
        Direction CommonWall(Room*, Room*);
        Maze* _currentMaze;
};

/* 미로는 만들지 않고 방과 문의 숫자를 세는 Builder 구현체 */
class CountingMazeBuilder : public MazeBuilder {
    public :
        CountingMazeBuilder();
        virtual void BuildMaze();
        virtual void BuildRoom(int);
        virtual void BuildDoor(int, int);
        virtual void AddWall(int, Direction);
        void GetCount(int &, int &) const;
    private :
        int _doors;
        int _rooms;
}
```

### Director

- 디렉터는 빌더에게 방을 몇 개 만들고, 문을 몇 개 만들 것을 지시하여 미로를 완성한다.
- 빌더는 시키는대로 방과 문만 잘 만들면 된다.

```cpp
/* 기본 미로를 만드는 Director */
Maze* MazeGame::CreateMaze(MazeBuilder& builder) {
    builder.BuilderMaze();
    builder.BuildRoom(1);
    builder.BuildRoom(2);
    builder.BuildDoor(1, 2);

    return builder.GetMaze();
}

/* 복잡한 미로를 만드는 Director */
Maze* MazeGame::CreateComplexMaze(MazeBuilder& builder) {
    builder.BuildRoom(1);
    // ...
    builder.BuildRoom(1001);

    return builder.GetMaze();
}
```

```cpp
Maze * maze;                    /* product */
MazeGame game;                  /* director */
StandardMazeBuilder builder;    /* builder */
game.CreateMaze(builder);
maze = builder.GetMaze();
```
