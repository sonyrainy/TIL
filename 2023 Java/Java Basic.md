# java 기초

- **입력 받기**
 
`Scanner scanner = new Scanner(System.in);`
> 이런 식으로 Java에서 Scanner을 이용하여, C언어의 scanf처럼 사용할 수 있다.

- **객체**

객체가 생성되면 instance 라고 하고, 생성된 인스턴스는 heap 메모리로 간다.

하나의 클래스에는 반드시 하나 이상의 생성자가 존재해야 한다. 
생성자를 구현하지 않을 경우, 컴파일러가 자동으로 기본 생성자 코드를 넣어준다. 

기본 생성자는 매개 변수가 없고, 구현부가 존재하지 않는다.

클래스는 객체의 청사진으로 볼 수 있다.

**ex) Student 예시**

**1.1) Student.java**
```
public class Student {
  public int studentID;
  public String studentName;
  public String address;

  public Student(int id, String name) { //생성자 생성
    studentID = id;
    studentName = name;
  }
}
```

**1.2) StudentTest.java**
```
public class StudentTest {
  public static void main(String[] args) {
    Student studentSon = new Student(1234, “현진”); //studentSon 객체 생성
**//Student studentSon = new Student();, 매개변수를 받는 생성자를 생성했는데,
//기본 생성자를 호출하는 경우, error가 발생한다.**
  }
}
```

- **생성자 오버로딩**

학번과 이름을 받는 생성자를 이전에 만들었는데, 학번만을 입력 받거나 이름만을 입력받는 생성자를 만들고자 하는 경우가 있다고 치자.

그런 경우, 생성자 명이 클래스명과 동일해야 하기 때문에, 매개 변수가 다른 똑같은 이름의 생성자들을 여러 개 만들어야 한다. 

이렇게 **생성자를 두 개 이상 구현**하는 경우를 **생성자 오버로딩**이라고 한다.


- **객체 지향 프로그램은 어떻게 구현하는가?**

>1) 객체를 정의한다.
>
>2) 각 객체의 속성을 멤버 변수로, 역할을 메서드로 구현한다.
>
>3) 각 객체 간의 협력을 구현한다.


- **(String이라는) 객체로 되어있는 자료형 => 참조형 변수**

- **클래스**

객체의 청사진이다. 클래스는 대문자로 시작하는 것이 관행이다. 

.java 파일 하나에 클래스는 여러개가 있을 수 있으나, **public 클래스는 하나**이고, **public 클래스와 .java 파일의 이름이 동일**해야 한다.

camel notation(첫 소, 단어 바뀔 때 첫 문자 대문자)으로 변수명, 메서드명을 정의한다.

- **함수**

하나의 기능을 수행하는 일련의 코드이다. 되돌려주는 값이 없으면 void를 함수타입으로 사용한다.

> 함수는 되도록 간결하고, 이름에 맞는 하나의 기능을 제공하도록 한다.

ex) addNum 예시
```
int n1 = 10;
int n2 = 20;

public static int addNum(int num1, int num2){
  return num1+num2;

}
```

+) 객체의 속성은 멤버 변수로, 객체의 기능은 메서드로 구현한다고 볼 수 있다.

- **method**

객체의 기능을 구현하기 위해 클래스 내부에 구현되는 함수이다. C++에서는 멤버함수라고도 한다.

메서드를 구현함으로써 객체의 기능이 구현된다. 메서드의 이름은 그 객체를 사용하는 객체에 맞게 짓는 것이 좋다.

- **module**

 프로그램을 구성하는 요소, 관련된 데이터와 함수를 하나로 묶은 단위이다.
```
Student studentSon = new Student();
//studentSon은 생성된 객체를 가리키는 참조 변수라고 한다.
studentSon.studentName = "Son";
studentSon.studentAddress = "Daegu"

System.out.println(studentSon); //객체의 가장 앞 heap 메모리 주소가 같이 나온다.
```

- **인스턴스 생성과 힙 메모리**

new 키워드와 같이 생성된 Student를 우리는 인스턴스라고 한다. 각각의 인스턴스는 각자 다른 address를 가진다. 인스턴스는 생성되어 힙 메모리에 할당된다.

객체 : 실제 클래스 기반으로 생성된 인스턴스(객체)는 각각 다른 멤버 변수를 갖는다. Student 클래스로 생성된 인스턴스는 각각 다른 이름, 학번, 학년 등을 가진다.

**클래스는 코드의 상태, 인스턴스는 힙 메모리에 올라와있는 상태를 말한다.**

