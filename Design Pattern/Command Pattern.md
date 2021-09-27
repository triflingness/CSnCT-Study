# Command Pattern

요구 사항을 요청에 대한 모든 정보를 포함한 객체로 캡슐화하는 행위 패턴이다.

요청을 매개변수로  요청 내역을 큐에 저장, 로그 기록, 작업 취소 기능을 지원한다.

- 요청을 생성하는 클라이언트와 실행하는 클라이언트를 분리한다.
- Command 객체는 "tokens"로, 실행을 요청하는 클라이언트가 실행하는 클라이언트로 전달된다.
- 요청 기능들을 캡슐화하여 호출자와 수신자 사이의 의존성을 제거한다.
- 다양한 기능 변경이 요구될 때 클래스 변경 없이 재사용이 가능하다.

### Command Pattern 구조

<img src="./images/command_structure.svg">

- **Client**
    - `Invoker` 를 사용하여 기능을 요청하는 클래스이다.
    - `ConcreteCommand` 를 생성하고, `Receiver` 를 포함한 모든 요청 매개 변수를 Command 생성자에 전달한다.
- **Invoker**
    - 기능 실행을 요청하는 `호출자, 발신자` 클래스이다.
    - 생성자를 통해 클라이언트에서 작성된 명령을 가져온다.
    - Command 객체에 대한 참조를 저장하는 필드가 필요하다.
- **Receiver**
    - `ConcreteCommand`  의 기능을 실행하기 위해 사용되는 `수신자` 클래스
    - `execute` 메서드를 구현할 때 필요하며, `Command` 명령의 대상이 되는 클래스 이다.
- **Command**
    - 실행될 기능을 수행하는 `execute` 메서드가  선언된 인터페이스
    - 일반적으로 명령을 실행하기 위한 메서드를 선언한다.
- **ConcreteCommand**
    - Command 를 구현하는 클래스
    - 실질적으로 실행되는 기능을 구현한다.

→ 실행될 기능을 캡슐화함으로써 기능의 실행을 요구하는 호출자(Invoker) 클래스와 실제 기능을 실행하는 수신자(Receiver) 클래스 사이의 의존성을 제거한다. 따라서 실행될 기능의 변경에도 호출자 클래스를 수정 없이 그대로 사용할 수 있다.
  
### **구현 방법**

1. 단일 실행 메서드를 포함한 Command Interface를 선언한다.
2.  Command Interface를 구현하는 ConcreteCommand Class에서 요청을 추출한다.
    1. 각 클래스는 실제 Receiver 객체를 참조와 요청 매개 변수를 저장하는 필드가 필요하다.
    2. 모든 값들은 Command Constructor를 통해 초기화해야 한다.
3. 호출자 역할을 하는 Invoker 클래스를 식별한다.
    1. Command를 저장하기 위한 필드를 추가해야 한다.
    2. 호출자는 Command Interface만을 통해서 명령을 통신한다.
    3. 호출자는 Command 객체를 만들지 않고 Client에서 가져온다.
4. 수신자에 직접 요청을 전달하는 대신에 명령을 실행할 발신자로 변경한다.
5. Client는 다음 순서로 개체들을 초기화한다.
    1. Receivers를 생성한다.
    2. Command를 작성하고, 필요에 따라 명령들을 수신자에 연결한다.
    3. 호출자를 만들고, 이를 특정 명령에 연결한다.

### 사용 예시 - remote control example

**Command Interface**

```java
interface Command{
	public void execute();
}
```

**Receiver class**

```java
class Light{
	public void on(){
		System.out.println("Light is on");
	}
	public void off(){ 
		7
		System.out.println("Light is off");
	}
}
```

**ConcreteCommand class**

```java
pclass LightOnCommand implements Command{
	Light light;

	// The constructor is passed the light it is going to control.
	// 생성자에 제어할 빛을 전달받는다.
	public LightOnCommand(Light light){
		this.light = light;
	}

	public void execute(){
		light.on();
	}
}
```

```java
class LightOffCommand implements Command{
	Light light;
	public LightOffCommand(Light light){
		this.light = light;
	}
	public void execute(){
		light.off();
	}
}
```

**Receiver class**

