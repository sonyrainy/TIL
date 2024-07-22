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


---

### 액터 스폰하기

space bar를 누르면 새 발사체에 Impulse를 추가하여 해당 씬과 게임을 역동적으로 만들 수 있다.

+) 게임에서 총을 쏠 때 나오는 발사체를 스폰이라고 한다.

+) 블루프린트에서 노드 간 선을 제거하려면 alt 누르고 마우스로 클릭하면 된다.

<br>

- spacebar Pressed - Spawn Actor Node

spacebar를 누르면 생성되게 하기 위해서이다. 생성된 Spawn Actor Node에서 지정할 클래스를 BP_Projectile로 설정해둔다.
<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/01bd1748-37d2-429e-ac0f-7f7bafd9ecc5" width="350" />

그리고, BP_Projectile의 Transfrom에서 위치를 Spawn Transform Location과 동일하게 주고 play를 누르면 어떻게 될까?

>게임이 시작되며 Projectile을 여러 개 생성한다면 게임 내에서 만들어진 Projectile 위에 새로운 Projectiile이 생성된다.

<br>

- 스폰들에 임펄스 추가
임펄스를 추가하려는 대상은 Static Mesh이다.

>새 발사체를 만들고, Static Mesh Component를 가져오고, Impulse를 추가하는 식으로 진행하면 된다.
>
>그리고 실행핀은 add impulse에 연결한다.
>
>Spawn Actor의 return 값을 통해 입력받은 StaticMeshComponent 값은 add impulse에서 변수로 사용된다.
>
>Spawn되고 StaticMeshComponent(시각적인 모습 결정)을 지나 Impulse가 추가되도록 하는 구조이다.

---

### 데이터구조
- Object : 데이터와 기능의 집합
- Struct(구조체) : 많은 구조체가 오브젝트와 동일하지만, 보통 상당히 작은 것을 위주로 말한다. 레퍼런스를 사용하지 않는다. 너무 작아서 바로 메모리로 전달하고 복사한다.
- Actor : ex) Cube, BP_Projectile
- Component : ex) StaticMeshComponent

---

### Pawn과 Actor의 위치
- 발사체가 내가 보고 있는 곳에서 발사되도록 하기 위해서는 "배출"이라는 기술을 사용한다.
>play 한 상태에서 f8을 눌러 어떤 오브젝트가 빠져나가는 것을 볼 수 있다.

해당 상태가 되면 게임 플레이 중에 돌아다니고, Object를 선택할 수 있게 된다. 생성한 Object는 'Pawn'이라고 한다. 폰은 게임 월드에서 플레이어의 물리적 묘사를 나타낸다.

+) 빨간 버튼을 누르거나 esc를 눌러 게임을 정지 한 후, pawn을 검색해보면 pawn은 없는 것을 확인할 수 있다.

기본적으로 사용자를 위해 Scene 내에 폰을 스폰하고 details - player Start의 Scene 안(플레이를 시작해야 폰이 스폰된다.)의 액터가 주어진 위치에 배치되는 것을 알 수 있다.

이 때, Outliner에서 player Start를 검색하면 캡슐과 비슷하고 컨트롤러/깃발 아이콘이 있는 오브젝트를 확인할 수 있다.

<br>

- 기본 블루프린트의 레벨 블루프린트에서 폰을 찾아볼 수는 없을까?

우선 큐브의 레퍼런스가 있는 것처럼 폰의 레퍼런스는 참조할 수 없다(폰은 플레이를 해야 스폰되므로).

블루프린트 창에서 get player pawn을 가져와보자. 해당 노드에는 실행핀이 없다. 입력핀(플레이어 인덱스를 받음.), 출력핀(플레이어의 폰을 반환함.)만 존재한다.

>마우스를 입력 데이터 핀에 호버해보면 Integer이 뜬다. 이는 정수를 찾는다는 뜻이다. 이는 플레이어 컨트롤러 목록의 index이다(Player의 index 값).
>
>로컬 플레이어로 시작하여, 사용 가능한 원격 플레이어로 넘어간다는 설명이 표시된다. 이 설명은 일반적으로 "플레이어 컨트롤러에 의해 제어되는 액터를 반환하는 것"으로 볼 수 있다.
>멀티 플레이 게임에서 각 플레이어에 대한 인덱스 값을 지정해 해당 플레이어의 폰을 가져올 수 있다. 