new 키워드를 사용하여 각각의 인스턴스마다 다르게 생성되는 변수가 있다. 그 변수를 인스턴스 변수라고도 한다.

```
public class Student {
  int studentId;
  String studentName;
  String studentAddress;

  public void showStudentInfo) {
    System.out.println(studentName + ", " + studentAddress);
  }
  public String getStudentName() {
    return studentName;
  }
}
```
위 코드에서 **studentId, studentName, studentAddress**가 인스턴스 변수라고 볼 수 있다.

- **heap 메모리(동적으로 할당되는 메모리)**

생성된 인스턴스는 동적메모리(heap 메모리)에 할당된다.
(C나 C++에서는 사용한 동적메모리를 프로그래머가 해제시켜야 한다.
따라서 C나 C++에서는 free()나 delete를 이용해야 한다.)

자바는 가비지 컬렉터가 동적메모리 해제(필요없게 된 영역 해제)를 주기적으로 해준다.
![image](https://github.com/sonyrainy/TIL/assets/91364766/664fad9e-8384-415e-95ed-5526093a3760)


- **용어정리**
>
>객체 : 객체지향프로그래밍의 대상, 생성된 인스턴스
>
>클래스 : 객체를 프로그래밍하기 위해 코드로 정의해둔 상태
>
>인스턴스 : new 키워드를 사용하여 클래스를 메모리에 생성한 상태
>
>멤버 변수 : 클래스의 속성, 특성
>
>메서드 : 멤버 변수를 이용하여 클래스의 기능을 구현한 함수
>
>참조 변수 : 메모리에 생성된 인스턴스를 가리키는 함수
>
>참조 값 : 생성된 인스턴스의 메모리 주소값

- **생성자**

new Student();를 보고 생성자라고 한다.

디폴트 생성자(매개변수와 구현부가 존재하지 않는 생성자)는 클래스 이름과 똑같다.

객체 생성할 때는 생성자를 꼭 써야한다.

생성자는 반환 값이 없고, 클래스 이름과 동일하다. 대부분의 생성자는 외부에서 접근이 가능하지만, 필요에 의해 private으로 생성될 수도 있다.

>**1) 생성자는 객체를 생성할 때 호출되는 메서드이며, 클래스 내부에 정의되어 있다. 생성자의 이름은 클래스 이름과 동일하다.**
>
>**2) 생성자는 인스턴스 변수를 초기화하는 역할을 한다. 즉, 객체가 생성될 때 필요한 값들을 인자로 받아 초기화하는 역할을 수행한다.**
>
>**3) 생성자는 반환 타입이 없다. 따라서, 생성자를 호출할 때는 'new' 키워드를 사용하여 호출하며, 반환값이 없는 것을 확인할 수 있다.**



- **참조자료형**

기본 int, long, float, double 등으로, 몇 byte가 할당되는 것이 있는 자료형이다.

+) **객체가 변수의 자료형이 되는 경우는 참조 자료형**이다.

참조자료형을 쓸 때는 해당 변수를 생성하고 사용해야 한다.

**1.1) Student.java**

```
public class Student {

	ins studentId;

	String studentName;

  /*
	int koreanScore;
	int mathScore;
	String koreanName;
	String mathName;
  */

	Subject korean;
	Subject math;//위 Subject(과목) 관련된 코드보다 이게 더 유지보수에 좋다.

// 이제 생성자를 생성하자
	public Student(int id, String name) {
		this.studentId = id;
		this.studentName=name;

		korean = new Subject();
		math = new Subject()
	}
}
```

**1.2) Subject.java**

```
public class Subject {
	int score;
	String subjectName;
}
```

> 하나의 클래스는 그 클래스에 해당되는 속성만 가지고 있는게 좋다.

- **접근 제어 지시자**

>**private** : **같은 클래스 내부에서만** 접근 가능(외부 클래스, 상속 관계의 클래스에서도 접근 불가)
>
>**default(아무 것도 없음)** : 같은 패키지 내부에서만 접근 가능(상속 관계라도 패키지가 다르면 접근 불가)
>
>**protected** : 동일 패키지 상속관계의 클래스에서만 접근 가능하며, 그 외 외부에서는 접근 불가
>
>**public** : 어디서든 접근 가능

- **외부에서 private을 알고 싶으면(보여주기만)? : get**
```
public int getStudentId() {
  return studentId;**
    
}
``` 

> get을 활용해서, 외부에서 볼 수 있있도록 할 수 있다.

