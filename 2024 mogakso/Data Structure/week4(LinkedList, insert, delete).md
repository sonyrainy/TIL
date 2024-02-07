- List Intro

아이템들이 나열되어 있고, 아이템들이 어디에 있는지를 가리키는 정보가 함께 있는 것을 Linked List라고 한다.

```
typedef struct listNode* listPointer
// 정의할 때, 포인터를 사용

typedef struct listNode {
char data[4];
listPointer link;
};
// 를 해서 list의 노드에 자기 자신에 대한 포인터(위치정보)를
// 같이 가지고 있도록 위와 같이 노드를 정의한다.
```

```listPointer``` 자체는 pointer이다. typedef 할 때, 이미 포인터 기호를 사용해서 node 내에서 pointer를 정의할 때에는 포인터(*) 기호를 넣을 필요는 없다고 볼 수 있다.

+) 공간 할당 + ...

```
listPointer first = NULL;
MALLOC(first, sizeof(*first));//메모리 공간 할당
strcpy(first->data, "BAT");
first->link=NULL;
```

위 코드에 대한 설명은 아래와 같다.
first가 가리키는 것은 list node으로 설정한다.
MALLOC에서 sizeof(*first)라는 것은 listPointer가 가리키고 있는 대상(list node)를 위한 메모리 공간을 할당해서 first가 그 할당된 공간의 주소값을 가지고 있게 된다.

이후에는 first의 data 부분에 "BAT"를 카피하고, 해당 부분 LINK에는 NULL을 넣어둔다.

아래 그림과 같다고 볼 수 있다.(+) link 공간은 1byte가 아니다. pointer는 int와 같이 4byte이다. 하지만 편의상 한 칸으로 표시하였다.)

![image](https://github.com/sonyrainy/TIL/assets/91364766/71274439-9adb-4931-a841-26434f1fb1a4)


- two nodes Linked List

첫 번째 노드에 대한 포인터만 알고 있으면, 그 다음 link의 link의 link를 따라가는 식으로 그 다음 data를 찾을 수 있다.

- List insertion

```
if(*first) {//기존 chain이 empty가 아니고 새로운 노드 추가
	temp->link = x->link;
	x->link = temp;
} else {
	temp ->link = NULL;
	*first - temp;
}
```

ex_1) 기존의 List가 있는 상황에서 새로운 노드를 추가

first는 10을 가리키고 있는 start를 가리킨다. 따라서 위 코드에서 ```if(*first)``` 조건에 걸릴 것이다.

temp는 insert 될 빈 공간(data, link가 할당된)이다.

>40 → 60 해당 노드 사이에 40 → 50 → 60 이 되도록 50 노드를 넣으려고 한다.

temp_data에 50을 넣어두고, temp_link에는 x_link 값을 넣는다(x_data는 40을 갖고, x_link는 60을 가리킴).

그런 뒤, x_link가 temp_data를 가리키도록 하면 된다.

```
void insert50 (listPointer *first, listPointer x) {
	listPointer temp;
	MALLOC(temp, sizeof(*temp));
	temp->data = 50;
	if(*first c) {
		temp- >link = x->link;
		x->link = temp;
	} else { /*...*/ }

}
```

![image](https://github.com/sonyrainy/TIL/assets/91364766/77492b98-23fc-4290-9f45-ba00ca881cb9)


ex_2) start를 위한 메모리는 할당되어 있지만 갖고 있는 값은 0인 경우, 어떤 노드도 가리키고 있지 않은 경우

```
else {
  temp -> link = NULL;
  *first = temp;
}
```

비어있으니까, temp_link는 가리킬 값이 없다. first가 가리키고 있는 start 부분에 50을 줘서 가장 앞에 50이 insert 되도록 한다.


<br>

- List delete

지운 노드는 시스템에 반납(free(x))까지 해준다고 생각하면 된다.

인자로 받는 *first는 정해진 List의 가장 앞을 가리킨다.

```
void delete(listPointer *first, listPointer trail, listPointer x){
		if(trail){ trail->link = x->link;}
		else { *first = (*first)->link;}
		free(x);
}

delete(&list, list, y);
delete(&list, NULL, list);
```

ex_1) 10 → 50 → 20 이 있을 때, 50을 지우려고 할 때,

받은 trail_link는 x_link가 가리키는 값을 가리키도록 한다. x가 delete 돼도 x가 가리킬 값을 받아 문제가 없도록 하기 위해서이다.

그리고 x를 반납(free(x))한다.

ex_2) 가장 앞의 노드를 지우려고 할 때,

first가 'first의 link가 가리키는 값'을 가리키도록 한다. 그리고 x는 반납(free(x))한다.











