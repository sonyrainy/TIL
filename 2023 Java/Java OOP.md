- **객체 간 상속은 어떤 의미일까?**
  
상속(=물려 받는 것)
상위 클래스(일반적), 하위 클래스(구체적)는 일관성이 존재한다.
하위 클래스는 상위 클래스를 모두 포함하고 있겠다고 볼 수 있다.

>상위(상속하는 클래스) : 상위 클래스, parent class, base class, super class
>
>하위(상속받는 클래스) : 하위 클래스, child class, derived class, sub class
```
class 자식 extends 부모 {
  ...
}
```

**ex) Human**
```
class Mammal{
  ...
}
```
```
class Human extends Mammal {
  //(Human을 사용할 것인데, 그것은 Mammal의 기능을
  //모두 사용할 수 있도록 확장한다는 느낌이다.)
}
```
→ extends(확장) 키워드 뒤에는 단 하나의 클래스만 올 수 있다.(C++은 더 가능하다.)

- **ex) 상속을 활용한 멤버십 클래스 구현**
> 멤버십 시나리오 → Customer, VIPCustomer을 구분하여 서비스를 제공하기


- **상속에서 클래스 생성 과정, 형 변환**
하위 클래스를 생성하면 상위 클래스가 먼저 생성된다.

즉, new VIPCustomer()을 호출하면, Customer()가 먼저 호출된다는 것이다.

- **super 키워드**

하위 클래스에서 가지는 상위 클래스에 대한 참조 값이다. super()은 상위 클래스의 기본 생성자를 호출한다.

Customer에서 기본 생성자가 없고, Customer(int cumstomerId, String customerName) {...} 이런 식으로만 생성자가 존재한다면, 
VIPCustomer에서 public VIPCustomer(){...}을 사용할 수 없게 된다.

그렇지만 Customer(int customerId, String customerName)이 있고, VIPCustomer(int customerId, String customerName)이 있는 경우를 보았을 때,

VIPCustomer(int customerId, String customerName)을 사용하기 위해서, VIPCustomer 내부에 super(customerId, customerName)을 작성해야 한다.

```
public class VIPCustomer extends Customer {
    public VIPCustomer(int customerId, String customerName) {
        super(customerId, customerName); //super를 사용하여 Customer의 생성자를 호출한다.
        //VIPCustomer의 추가적인 초기화 로직을 여기에 추가 가능하다.
    }
}
```

```super(customerId, customerName);``` 이 부분을 통해, VIPCustomer 객체를 생성할 때, Customer 클래스의
필드가 초기화되도록 할 수 있다.

+) ```Customer vc = new VIPCustomer();```으로도 선언이 가능하다. 그렇게 생성된 vc는 Customer 클래스의 멤버 변수만 사용가능하며, VIPCustomer 클래스의 멤버변수는 선언이 불가능하다.
(+) vc 변수 타입 : Customer, 인스턴스 타입 : VIPCustomer)

즉, VIPCustomer() 생성자로, VIPCustomer 클래스의 모든 멤버 변수에 대한 메모리는 생성되었으나, 변수 타입이 Customer이라서 실제 접근 가능한 변수나 메서드는 Customer의 변수와 메서드가 되는 것이다.


- **메서드 재정의(overriding, 오버라이딩)_(다형성)**

상위 클래스에서 정의된 메서드를 하위 클래스에서 새롭게 구현하여 재정의할 수 있다.
상위 클래스와 하위 클래스는 반드시 상속 관계에 있어야 하며, 메서드명, 매개변수, 반환값 등의 시그니처가 동일해야 한다.
상위 클래스에서 정의된 메서드를 하위 클래스에서 다른 구현으로 대체할 수 있으므로, 하위 클래스에서 상위 클래스의 메서드와 같은 이름의 메서드를 호출 할 때, 해당 클래스에 맞는 새로운 동작을 수행 할 수 있다.