- **그 정보를 저장할 수 있도록 하기 위해서는? : set**
```
public in setStudentId(String studentName) {
  this.studentName = studentName;
}
```

> 위와 같은 방식으로, 외부에서 수정할 수도 있다.

- +) 외부에 제공은 하지만, 외부에서 수정되지는 않도록 하고 싶은 경우

→ **get은 제공하고, set은 제공하지 않으면 된다.**

**+) boolean은 초기값이 false이다. 해당 클래스에서 초기값을 true로 주고 싶은 경우**
```
public class BirthDay {
  private boolean isValid;

    pulbic BirthDay() {
      isValid = true;
    }
}
```

- **캡슐화**

꼭 필요한 정보와 기능만 외부에 오픈한다.

정보를 클래스화 해서 멤버 변수와 메서드를 감추고 외부에 통합된 인터페이스만을 제공하여 일관된 기능을 구현하게 한다(setter, getter을 적절하게 활용한다.).

각각의 메서드나 멤버 변수에 접근함으로써 발생하는 오류를 최소화한다.


- **객체 자신을 가리키는 this(this. : 현재 객체를 참조, this() : 다른 생성자를 호출하는 용도)**
    - **this가 하는 일**
>→ 인스턴스 자신의 메모리를 가리킨다.
>
>→ 생성자에서 또 다른 생성자를 호출할 때 사용한다. 생성자 오버로딩일 때, 하나의 생성자에서 다른 생성자를 호출하는 경우가 있는데, 그 경우에 사용한다. 
>
>→ 자신의 주소(참조값)을 반환한다. 

this.year의 year은 heap 메모리의 year이다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/85e1c274-348a-4d28-aedd-c7895409193b)

- **생성자에서 다른 생성자를 호출하는 경우, 인스턴스의 생성이 완전하지 않은 상태라서, this() statement 이전에 다른 statement를 사용할 수 없다(statement==동작, 상태, 명령문).**

**ex)**
```
public class Person {
  String name;
  int age;
  public Person() {
    // age = 10; error 발생
    this(이름없음, 1); // 즉, 이 부분의 코드가 없으면 public Person(){...} 부분에서 다른 statement는 사용 불가능하다.
    age = 10; // 위에서 this로 초기화한 후, 여기서 age를 사용할 수 있다.
  }
  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }
  public Person getPerson() {
    return this;
    //자기 자신의 주소를 반환할 때 타입은 클래스의 타입을 사용하면 된다.
  }
}
```

- **객체 간의 협력**
[(버스와 지하철을 타는 예제 프로그래밍)](https://velog.io/@ldevlog/14.-%EB%B2%84%EC%8A%A4-%ED%83%80%EA%B3%A0-%ED%95%99%EA%B5%90-%EA%B0%80%EB%8A%94-%ED%95%99%EC%83%9D%EC%9D%98-%EA%B3%BC%EC%A0%95%EC%9D%84-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9C%BC%EB%A1%9C-%EA%B5%AC%ED%98%84%ED%95%B4%EB%B3%B4%EA%B8%B0)

James와 Tomas는 각각 버스와 지하철을 타고 학교에 간다.

James는 5000원을 가지고 있었고, 100번 버스를 타며 1000원을 지불한다.

Tomas는 10000원을 가지고 있었고, 초록색 지하철을 타면서 1200원을 지불한다.

몇 번 버스(어느 색 지하철)를 몇 명이서 탔는지, 얼마의 수입이 있는지를 출력해야 한다.

→ 두 학생이 버스와 지하철을 타는 상황을 구현해보기.

- **static 변수**

여러 인스턴스에서 공통(공유)으로 사용하는 변수를 선언하자(static 변수, 변수의 유효범위)

ex) 새로운 학번을 생성할 때, 생성하는 학번의 기준을 공유하면 쉽게 생성할 수 있다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/3e0cad36-b220-4b54-a1cc-56344f5a2e33)

+) **인스턴스 변수**는 **힙 메모리**, **스태틱 변수**는 **데이터 영역 메모리**에 생성된다.

+) generate getter setter 으로 하면 바로 받고 쓰고를 할 수 있는, get~ set~을 바로 생성할 수 있다.

**ex) static 변수 예제**