+) 이번 게임에서의 index = 0은 첫 번째이자 유일한 player라고 보면 된다.

출력 부분은 Pawn Object Reference가 출력된다. 이것으로 Pawn의 위치를 찾을 수 있다. get actor location을 검색하여 입력을 Pawn Object Reference로 이어 받으면 된다.

이 때 해당 노드의 return value는 vector가 된다. 그 vector 값으로 BP_Projectile의 발사에 사용하여 위치, 형태를 볼 수 있다(아래 사진 참고).


<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/7976ee8e-33e9-47ea-9749-7d53b19ca227" width="850" />

<br>

- 공이 약간 가볍게 느껴진다면?
>1) content drawer - BP_Projectile ViewPort - Open Full blueprint Editor - Static Mesh Component - 질량 수정
>
>2) Simulate Physics을 체크한다.

위 내용까지는 공이 앞으로만 발사하는 문제가 발생한다.

---

### 회전 다루기
>블루프린트에서 Get Player Pawn에서 Get Actor Rotation을 생성한다.
>
>get Actor Rotation의 return value에서 Spawn Actor BP_Projectile - Spawn Transform Rotation으로 노드를 연결한다.
>
>그리고 BP_Projectile tab에서 static Mesh Component - transform scale의 x를 2로 변경한다. 그렇게 되면 공이 눌린 모습을 확인할 수 있다.


<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/a1759803-23f3-402f-88c5-7c84f411a33c" width="700" />

<br>

- 공이 카메라 방향에 따라 발사되지 않는다면, 플레이를 누르고 f8로 가서 rotation을 확인해볼 수 있다. 이 때 rotation이 180도 밖에 되질 않는다. -> 언리얼의 pawn이 카메라 회전과 함께 회전하도록 설정되지 않았기 때문이다.

위 '+) 내용'을 연결하려면 control rotation을 이용한다.

>1) Player Controller의 설정을 확인한다.
>2) Control Rotation을 사용(적용)해 Pawn의 회전을 업데이트한다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/5f4ec4d0-6daa-4eff-91c0-6c893ea643c1" width="700" />

---

### forward vector(전방벡터) 가져오기

forward vector(전방 벡터)는 회전한 x방향이다. 회전한 다음 전방을 가리키는 벡터라는 뜻이다.

<br>

- 대포알의 전방 벡터를 조정하여 대포알의 속도 등을 조절하고자 한다면 액터 노드에서 끌고와서 참조해볼 수 있다.

>SpawnActor BP_Projectile의 return value에서 get actor forward vector를 생성한다. 그리고 get actor forward vector node의 return value를 add impulse의 impulse에 연결한다.

이 후 플레이를 누르고 대포알을 발사해보면, 바로 수직으로 떨어진다. get actor forward vector로 생성된 벡터는 단위벡터라서, 특별히 지정해두지 않으면 초당 1cm 이동한다(언리얼은 단위를 cm로 둔다.). 즉, x축으로 1 단위만 떨어진 벡터를 지닌 대포알이 생성될 것이다.

따라서 get actor forward vector 노드를 이용해서 vector에 부동소수점 값을 곱하여 대포알 속도, 발사 강도를 조절할 수 있다. 해당 노드의 return을 끌어서 muliply 라는 operator 노드를 이용한다. multiply node에서 우클릭해서 float 형(부동소수점을 사용하여 여러 물리 시뮬레이션 등 다양한 작업을 수행하기 편하기 위해서)으로 바꾼다.

그리고 multiply node에서 길이가 400 unit인 벡터가 가리키는 방향은 BP_Projectile이 회전하는 방향의 전방으로 볼 수 있다(카메라의 방향).

---


### assets 가져오기
>1) 에픽게임즈 런처 - 마켓플레이스에서 다운 받고 라이브러리- 보관함에서 프로젝트 추가
>
>2) content drawer - content - 다운받은 에셋

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/5b61d3c7-d611-4f76-b6c5-28f85f696a44" width="700" />

이제 원래 minimal default(원래 진행하던 프로젝트)로 가서, meshes 폴더로 가면 팩에서 나온 모든 에셋을 보고 적용할 수 있다.