**ex) Animal**
```
class Animal {
	public void makeSound() {
		System.out.println("동물이 소리를 냅니다.");
	}
}
class Dog extends Animal {
	@Override //해당 부분은 재정의된 메서드라는 것을 알려준다.
	public void makeSound() {
		System.out.println("멍멍");
	}
}
class Cat extends Animal {
	@Override
	public void makeSound() {
		System.out.println("냐옹");
	}
}
public class Main {
	public static void main(String[] args) {
		Animal animal1 = new Animal();
		Animal animal2 = new Dog();
		Animal animal3 = new Cat();

		animal1.makeSound(); //동물이 소리를 냅니다.
		animal2.makeSound(); //멍멍
		animal3.makeSound(); //냐옹
  }
}
```

자바는 모든 메서드가 가상 메서드이다. 인스턴스에 오버라이딩(재정의)되어 있다면, 생성된 인스턴스의 메서드가 호출된다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/5011468d-e90b-480d-a4d6-20acc2d3bf21)

- **상속**
> **IS-A 관계** : 하나의 변수에 의존하여 여러 분기문(else-if) 등을 사용할 때, 상속을 사용할 수 있다.
>
>**ex) 강아지는 동물(강아지 클래스가 동물 클래스를 상속받는다.)**

> **HAS-A 관계**(일반적으로 재사용을 하는 경우) : Student가 Subject를 포함하는 경우, Library를 구현할 때 ArrayList를 생성하여 사용하는 경우 등의 경우에는 상속하는 경우라고 보기 어렵다. 일반적인 포함 개념의 관계이다.
>
>**ex) Computer - Cpu, Ram, MainBoard**


- **다운 캐스팅(instanceof 활용)**
하위(자식) 클래스가 상위(부모) 클래스로 변환되는 것이 업캐스팅, 그 역이 다운 캐스팅이다.

오버라이딩으로 관리하는 것이 나을 수 있지만, 다운 캐스팅이 필요한 경우도 존재한다.

부모 → 자식으로 변환하는 것은 자동으로 이루어지지 않으므로, 명시적으로 타입(다운) 캐스팅을 해주어야 한다.

여기서 다운 캐스팅을 수행하기 전에, instanceof 연산자로 해당 객체가 실제 자식 클래스의 객체인지 확인해야 한다. 아니라면 error가 발생한다.

```
Animal animal = new Dog();

if (animal instanceof Dog) {
	Dog dog = (Dog) animal; // 다운 캐스팅
	dog.bark();
}
```

> 1. ```Animal animal = new Dog();```은 Dog 클래스의 객체를 Animal 클래스의 참조변수로 생성한다.
> Dog 클래스가 Animal의 하위 클래스이므로 가능하다.
> 2. instanceof 연산자로 animal이 Dog의 클래스의 객체인지 확인한다.
> 3. ```Dog dog = (Dog) animal;```은 animal을 Dog 클래스로 다운캐스팅한다.
> 확인되었기 때문에 안전하게 다운 캐스팅한다고 볼 수 있다.
> 4. 다운캐스팅 된 객체의 메서드를 호출한다.


- **추상 클래스(abstract class) 구현하기**
추상 클래스란?
> 구현 코드 없이 메서드의 선언만 있는 추상 메서드를 포함한 클래스이다.
선언 추상 메서드의 경우 abstract 예약어를 사용해야 한다.

이 메서드의 시그니처(메서드명, 매개변수 타입, 반환 타입 등을 명시하는 것)를 선언하는 것만으로도, 
그렇게 하위 클래스에서 추상 메서드를 구현하도록 하는 것도 상위 클래스에서 직관적으로 볼 수 있게 되는 것으로 볼 수 있다.

추상 클래스 자체는 new 키워드를 활용할 수 없다.(인스턴스화 할 수 없다.)

+) abstract로 선언된 메서드를 가진 클래스는 abstract로 선언한다. 모든 메서드가 구현되어 있는 클래스라도 abstract로 
선언되면 추상 클래스로 인스턴스화 할 수 없다.

