# Bridge Pattern

`기능 클래스 계층` 과 `구현 클래스 계층` 을 분리하여 각자 독립적으로 변형이 가능하고 확장이 가능하도록 하는 패턴

- 기능 클래스 계층
    - 상위 클래스를 상속받는 하위 클래스에서 새로운 기능을 추가하는 계층
    - 상위 클래스는 기본적인 기능을 가지고 하위 클래스는 추가되는 새로운 기능을 가짐
- 구현 클래스 계층
    - 인터페이스(API)를 구현하는 객체가 존재할 때 구현 클래스 계층이라고 함
    - 상위 클래스는 추상 메소드에 의해 인터페이스(API)를 규정하고 하위 클래스는 구체적인 메소드에 의해 그 인터페이스를 구현하는 클래스 계층

→ `기능 클래스 계층` 과 `구현 클래스 계층` 을 독립된 클래스 계층으로 구현하고 두 개의 클래스 계층 사이를 연결하는 패턴

<img src="https://github.com/triflingness/CSnCT-Study/blob/aecf555f0fd9e8f91fa43e73969e22d934a36373/Design%20Pattern/images/bridgepatternstructure.png">

### Bridge Pattern 구조

- **Abstraction (추상화)**
    - 기능 클래스 계층의 상위 클래스
    - 기본적인 기능만 정의함
- **Refind Abstraction (개선된 추상화)**
    - 기능 클래스 계층의 하위 클래스
    - 기능 계층에서 새로운 부분을 확장한 클래스(기능 추가)
- **Implementor (구현자)**
    - 구현 클래스 계층의 상위 클래스
    - Abstraction의 기능을 구현하기 위한 인터페이스(API) 정의
- **Concrete Implementor (구체적인 구현자)**
    - 구현 클래스 계층의 하위 클래스
    - 실제 기능 구현

### 사용 예시

Abstraction (추상화) - 공통된 기능 정의

```jsx
// 기능 클래스 계층
public class Display {
	
	// impl 필드는 Display 구현을 나타내는 인스턴스 입니다. 
	// 이 필드가 두 클래스 계층의 '다리'가 됩니다.
	private DisplayImpl impl; 

	public Display(DisplayImpl impl) {
		this.impl = impl;
	}
	
	public void open(){
		impl.rawOpen();
	}
	
	public void print(){
		impl.rawPrint();
	}
	
	public void close(){
		impl.rawClose();
	}
	
	public final void display(){
		open();
		print();
		close();
	}
}
```

Refind Abstraction (개선된 추상화) - 기능 추가

```jsx
// 기능 클래스 계층
public class CountDisplay extends Display {

	public CountDisplay(DisplayImpl impl) {
		super(impl);
	}

	public void multiDisplay(int times){
		open();
		for(int i = 0; i< times; i++){   	
		// times회 반복해서 표시한다
			print();
		}
		close();
	}
}
```

Implementor (구현자) - 구현 클래스

```jsx
// 구현 클래스 계층
public abstract class DisplayImpl {
	public abstract void rawOpen();
	public abstract void rawPrint();
	public abstract void rawClose();
}
```

Concrete Implementor (구체적인 구현자)

```jsx
// 구현 클래스 계층
public class StringDisplayImpl extends DisplayImpl {
	
	private String string;			   // 표시해야 할 문자열
	private int width;				   // 바이트 단위로 계산할 문자열의 '길이'
	

	public StringDisplayImpl(String string) {		// 생성자에서 전달된 문자열 string을
		this.string = string;						// 필드에 기억해둔다.
		this.width = string.getBytes().length; 	    // 그리고 바이트 단위의 길이도 필드에 기억해두고 나중에 사용한다.
	}

	@Override
	public void rawOpen() {
		printLine();
	}

	@Override
	public void rawPrint() {
		System.out.println("|" + string + "|");    // 앞뒤에 "|" 를 붙여서 표시한다.
	}

	@Override
	public void rawClose() {
		printLine();

	}
	
	private void printLine() {
		System.out.print("+");		           // 테두리의 모서리를 표현하는 "+" 마크를 표시한다.
		for (int i = 0; i < width; i++) {	   // width개의 "-"를 표시해서
			System.out.print("-");			   // 테두리 선으로 이용한다.
		}
		System.out.println("+");	           // 테두리 모서리를 표시하는 "+" 마크를 표시한다.
	}

}
```

Main class

```jsx
public class Main {
	public static void main(String[] args) {
		
		Display d1 = new Display(new StringDisplayImpl("Hello, Korea!"));
		Display d2 = new CountDisplay(new StringDisplayImpl("Hello, World!"));
		
		CountDisplay d3 = new CountDisplay(new StringDisplayImpl("Hello, Universe!"));
		
		d1.display();
		d2.display();
		d3.display();
		
		d3.multiDisplay(5);
	}
}
```

### 사용 이유

- 두 계층을 분리하여 확장이 편리하다. 서로 변경되어도 클라이언트에는 영향이 없다.
- 유지보수를 간결하게 하기 위한 유용한 패턴
- 여러 플랫폼에서 사용해야할 그래픽스 및 윈도우 처리 시스템에서 유용하게 사용된다.

*단점* → 브릿지 패턴을 매우 응집력이 있는 클래스에 적용하면 코드가 더욱 복잡해질 수 있다.

---

참고

[https://lee1535.tistory.com/102](https://lee1535.tistory.com/102)

[https://m.blog.naver.com/tradlinx0522/220928963011](https://m.blog.naver.com/tradlinx0522/220928963011)

[https://joycestudios.tistory.com/38](https://joycestudios.tistory.com/38)

[https://lktprogrammer.tistory.com/35](https://lktprogrammer.tistory.com/35)

[https://pacientes.github.io/posts/2020/11/design_pattern_bridge/](https://pacientes.github.io/posts/2020/11/design_pattern_bridge/)
