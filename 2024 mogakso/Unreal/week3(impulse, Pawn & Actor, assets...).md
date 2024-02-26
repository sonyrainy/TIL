### Object & Reference
- 현재 map이나 level 뒤의 블루프린트를 보기 위해서는 상단 여러 개의 상자가 선으로 연결된 툴바(Open level BluePrint)를 이용한다. 해당 화면에서 우클릭을 통해 여러 기능을 활용할 수 있다.

+) Blueprint에서 우측 상단의 play 버튼으로 노드가 실행(ex) Print String이 실행되도록 하여 플레이 화면에 문자가 출력되도록 하기)의 실행되는 것을 확인할 수 있다.

```
Print String 노드 2개를 생성하고,
Welcome to Warehouse Wreckage ➝ Get Ready to Rumble! 를 연결해두면,
앞에 있던 메시지가 먼저 출력되고, 이후 메시지가 출력되는데
pc가 너무 빠르기 때문에, 동시에 출력되는 것처럼 보인다.
```

- "reference"는 오브젝트를 찾는 위치이다.

- create reference to a cube하면 Cube에 대한 새 노드를 생성할 수 있다.

+) static mesh component는 해당 오브젝트의 시각적인 모습을 결정한다.

- data pin(ex) create reference to a cube)

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/d9e4f9a1-e986-4f72-8716-27d815d8f89b" width="150" />


>위 사진의 파란색 원 부분이다. 다른 색으로 보이는 경우도 있다. 노드의 '데이터 입력/출력' 부분으로 볼 수 있다. 노드의 왼쪽에 있으면 입력, 오른쪽에 있으면 출력(노드가 만드는 데이터)이다.
>노드가 다룰 수 있는 데이터라는 것이다. 위 노드는 큐브 액터의 레퍼런스를 만든다.

create reference to a Cube 노드의 출력부분을 Static Mesh Component 노드와 연결하면 Cube로부터 생성된 노드(Static Mesh Component)의 입력은 'Cube Reference'이고, 출력은 Sstatic Mesh Component의 reference이다. 해당 노드의 출력 부분에서 드래그하면 Static Mesh Component의 기능을 요청할 수 있다.

+) get display name : Print String Node를 사용해 프린트할 수 있는 String이나 Test 값을 반환한다.)

- execution Pins
>데이터 핀과 구분하여 흰색 핀을 부르는 이름이다. 노드를 언제 실행할지를 결정한다.

정리해보면, data pin은 노드로 무엇을 실행할지 정하고, execution pin은 언제 실행할지를 결정한다.

+) Cube의 Reference Pin을 드래그하여 Cube의 모든 기능을 사용할 수 있다(아래 사진 참고).

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/b7cab59e-a9fe-45b8-9915-18e5b5197fe0" width="450" />

- StaticMesh
>형태가 있는 구조물이다. 의자, 벽, 사람 등도 StaticMesh인데 예를 들어 의자에 색이 들어가 있는 이유는 의자라는 StaticMesh에 material(재질)이 들어가있기 때문이다.

+) get static mesh component를 사용해보자. 입력은 Cube reference로 한다.
>**해당 노드의 output 부분에서 드래그하여 기능 요청이 가능하다.**
>
>**ex) get display name의 입력 부분에 Cube에 연결된 Static Mesh Component의 Reference를 연결할 수 있다. 그리고 get display name 노드의 return 부분을 Print String에 연결한다. 그렇게 play하면, Cube.StaticMeshComponent()가 뜨고, "get ready to rumble", "Welcome to ... " 메시지가 화면에 출력되는 것을 알 수 있다.**


---

### add impulse
- Spacebar를 눌러 큐브가 튀어오르도록 하고자 한다.

ex) 우선 spacebar 눌렀을 때 문자열 출력되도록 하기
>1. bluePrint에서 space bar를 생성한다.
>2. space bar node의 pressed를 Print String(게임 시작됐을 때 문자열이 출력되도록 해두었던 노드)과 연결한다. 그럼 이전에 연결해두었던 것을 토대로 연결되었으므로, 게임 시작 시 출력되던 문자열이 출력된다.

위 내용을 바탕으로 Cube - Static Mesh Component - Add Impulse에서 값을 조절하여 큐브가 뛰도록 할 수 있다.

+) Add Impulse에서 Vel Change를 체크 표시해두면, 질량과 관계없이 속력을 적용한다. 아래 사진에서는 z 방향으로 400m/s의 속력을 받게 되는 것이다.
<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/e8d024d9-2fa3-4c67-b5d1-f9a6c4459150" width="450" />

---

### BluePrint Class & Instance
ex) 모험가 Class를 통해(기본 데이터와 일부 기능) 모험가 1과 같이 클래스의 인스턴스를 만들 수 있다. 해당 인스턴스는 고유한 데이터 사본을 갖고 있다고 볼 수 있다. 다른 오브젝트간 모든 기능이 공유된다.

구를 생성하고 이를 단일 오브젝트에서 여러 오브젝트의 블루프린트 클래스로 변경하고자 한다면, details 패널에서 BluePrint 버튼을 클릭한다.

+) 규칙: 블루프린트 클래스를 생성할 때는 접두어 BP_...를 작성한다.

블루프린트 클래스 자체의 새로운 에디터가 열리게 된다. 새로운 에디터 창에서 오브젝트 인스턴스를 만들 때, 해당 블루프린트 클래스가 어떻게 보일지를 미리 확인 가능하다.

Content Drawer - content - 생성한 Map 파일에서 위 설명 부분에서 생성한 발사체 블루프린트를 확인할 수 있다. 이를 씬으로 드래그하면 새 인스턴스가 생성된다. BP_Projectile editor에서 property를 변경하면 모든 인스턴스에 대한 해당 속성이 변경된다.


