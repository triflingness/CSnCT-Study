# Prototype

- 처음부터 일반적인 원형을 만들어 놓고 그것을 복사한 후 **필요한 부분만 수정하여 사용**하는 패턴으로, 생성할 객체의 원형을 제공하는 인스턴스에서 생성할 객체들의 타입이 결정되도록 설정하며 **객체를 생성할 때 갖추어야 할 기본 형태가 있을 때 사용되는 디자인 패턴**
- 기존 객체를 복제함으로써 객체를 생성
- 객체를 생성하는 데 비용(시간과 자원)이 많이 들고(ex. DB참조 등), 비슷한 객체가 이미 있는 경우에 사용 → **객체 생성의 비용을 줄일 수 있음**
- 복사를 위하여 Java에서 제공하는 `clone()` 사용
- 구성 객체
    - ConcretePrototype
    - Client

## 예제

```java
// Shape abstract Class
public abstract class Shape implements Clonable{ // clone() 메소드를 사용하기 위해 Cloneable 인터페이스를 구현
	protected Type types;
	
	abstract void draw(); // 공통 메소드인 draw()는 추상 메소드로 정의
	
  // 하위 클래스에서 사용할 clone()은 공통으로 동작하는 메소드를 정의
	@Override
	public Object clone() throws CloneNotSupportedException{ 
		Object clone = null;

		try {
			clone = super.clone();
		} catch (RuntimeException e){
			e.printStackTrace();
		} catch (CloneNotSupportedException e){
			// Cloneable 인터페이스를 구현했기 때문에 해당 예외는 발생하지 않음
			e.printStackTrace();
		}
		return clone;
	}
}
// 상황에 따라 clone() 메소드를 공통으로 동작하지 않게 할 경우, 해당 클래스 자체를 interface로 선언 후
// clone() 메소드 정의를 하위 클래스에 위임하는 방식도 존재
```

```java
// Circle, Triangle, Rectangle Class
public class Circle extends Shape { // Shape 상속
	public Circle() {
		this.type = Type.CIRCLE;
	}

	@Override
	void draw() { // 재정의
		System.out.println("[Circle]입니다.");
	}
}
```

```java
// ShapeStore Class
public class ShapeStore {
	private static Map<Type, Shape> shapeMap = new HashMap<Type, Shape>();
	
	// 복제에 사용할 객체를 인스턴스화해서 shapeMap에 저장
	public void registerShape(){
		Rectangle rec = new Rectangle();
		Circle cir = new Circle();
		Triangle tri = new Triangle();
		
		shapeMap.put(rec.type, rec);
		shapeMap.put(cir.type, cir);
		shapeMap.put(tri.type, tri);
	}

	// 객체의 복사본을 반환
	public Shape getShape(Type type) {
		return (Shape) shapeMap.get(type).clone();
	}
}
```

```java
// Client
public class Main{
	public static void main(String[] args){
	ShapeStore manager = new ShapeStore();
	manager.registerShape();
	
	Circle cir1 = (Circle)manager.gerShape(Type.CIRCLE);
	cir1.draw(); // [Circle]입니다.
	Circle cir1 = (Circle)manager.gerShape(Type.CIRCLE);
	cir1.draw(); // [Circle]입니다.
	
	Rectangle rec1 = (Rectangle)manager.getShape(Type.RECRANGLE);
	rec1.draw(); // [Rectangle]입니다.

	Triangle tri1 = (Triangle )manager.getShape(Type.TRIANGLE);
	tri1.draw(); // [Triangle ]입니다.
	}
}
```

### 고려사항

예제에서 사용된 `clone()` 메소드는 Object 클래스의 메소드로 얕은 복사이므로 깊은 복제를 사용해야 할 경우 `clone()` 메소드를 재정의 해야 함

##### 참고
- https://readystory.tistory.com/122
- https://lee1535.tistory.com/76
- https://catsbi.oopy.io/16109e87-3c7e-4c6e-9816-c86e6b343cdd
