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

- queue

- stack
