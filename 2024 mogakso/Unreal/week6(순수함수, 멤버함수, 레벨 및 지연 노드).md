### 리턴타입
- 이미 존재하는 기능을 함수로 추출할 수도 있었고, 아예 새로운 함수를 만드려고 하면 어떻게 해야할까?
My Blueprint 탭에서

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/17276e04-ffe7-499f-a04c-946d912b7346" width="150" />

사진과 같이 + 버튼을 눌러서 함수를 생성할 수 있다. 생성한 함수를 원래의 블루프린트 탭에서 드래그해서 들고오면 된다.

우리의 함수에 input/output을 설정하려면 생성할 함수 탭의 Details 탭에서 Input, Output을 설정한다(아래 사진 참고).

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/caf8bba8-a39b-45a1-ad77-23b7b51f840f" width="750" />

<br>

- Ammo, Greater 노드를 묶어 Has Ammo 함수를 만든다. Ammo의 개수를 파악하고, 조건에 맞다면 return 값으로 True, 아니면 False를 내뱉는다. Input 값은 없다(아래 사진 참고)

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/9e218aae-5a60-491c-8454-a10723f318b5" width="850" />

---

### 사이드 이펙트 함수, 순수 함수
- 사이드 이펙트 : 함수가 실행되고 식별 가능한 이펙트(효과)가 생기는 것이다.

ex) 사이드 이펙트 함수

>print String : 문자열을 출력하고, 컴퓨터 내부에서 무언가가 발생한다. 그 후 화면에 문자열이 보인다.
>add Impulse : 충격을 가한 물체가 멀리 날라간다.
>Set Ammo : Set ammo 후에는 변수의 설정 값이 바뀐다.

<br>

- 그럼 거의 모든 함수가 식별 가능함수가 아닌가?

<br>

- 순수함수 : 사이드 이펙트가 없는 함수. 하지만 return 값은 있다. 순수함수의 목적은 계산하고 값을 돌려주는 것 뿐이다.

ex) 순수함수

>get ammo : 계속해서 탄약 값을 얻어도 게임(게임 내부)에서는 아무 일도 일어나지 않는다.
>Get Actor forward vector : 여러 번 얻어도 괜찮다. 변환된 값으로 뭔가를 하기 전까지는 아무것도 바뀌지 않는다.
>multiply, minus greater같은 수학 함수도 프로젝트에 영향을 주지 않는다.
>
> 순수함수는 실행핀(노드 간 데이터 흐름을 제어한다. 노드 간 실행 순서 결정을 위해 사용한다.)이 없는 함수를 말한다.

+) 만든 함수의 details 탭에서 pure을 체크표시하면 실행핀이 사라지는 것을 확인할 수 있다. 이 함수의 입/출력 핀만 남게 된다.
즉, 그렇게 생성된 노드의 output핀을 Print String과 연결하면 문자열 출력 전에 함수를 실행한다.

사이드 이펙트가 없어, 함수의 호출이 다른 작업에 영향을 미치지 않고, 안정적이다.

>has ammo 같이 간단한 값을 계산할 때 사용하는 것이 당연하다고 볼 수 있다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/0052a0e7-4167-4429-89ce-c203f07f4515" width="450" />

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/7005e9fe-9e41-4776-8040-5c6f098ef985" width="450" />


두 사진 중 아래 부분을 보면 has Ammo의 이전 실행 흐름이 사라졌다. has Ammo는 바로 분기문으로 갈 수 있다. 분기문이 실행되자마자 Has Ammo가 실행되고, 그 반환 값을 분기문이 받아올 것이다.

<br>

- 정리
>사이드 이펙트 : 함수에서 눈에 보이는 효과
>순수 함수 : 사이드 이펙트가 없는 함수. 무언가를 가져오는 함수나 질문에 대답하는 함수.

---

### 멤버함수
레벨 블루 프린트가 아닌, 특정 블루프린트 클래스에 있는 함수를 멤버함수라고 한다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/5121c8eb-6658-41c1-b097-a616f37bdc07" width="650" />

 
ex) BP_Projectile 인스턴스를 사용한다. 즉, 이 코드를 BP_Projectile를 인스턴스로 쓰는 한 어떤 곳으로 옮기면 좋지 않을까?

<br>

- 특정 인스턴스에 어떻게 함수를 만들까? BP_Projectile 클래스를 content drawer을 통해 열고 Open full blueprint editor을 연다.

거기에서 NewFunction을 생성하면 된다. 이는 멤버함수이다. 해당 오브젝트를 더블클릭하면 있던, 만들어둔 멤버함수를 볼 수 있고, 새로 생성도 할 수 있다. 그 오브젝트의 특징과 그것이 가지고 있는 함수이다.

암묵적으로 모든 멤버 함수는 현재 타겟이나 현재 인스턴스라는 파라미터를 가지고 있다. 이 파라미터로 함수가 호출된 클래스의 인스턴스를 참조할 수 있으며, 인스턴스에 대한 작업을 수행할 수 있다.

+) 블루프린트에서 self를 검색하여 get a reference to self 노드를 만들면 이것을 통해 객체의 속성을 알수 있다. BP Projectile의 이름을 알고 싶으면 self에서 끌고 나와서 get display name을 연결하고 거기서 Print String을 연결하면 된다.

그렇게 연결하고 play를 눌러 Spacebar를 눌러 공을 발사하면 계속 다른 문자열이 출력된다. 새로 생성된 발사체의 이름이 모두 다르다. 이는 self가 다른 발사체에서는 다른 self이기 때문이다(멤버함수에 의해 참조되는 self가).

+) static mesh component 는 해당 오브젝트의 시각적인 모습을 결정한다. Launch 함수는 BP_Projectile의 이름을 출력하고, 그 정보를 담고 있으며, add impulse를 해준다.
Launch 함수를 생성할 때, 스폰된 BP_Projectile을 인풋으로 받으니까 현재 인스턴스 파라미터는 그 스폰된 BP_Projectile이다. 근데 안되어 있었다. 따라서, 새 Launch의 static mesh component - add impulse를 연결할 때 발생하는 오류는 static mesh component 노드의 input 부분에 self 노드를 생성하여 해결할 수 있는 것이다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/5a8e1a76-a8d0-44b2-9134-b8e594e81fc4" width="650" />

---

### 레벨노드와 지연노드
발사체를 다 사용하면 5초 뒤 다시 시작하도록 만드려고 한다. delay는 함수 끝나고 바로 아웃풋 나오는게 아니라 좀 이따가 실행되도록 한다.

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/769d6b30-0a41-4bf6-ac32-782455ca6d21" width="450" />

get current level name과 open level은 다 끝나면 5초 뒤에 현재 레벨을 보여주고 다시 시작하는 것이다.

변수를 전환하는 노드까지 포함하여 3가지 노드를 묶어 Restart Level 노드를 생성하여 최종본을 완성했다(위 사진 참고).

---

### 최종 블루프린트
 <p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/24433f6f-e54f-4d86-8a7f-a532784f9e8a" width="750" />

