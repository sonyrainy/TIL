- StringPatternMatching : String 내부에 찾고자 하는 패턴이 있는지 찾는다.
  - 브루트포스_(O(M*N)) : 그냥 다 조사한다. 주어진 String을 i = 0 ~ N(String Size), j = 0 ~ M(SubString Size) 하나하나 조사한다.
  - KMP 알고리즘_(O(N)) : String과 SubString 사이 완전 같지는 않지만 겹치는 것이 있으면, 해당 부분을 활용하여 효율적으로 조사한다.
> 접두사와 접미사가 같은 특징적인 문자열을 활용하여 빠르게 조사한다.
>
> 이 때 활용하는 것이 failure function이다. failure function은 접미사와 접두사가 얼마나 겹치느냐에 따라
> 배열형식으로 값을 부여한다. (1) 자기 자신과 겹치는 건 제외한다. 2) 접두사, 접미사가 절반을 넘어가도 된다.)

(failure function(검색하면 잘 나와있음)을 이해하고, '미스매치된 str의 위치와, 미스매치된 substr의 해당 index - 1이 가리키는 값(반복패턴의 정보를 읽는 것)을 맞추고 재탐색을 진행하도록 하는 것'을 활용하면 KMP 알고리즘을 구현할 수 있다.)


![image](https://github.com/sonyrainy/TIL/assets/91364766/6dd1a3e3-9ba9-4085-ad1c-8b2662eb6f30)

---

>'가장 위(최근)에 들어온 데이터의 위치를 가리키게 하는 변수로 작동되도록 하기 위해서는 stack'을, '먼저 온 데이터가 먼저 나가고 나중에 들어온 데이터가 나중에 나가야 하도록 하기 위해서는 queue'를 사용하여 관리한다.

<br>

- queue(FIFO) : front, rear를 활용한다. 먼저 오는 것이 front로 오고 먼저 서비스를 받는다.
  - addQ : queue의 가장 뒤에 요소를 추가한다. rear++ 한다.
  - deleteQ : queue의 가장 앞에 있는 요소를 삭제한다. 이 후 front++ 한다.

이 때, queue의 앞부분에 공간이 있지만, 뒷 부분은 가득 찬 경우, addQ를 통해 요소를 추가할 수 있을까? 할 수가 없다.

따라서 순환되도록 circular queue 형태로 진행하기도 한다. 다 찼으면 가장 앞으로 다음에 들어올 값을 보내는 형태이다.

- circular queue : 생성하면 front = 0, rear = 0인 상태
  - addQ : 처음에 add하면, front = 0 값은 그대로 두고, rear 값은 + 1 증가하며 rear 값을 index로 갖는 queue의 위치에 값을 대입한다. queue의 index = 0인 부분을 비워두는 이유는 circular의 성질을 활용하기 위함이다.
  - deleteQ : delete하면, ++front 한다. 그리고 해당 index를 갖는 값을 제거한다.
  
rear == front가 되면 error라고 본다.(queue is full)

![image](https://github.com/sonyrainy/TIL/assets/91364766/e40ebe89-9ed6-481c-9366-69ab690f44e4)

<br>

- stack(FILO) : 가장 위에서 삭제와 추가가 이루어진다.
연속적으로 stack에 값을 추가할 때, top 부분이 0, 1, 2, ... 이렇게 올라가야 할 것이다. 코드를 간단하게 짜기 위해 top = -1로 초기화하여 작성하는게 일반적이다.
