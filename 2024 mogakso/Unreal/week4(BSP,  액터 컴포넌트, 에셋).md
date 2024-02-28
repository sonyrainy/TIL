### 지오메트리 브러쉬

- 창고 생성

```file - new level - basic``` 을 통해 새로운 레벨을 만든다. 바닥을 일단 지운다. 

그리고 박스를 생성한다. ```quickly add to the project - place actors panel - 박스 생성```

+) OutLiner가 사라졌다면? ```window - outliner```

창고를 생성하기 위해서 다른 박스를 생성 하고 크기를 정한다. 생성한 박스를 wallsSubstract로 이름 지어 생성한다. 제일 앞서 만들었던 박스 크기의 -200만큼 x, y, z 성분 다 뺀다.
그리고 brush type을 substractive로 설정한다.

그리고 원래 있던 박스의 내부로 들어가면 안이 비어있는 것을 확인할 수 있다.

해당 레벨을 시작하자마자 열리는 메인 레벨로 설정하려면, ```settings - project settings- maps&modes startup map과 default map을 main으로 해둔다.```

<br>

- 위의 창고를 만든 방식으로 창문을 만들 수 있다.

브러쉬로 박스를 만들고 substractive로 해두고, 하나를 창문을 만들 수 있다. 그리고, alt를 누른 채로 이동시키면 하나 더 생성된다. 그렇게 한 쪽 벽에 여러 창문을 만들 수 있다.
그리고 해당 창문 그룹을 다른 벽에 똑같이 복사할 수 있다. 전체선택(shift) + alt + 이동

<br>

### 액터(레벨에 배치할 수 있는 오브젝트) 컴포넌트
기둥만 있는 선발 틀에 선반바닥을 놓으려고 한다. 선반의 기둥 부분을 세워두고, 선반의 바닥 부분을 detail에서 기둥 부분의 자식으로 바닥 부분을 두면서, 일체적으로 표현할 수 있다.

자식의 transform 위치는 부모에서 상대적으로 표현된다. 부모를 옮길 때 자식도 같이 움직이게 된다.(rotate, scale도 모두 마찬가지)

자식과 부모 모두의 공통 특징을 조작하고자 하면 details에서 루트가 되는 부분을 클릭하여 조절하면 된다.

여기에서는 선반의 바닥 부분은 움직이지 않게 하기 위해서(일체형 선반 액터를 생성), root 부분에는 simulate physics를 적용하고, 선반 부분(자식 부분)에는 simulate physics를 해제한다.
