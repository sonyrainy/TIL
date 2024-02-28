### 재료와 조명

새로운 레벨로 이동된 상태에서는 이전 레벨에서 가지고 있던 기능이 없다. 플레이에서 스페이스를 누르면 BP_Projectile이 올라가기만 하고, 발사되지는 않는다.

- 이 때 이전 레벨의 기능을 쉽게 복사할 수 있는데, content drawer에서 maps 폴더로 들어가 minimal_default(이전레벨)을 열기만 하면된다. 그리고 해당 맵에서 블루프린트를 열고, 모든 노드를 선택하여 복사하고 (content drawer에서 원래 레벨을 다시 선택한 후, content-main) 붙여넣기를 하면 된다.

<br>

- 아무 material이 적용되지 않은 상태에서, 바닥과 천장, 벽 등에 재질을 주려고 한다. content drawer에서 all - content - material을 검색하면 여러 재질이 나온다. 벽에 원하는 재질을 드래그하여 사용할 수 있다.

<br>

- 조명도 수정할 수 있다. outliner에서 light를 조절가능하다. skyligh은 전방향 조명을 나타낸다. light source를 거기서 클릭하고 조절할 수 있다. 태양광의 방향을 조절할 수도 있다.

<br>

---

### 충돌 메시

- 언리얼에서 물품 여러 개의 원통을 쌓아두고, 물리 적용을 체크하면, 푱하고 튀기도 한다. 이런 경우, 메시가 불안정한 경우로 볼 수 있다.

이런 결과가 나오는 이유는 언리얼에서 충돌을 계산하는 방식 때문이다. 

Lit으로 되어있는 좌측상단 화면 보기 부분을 WireFrame 으로 하여 컴퓨터가 보는 메시 화면을 볼 수 있다. 적용된 화면은 아래와 같다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/791219f4-8452-4e82-8886-d64abc578b19" width="550" />


컴퓨터는 해당 화면에서 material을 적용하여 우리에게 보여준다.

이 원통에 존재하는 복잡한 메시가 물리학이 적용되는 것은 아니다. 물리적 계산을 쉽게 하기 위해 더 간단한 메시를 사용한다.
wireframe을 player collision으로 적용하면, 물리학 계산이 적용된 간단한 메시를 볼 수 있다. 적용된 화면은 아래와 같다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/38655107-af70-4024-8708-8b1edede4cc6" width="350" />

충돌 메시는 언리얼에서 쉽게 수정이 가능하다.

Content Drawer에서 collision - remove collision 하면 player collision 화면에서 메시를 확인할 수 없는 것을 볼 수 있다.

이 때, play 를 누르면 remove collision 된 원통이 그냥 바닥을 통과하는 것을 확인해볼 수 있다.

Add 10DOP-Z simplified collision을 클릭하면, 4개의 z축 정렬 모서리가 기울어진 새로운 상자 충돌 메시를 생성하는 것을 확인해볼 수 있다.

적용된 화면은 아래와 같다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/d4153ffa-9681-4813-8cfe-2f7a618f76f7" width="350" />

그럼 그것을 적용한 배럴에는 간단하게 바닥이 처리되어, 안정적인 물리학이 적용되게 된다.

<br>

- 블루 프린트 배럴 클래스를 만들어서, 매번 배럴을 만들 때마다 설정을 변경하지 않아도 되게 하고자 하면 어떻게 해야할까?

설정 변경한 배럴을 선택하고 details tab에서 블루프린트 모양을 누른다. 그리고 경로는 루트 폴더를 더블클릭해 지정하여 선택해본다.
그리고 Content Drawer에서 제작해둔 폴더로 가서 드래그하여 꺼낸다.

OutLiner에서 생성된 BP_Barrel에다가 move to - create new folder - BarrelWall 으로 이름 짓는다(배럴의 묶음으로 벽을 만들건데, 그 배럴들을 묶어두기).

+) 복사할 때 outliner로 다 클릭해서 이동시키면 빠르게 복사 붙여넣기가 가능하다.

+) 공이 벽을 뚫고 지나가는 경우도 있는데, 이는 공이 너무 빨라서 물리학 시뮬레이션이 따라잡지 못하는 경우이다.

---

### get, set (변수)

- 탄약 개수를 변수를 통해 나타내려고 한다. 블루프린트에서 window - myblueprint로 들어간다. variables section에서 변수 생성이 가능하다.

생성 후, 좌측상단 compile 버튼을 눌러서 default value를 지정할 수 있다. 20개의 탄약으로 시작하고자 한다면, default value에 20을 입력한다.

게임을 하면서 그 값을 업데이트 하고자 하면 변수를 블루프린트 그래프에 드래그 한다.

>get 변수는 저장된 값을 가져오는 것이다.
>
>set 변수는 그 안에 있는 값을 덮어쓴다는 것이다. 즉, 새로운 값을 설정한다. 그렇게 변수를 변경되고, get 변수를 호출하여 변경된 값을 가져온다.

+) 변수를 컨트롤을 누른채로 드래그하면 get, alt를 누른채로하면 set의 노드가 생성된다.

언제 set 변수를 덮어쓸지 알려주는 실행핀이 필요한데, begin play에서 변수 값을 가지고 올 수 있다.

begin play와 PrintString 노드를 새로 연결하고, get 변수 노드와 그 String을 연결하면 시작하고 20(20발 지닌채로 시작)이 출력된다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/efef0a47-37da-45eb-970a-f6e3cc22b622" width="350" />

 
>```get 변수 노드와 substract 노드(-1이 되도록 지정)와 set 노드를 연결```한다. 그리고 ```Add Impulse를 이전의 세 노드가 연결된 set 변수 노드에 연결하고, print string 노드에 연결하면 대포알을 사용할 때마다 1씩 줄어드는 값이 출력```되는 것을 볼 수 있다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/dd1caab4-5f9c-4767-97ab-5f997a38b94d" width=750" />

---

### Booleans and branches

- branch는 무언가가 true인지, not(bool)인지 볼 수 있도록 한다. 그리고 결과에 따라 무엇인가를 하게한다. 

```space bar - spawn a projectile``` 되던 것을 뜯어서 ```spacebar - branch```에 연결하고, branch가 true일 때 Projectile이 출력되도록 한다.

false라면 공이 나오지 않고, out of ammo가 출력되도록 한다.

---

### 함수
엉망인 블루프린트 이벤트 그래프에서 어떤 일이 발생하는지 만든다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/eb2de660-ea1b-4c3f-aca8-8fd1c73414b4" width=1050" />

너무 더럽다.

우선, 발사체를 위한 노드들을 c키를 눌러서 블록으로 묶는다. 그리고 해당 부분을 Spawn Projectile로 명명하여 묶을 수 있다.

- 그렇지만 함수라는 더 좋은 도구가 있다. 사실 거의 대부분의 노드가 함수라고 볼 수 있다.
아무튼 묶을 것들 묶어서 함수로 만들 수가 있다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/d6a5951f-0a0e-4784-a546-b6a7e53e7e84" width=950" />


 