```java
class Stereo{
	public void on(){
		System.out.println("Stereo is on");
	}
	public void off(){
		System.out.println("Stereo is off");
	}
	public void setCD(){
		System.out.println("Stereo is set " + "for CD input");
	}
	public void setDVD(){
		System.out.println("Stereo is set"+ " for DVD input");
	}
	public void setRadio(){
	System.out.println("Stereo is set" + " for Radio");
	}
	public void setVolume(int volume){
		// code to set the volume
		System.out.println("Stereo volume set" + " to " + volume);
	}
}

class StereoOffCommand implements Command{
	Stereo stereo;
	public StereoOffCommand(Stereo stereo){
		this.stereo = stereo;
	}

	public void execute(){ 
		stereo.off();
	}
}

// and its corresponding command classes
class StereoOnWithCDCommand implements Command{
	Stereo stereo;
	public StereoOnWithCDCommand(Stereo stereo){
		this.stereo = stereo;
	}

	public void execute(){
		stereo.on();
		stereo.setCD();
		stereo.setVolume(11);
	}
}
```

**Invoker class - A Simple remote control with one button**

```java
class SimpleRemoteControl
{
	Command button; // only one button

	public SimpleRemoteControl(){}

	public void setCommand(Command command){
		// set the command the remote will
		// execute
		button = command;
	}

	public void buttonWasPressed(){
		button.execute(); 
	}
}
```

**Client class**

```java
class RemoteControlTest
{
	public static void main(String[] args){
		SimpleRemoteControl remote = new SimpleRemoteControl();
		Light light = new Light();
		Stereo stereo = new Stereo();

		// we can change command dynamically
		remote.setCommand(new LightOnCommand(light));
		remote.buttonWasPressed();
		remote.setCommand(new StereoOnWithCDCommand(stereo));
		remote.buttonWasPressed();
		remote.setCommand(new StereoOffCommand(stereo));
		remote.buttonWasPressed();
	}
}
```

### 사용 경우

- 작업 개체를 매개 변수화하는 경우
    - 특정 메서드 호출을 독립 개체로 바꿀 수 있어, 명령을 메서드 인수로 전달하거나 다른 객체에 저장하고 런타임에 링크된 명령을 바꿀 수도 있다.
- 작업을 큐에 넣고 실행을 예약하거나 원격으로 수행할 경우
    - 명령을 직렬화할 수 있어, 파일이나 데이터베이스에 쉽게 쓸 수 있는 문자열로 변환할 수 있다. 따라서 명령 실행을 지연하거나 예약할 수 있다.
- 작업 취소를 구현할 경우
    - 작업을 취소할 경우 실행된 작업의 기록이 필요하다. 해당 기록은 실행된 모든 명령 개체와 응용 프로그램의 상태에 대한 백업을 포함한 스택이다.
    - 하지만 공개되지 않은 응용 프로그램의 상태를 저장할 수 없고 상태 백업은 상당한 RAM 소비를 야기한다.

### 장점

- **Single Responsibility Principle,** 작업을 수행하는 클래스에서 작업을 호출하는 클래스를 분리할 수 있다.
- **Open/Closed Principle**, 기존의 Client 코드를 변경하지 않고 새로운 명령을 추가할 수 있다.
- 실행 취소, 작업의 재실행을 구현할 수 있다.
- 작업 예약을 구현할 수 있다.
- 간단한 명령 집합을 복잡한 명령으로 조합할 수 있다.

### 단점

- 호출자와 수신자 사이에 새로운 계층을 추가해서 코드가 더욱 복잡해질 수 있다.

---

참고

[https://sourcemaking.com/design_patterns/command](https://sourcemaking.com/design_patterns/command)

[https://refactoring.guru/design-patterns/command](https://refactoring.guru/design-patterns/command)

[https://www.tutorialspoint.com/design_pattern/command_pattern.htm](https://www.tutorialspoint.com/design_pattern/command_pattern.htm)

[https://velog.io/@kwj1270/Command-pattern](https://velog.io/@kwj1270/Command-pattern)

[https://leveloper.tistory.com/156](https://leveloper.tistory.com/156)

[https://sun-22.tistory.com/16](https://sun-22.tistory.com/16)