추상 클래스의 추상 메서드는 하위 클래스에게 상속되고 하위 클래스에서 구체적으로 구현한다. 상속용으로 사용하는 것이다.
즉, 추상 메서드는 하위 클래스가 구현해야 하는 메서드라고 볼 수도 있다.

추상 클래스 내의 구현된 메서드는 하위 클래스가 공통으로 사용하는 메서드이다.(필요에 의해 하위 클래스에서 재정의 될 수도 있다.)

- 추상 클래스 응용_(템플릿 메서드 패턴)
  - 템플릿 메서드 패턴(추상적으로 흐름을 생성해두는 것)
  추상 메서드나 구현된 메서드를 활용하여 코드의 흐름(시나리오)를 정의하는 패턴이다. 즉, 상위 클래스에서 처리의 뼈대를 결정 후, 하위 클래스에서 구체적인 내용을 결정하는 패턴이다.

  - final을 선언하여 하위 클래스에서 재정의 할 수 없게 한다.

**ex) Car에서 run() 메서드**
```
public abstract class Car {
	public abstract void drive();
	public abstract void stop();
	public void startCar(){
		System.out.println(”시동을 켭니다.”);
	}

	public void turnOff(){
		System.out.println(”시동을 끕니다.”);
	}

	final public void run() {
		startCar();
		drive();
		stop();
		turnOff();
	}
}
```

+) final을 메서드에 정의하면 overriding 할 수 없게 된다. class에 사용하면 상속될 수 없게 되고, 변수에 사용하면 상수가 된다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/aad09f1d-6f50-4686-90b3-b4c21daa4c89)

+) intellij에서 새로운 클래스 생성 → alt + insert

+) 코드에 마우스를 갖다대면 implement methods가 뜨거나, alt+insert 하여 @Override를 이용할 수 있다.

+)
Car class에 있는 함수 중, abstract가 없는 함수라면, 오버라이딩의 여지가 있는 함수이다. 즉, 해당 함수를 상속받은 모든 클래스가 구현될 필요는 없다.

- 상수 값 정의하기_(여러 자바 파일에서 사용이 가능한)
상수들을 그냥 몰아서 .java 파일을 만들어 줄 수도 있는데, 그것도 괜찮은 방법이다.

ex) DEFINE
1.1.) Define.java
```
public class Define {
	public static final in MIN = 1;
	public static final in MAX = 999999;
	public static final double PI = 3.14;
}
```

1.2.) UsingDefine.java
```
public class UsingDefine {
	public static void main(String[] args) {
		System.out.println(Define.MIN);
		System.out.println(Define.MAX);
		System.out.println(Define.PI);
	}
}
```

- 인터페이스(interface)_구현(implement)

1. (public abstract)모든 메서드는 기본적으로 추상메서드(선언은 있지만, 구현 내용이 없는 메서드)이다.
자바 8부터는 디폴트 메서드와 정적 메서드를 지원하므로, 일부 메서드가 구현 코드를 가질 수 있다.
그렇지만, 인터페이스의 목적은 여전히 메서드 선언을 제공하는 것이고, 구현은 하위 클래스에서 제공하는 것이 일반적이다.

2. (public static final)모든 변수는 상수로 선언된다.

3. implements 키워드 뒤에는 여러 개의 interface가 올 수 있다. 구현 코드가 없으니 모호함이 발생하지 않기 때문이다.

**ex) MyClass 클래스가 MyInterface1, 2에서 선언된 모든 메서드를 구현해야 한다.**
```
public class MyClass implements MyInterface1, MyInterface2 {
    // MyInterface1과 MyInterface2에서 선언된 메서드를 모두 구현해야 함
    // 추상 메서드를 오버라이드하거나, 디폴트 메서드를 재정의할 수 있음
    @Override
    public void method1() {
        // 구현 내용
    }

    @Override
    public void method2() {
        // 구현 내용
    }
}
```

- 인터페이스와 상속의 차이점
- 







---
23.09.02 내로 추가할 예정