![image](https://github.com/sonyrainy/TIL/assets/91364766/d10c622f-6d51-423e-af83-ab55edf9b0a3)

→ employeeKim.serialNum++;으로 했는데 employeeLee.serialNum을 출력했을 때도 1001이 되어있는 것을 볼 수 있다.

→ 늘 ++을 하기는 너무 귀찮다. 그냥 Employee가 생성이 될 때 ++serialNum을 학번으로 주는 코드를 작성하는게 낫다.

+) static 변수는 어디에 있든, 프로그램이 로드될 때 이미 생성이 되어있다. 그러므로 호출할 때, 참조변수를 호출하지 말고 클래스 명으로 호출하는게 직관적이다. 뭐 오류가 발생하지는 않겠지만.

→ employeeLee.serialNum++ 이렇게 하지 말고, Employee.serialNum++ 이렇게 하는게 낫다는 소리이다.

+) 인스턴스 변수는 스태틱 메서드에서 사용할 수 없다. 

- **변수의 유효 범위와 메모리**

>지역변수(로컬 변수) : 함수 내부에 선언 / 함수 내부에서만 사용 / stack / 함수가 호출될 때 생성되고 끝나면 소멸
>
>멤버 변수(인스턴스 변수) : 클래스 멤버 변수로 선언 / 클래스 내부에서 사용하고 private이 아니면, 참조 변수로 다른 클래스에서 사용 / heap / 인스턴스가 생성될 때 힙에 생성되고, 가비지 컬랙터가 메모리를 수거할 때 소멸된다.
>
>스태틱 변수(클래스 변수) : 스태틱 예약어를 사용하여 클래스 내부에 선언 / 클래스 내부에서 사용하고 private이 아니면 클래스 이름으로 다른 클래스에서 사용 가능(global variable) / 데이터 영역 / 프로그램이 시작할 때 상수와 함께 데이터 영역에 생성되고 프로그램이 끝나고 메모리 해제할 때 소멸된다.
>
>static 변수는 메모리에 있는 동안 그 영역을 계속 차지하므로, 너무 큰 메모리는 할당하지 않는 것이 좋다. 또, 객체 이름을 통한 접근이 불가능하고, 클래스 이름을 통해 접근이 가능하다.
>
>클래스 내부의 여러 메서드에서 사용하는 변수는 멤버 변수로 선언하는 것이 좋다.
>
>멤버 변수가 너무 많으면 인스턴스 생성 시, 쓸데 없는 메모리가 할당된다.

**+) 가비지 발생시키기**
```
Person person = new Person();
person.setName("Mang");
person = null;*// 가비지 발생***

person = new Person();
person.setName("MangKyu");
```

- **싱글톤 패턴**

인스턴스는 new를 이용하면 생성된다. 인스턴스가 단 하나만 있어야 하는 것이 있다.

**ex) 학교, 웹 서비스의 커넥션이 존재하는 ‘풀’**

**1) School.java**
```
public class School {
  private static School instance = new School(); //2. 그래서 내부에서 만든다. 이 instance가 유일한 School 객체이다.
  private School() {} //1. 해당 클래스 내부에서만 School() constructor(생성자)를 생성할 수 있다.
  //해당 School 인스턴스를 밖에서 사용하기 위한 것이다.
  //인스턴스를 생성하지 않고, 메서드를 제공해야 하므로 static method로 선언한다.

  public static School getInstance() {
    if(instance ==null){
      instance = new School();
    }
    return instance;
  }
}
```
> **위 싱글톤 패턴 예시 설명**
> 
> 1. `private static School instance = new School();`: School 클래스 내에서 유일한 인스턴스를 가리키는 private 정적 변수 `instance`를 선언하고, 이를 바로 생성한다. 클래스가 로드될 때 School 인스턴스가 미리 생성되어 있다.
> 2. `private School() {}`: School 클래스의 생성자를 private으로 선언한다. 이것은 외부에서 직접 School 인스턴스를 생성하는 것을 막는다. 즉, 외부에서 `new School()`를 호출할 수 없다.
> 3. `public static School getInstance()`: 유일한 School 인스턴스에 접근하기 위한 public static 메서드이다. 이 메서드를 호출하면 내부적으로 유일한 인스턴스를 생성하거나 이미 생성된 인스턴스를 반환한다.
> 4. `if(instance == null) { instance = new School(); }`: getInstance() 메서드 내에서 School 인스턴스를 생성하는 부분이다. 처음 호출 시에만 인스턴스가 생성되고, 이미 생성된 경우에는 기존 인스턴스를 반환합니다. 이렇게 함으로써 항상 하나의 인스턴스만 존재하게 된다.
> 5. `return instance;`: 인스턴스를 반환하는 부분이다.
> 
> → 이렇게 구현된 싱글톤 패턴을 사용하면 어디서든지 School 클래스의 유일한 인스턴스에 접근할 수 있으며, 중복된 인스턴스의 생성을 방지할 수 있다.
> 

