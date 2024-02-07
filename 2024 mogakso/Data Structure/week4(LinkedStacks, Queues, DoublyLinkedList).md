- linked stacks : stack을 구현할 때는 top 변수를 활용한다.

```
void push(int i, element item){
	stackPointer temp;
	MALLOC(temp, sizeof(*temp));
	temp->data = item;
	temp->link = top[i];
	top[i] = temp;
}
```

```
element pop(int i){
	stackPointer temp = top[i];

	element item;
	if(!temp) return stackEmpty();
	item = temp->data;
	top[i] = temp->link;
	free(temp);
	return item;
}
```

<br>

- linked queue : front와 rear 변수를 사용해서 가장 먼저 들어온, 그리고 가장 늦게 들어온 수를 가리키도록 한다.

```
void addq(int i, element item){
	queuePointer temp;
	MALLOC(temp, sizeof(*temp));
	temp->data=item;
	temp->link = NULL;
	if(front[i]) rear[i]->link = temp;
	else front[i] = temp;
	rear[i] = temp;
}
```

```
element deleteq (int i) {
	queuePointer temp = front[i];
	element item;
	if(!temp) return queueEmpty();
	item = temp->data;
	front[i] = temp->link;
	free(temp);
	retrun item;
}
```

<br>

- DoublyLinkedList : LinkedList의 정보를 양방향으로 훑어볼 수 있다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/6cf1785f-1ba4-4ff7-aed6-2890a9d3a442)

Llink, Rlink(item의 왼쪽, 오른쪽)도 활용한다. 아래는 표현 방법이다.

item의 Llink가 가리키는 값의 Rlink가 가리키는 값이 'item' 이다.
item의 Rlink가 가리키는 값의 Llink가 가리키는 값이 item이다.

해당 부분에서 insert와 delete는 아래와 같이 사용한다.

![image](https://github.com/sonyrainy/TIL/assets/91364766/f11d6a65-c7d4-4da2-9459-ba6344dd88b1)

![image](https://github.com/sonyrainy/TIL/assets/91364766/277fd985-6757-48b2-986d-a3b27abb4eca)



