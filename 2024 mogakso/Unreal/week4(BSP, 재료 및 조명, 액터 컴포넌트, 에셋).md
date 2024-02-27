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