**2) SchoolTest.java**
```
public class SchoolTest {
  public static void main(String[] args) {
    School school1 = School.getInstance();
    School school2 = School.getInstance();
    System.out.println(school1 == school2);
    //true, 100번을 불러도 true이다.

    Calender calendar = new Calendar();
    //생성할 수 없다.
    Calender calender = Calender.getInstance();
    //이것도 싱글톤 패턴이다. 왜냐하면, 달력이 여러 개라면 문제가 되기 때문이다.
  }
}
```

- **배열**

1) ```int[] numbers = new int[] {10, 20, 30}; //개수 생략```

2) ```int[] numbers = {10, 20, 30}; //new int[] 생략 가능```

→ 선언과 동시에 값을 초기화하는 경우 new int[]를 생략할 수 있다.

3) 먼저 선언하고, 배열을 생성하는 경우
```
int [] ids;

ids = new int[] {10, 20, 30}; //선언 후, 배열을 생성한다면 new int[]를 생략할 수 없다.
```

**ex) 문자배열을 만들어 A-Z까지 배열에 저장하고 다시 출력하기**
```
char[] alphabets = new char[26];
char ch = ‘A’;
for(int i=0;i<alphabets.length;i++){
  alphabets[i] = ch++
}

for(char alpha : alphabets) {
  System.out.print(alpha + “  “);
}
```

- **객체 배열 사용하기**

기본 자료형 배열은 선언과 동시에 배열의 크기만큼 메모리가 할당되지만, 객체 배열의 경우, **요소가 되는 객체의 주소가 들어갈(4바이트, 8바이트) 메모리만 할당되고 각 요소 객체는 생성하여 저장해야 한다.**

(32bit 운영체제의 경우 4바이트, 64bit 운영체제의 경우 8바이트)

- **객체 배열 복사하기**
1. **얕은 복사**

→ 주소만 복사가 되는 경우

단순히 배열 변수 선언을 통한 복사 방법으로 볼 수 있다. 배열의 주솟값을 가져오는 것으로 보면 된다.
```
int[] A = {1, 2, 3, 4};
int[] B = A;

B[0]=999;

System.out.println(A[0]); //999가 출력된다.
```

2. **깊은 복사(1차원 : array.clone(), 2차원 : System.arraycopy())**

→ 깊은 복사는

**System.arraycopy(복사하고자 하는 소스, 어디서부터 읽어올지(첫 부분부터 읽고 싶다면 0을 넣는다), 복사할 소스, 복사본 자료 어디부터 쓸지, 원본에서 복사본까지 얼만큼 읽어올지 입력)**

즉, 라이브러리가 바뀐다고 카피라이브러리까지 바뀌는 것을 원치 않는 경우에는 ‘깊은 복사’를 사용해야 하는 것이다.


**ex) 깊은 복사**
```
package ch18;

public class ObjectCopyTest {

public static void main(String[] args) {

	Book[] library = new Book[5];
	Book[] copyLibrary = new Book[5];//copy할 배열을 생성해둔다.

	library[0] = new Book("태백산맥1", "조정래");
	library[1] = new Book("태백산맥2", "조정래");
	library[2] = new Book("태백산맥3", "조정래");
	library[3] = new Book("태백산맥4", "조정래");
	library[4] = new Book("태백산맥5", "조정래");

	for(int i= 0; i<library.length; i++) {

		copyLibrary[i] = new Book();
		copyLibrary[i].setAuthor(library[i].getAuthor());
		copyLibrary[i].setTitle(library[i].getTitle());
	}

	library[0].setAuthor("박완서");
	library[0].setTitle("나목");

	for(Book book : library) {
		book.showBookInfo(); //그대로 출력
	}

	System.out.println("==============");

	for(Book book : copyLibrary) {
		book.showBookInfo(); //박완서, 나목이 포함되어 출력
	}
}}
```

- **객체 배열을 구현한 클래스 ArrayList**

→ 객체 배열을 좀 더 효율적으로 관리하기 위해 자바에서 제공해주는 클래스

**import java.util.ArrayList;**

**import ch18.Book;**

**ArrayList<Book> list = new ArrayList<Book>();**

객체 타입을 <> 내부에 넣는 것이다. int 타입으로 선언하고 싶다면 <integer>을 넣으면 되는 것이다.


+) 객체를 new만을 이용해서 생성하지 않고, 메서드를 두고, 메서드 내부에서 객체가 생성하도록 만들 수도 있다.
