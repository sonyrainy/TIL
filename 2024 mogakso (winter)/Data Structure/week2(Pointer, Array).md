> 시간복잡도, 포인터, Sparse Matrix, Transpose Operation, Fast Matrix Transpose, Array, StringPatternMatching(KMP 알고리즘), queue, stack 등에 대해 복습하였습니다.
---
- 성능분석
  - 공간복잡도 : 얼마나 많은 메모리를 차지하는가
  - 시간복잡도 : 얼마나 적은 시간을 소모하는가

<br>

- 인터프리터 언어 vs 컴파일 언어
  - 인터프리터 언어 : 소스 코드를 한 줄씩 번역/실행 동시에 진행한다.  Python, R, JavaScript 등.. 실행이 느리지만, 디버깅이 쉽고 운영체제 이식성이 좋다.
  - 컴파일 언어 : C, C++, Go… 컴파일이 오래 걸릴 수 있다. 컴파일이 다 된 프로그램이면 빠른 속도로 실행이 가능하다. 운영체제 이식성이 낮다.
 
<br>

- 시간복잡도 : run time + compile time ~= run time
step count(s/c) : 실행되는 부분

![image](https://github.com/sonyrainy/TIL/assets/91364766/ef76c235-140c-482e-bbb0-c038ed4bad65)

과하게 보면 위와 같은 방식이다.

<br>

- Array

![image](https://github.com/sonyrainy/TIL/assets/91364766/b50bd8b3-8007-4a53-bbf6-e9584fb4c125)

<br>

- 배열, 포인터 접근 방법
  - 배열과 포인터

```
list+2 == &list[2]
*(list+2) == list[2]

int* numPtr;과 int * numPtr;와 int *numPtr;가 다 같다.

즉,
list[1] ⇒ list의 0, 1 즉, 2번째가 ‘가리키는’ 값이 뭔가? (value)
&list[1] ⇒ list의 2번째가 ‘가리키는’ 값이 갖는 주소값은 뭔가? (주소)
*(list+2) ⇒ list의 3번째 값(주소)가 ‘가리키는’ 값이 뭔가? (value)
list + 2 ⇒ list의 3번째 값이 뭔가? (주소)
```

  - 포인터
```
포인터 변수는 주소값을 value로 갖는 변수이다.
따라서 초기화 할 때는 주소연산자 "&"가 붙은 변수를 통해 초기화할 수 있다.

int a = 1;
int* p = &a;

printf("%d", *p); //p의 값이 '가리키는' 값은 (value) 1이다.
```
  
  - 이중 포인터
```
int main()
{
    int* numPtr1;     // 단일 포인터 선언
    int** numPtr2;    // 이중 포인터 선언
    int num1 = 10;

    numPtr1 = &num1;    // num1의 메모리 주소 저장 

    numPtr2 = &numPtr1; // numPtr1의 메모리 주소 저장

    printf("%d\n", **numPtr2);//*numPtr2의 값이 가리키는 값, num1의 값(10, value)
    printf("%d\n", *numPtr2);//numPtr2의 값이 가리키는 값, numPtr1의 값(num1의 주소)
    printf("%d\n", numPtr2);//numPtr2의 값(할당 받은 주소값, numPtr1의 주소)
    printf("%d\n", numPtr1);//numPtr1의 값(할당 받은 주소값, num1의 주소)
    printf("%d\n", *numPtr1);//numPtr1의 값이 가리키는 값, num1의 값(10, value)

    return 0;
}
```

<br>

+) 유지보수 더 편하게 하려면
```
int i, n *list; //보다
int i; int n; int* list; //가 낫다.
```

<br>

+) 포인터 변수를 사용해 메모리를 동적으로 할당하기
```
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *dynamicVar; // 포인터 변수 선언

    // 메모리 동적 할당
    dynamicVar = (int *)malloc(sizeof(int));

    if (dynamicVar == NULL) {
        // 동적 할당 실패 처리
        fprintf(stderr, "메모리 할당 실패\n");
        return 1;
    }

    // 동적으로 할당된 메모리에 값 저장
    *dynamicVar = 42;

    // 사용 후 메모리 해제
    free(dynamicVar);

    return 0;
//동적으로 할당된 메모리는 프로그램의 실행 중에 사용이 끝나면 반드시 해제해야 한다.
//메모리를 해제하지 않으면 메모리 누수가 발생할 수 있다.
}
```

<br>

- Sparse Matrix(희소행렬 : 행렬의 값이 대부분 0인 경우)

그냥 표현한다면 많은 메모리 공간이 낭비된다. 따라서, 2차원 행렬로(row, col, value)를 열로 하여 표현한다.

가장 첫 값에 행, 열, 요소의 개수 값을 왜 넣을까? (약속) 첫 요소만을 보고, 행렬을 파악할 수 있도록 하기 위해서

![image](https://github.com/sonyrainy/TIL/assets/91364766/8ad39b6b-c2a7-40b1-9b36-82c68f2f0369)

<br>

- Transpose Operation(대각선을 기준으로 행→열, 열→행 변경)

그냥 원래 형태(2차원 표)에서 행과 열만 변경? 안된다. row(행)를 기준으로 순서대로 표현하는게 약속이기 때문이다.

> col 수만큼 +1 씩 반복적으로 scanning 하면서 정렬되도록 한다.

ex) col 값이 0인 것들을 원래 표에서 조사하여 행과 열을 swap한다. col 값이 1인 것들을 원래의 표에서 조사하여 swap한다... 를 반복한다.

이 경우, 시간복잡도가 O(행*열)로 매우 크다.

<br>

- Fast Matrix Transpose(디폴트가 row 값 기준으로 정렬)
위의 방법이 아닌, 여러 배열을 활용하여 transpose를 구현할 수도 있다. 중첩 for문을 줄여서 time complexity를 줄일 수 있다.

ex) rowTerms, startingPos를 활용하면 된다.

```
rowTerms[i]에는 본래 표의 col 값이 i인 값의 개수를 각각 적는다.
startingPos[i]에는 본래 표의 i번째 row 값에 따른 값이 몇개씩 있는지를 적는다.
(본래 표의 col 값이 바뀐 표의 row 값으로 변한다. 따라서, Transpose Matrix의 몇 번째 row에 들어갈지를 결정할 수 있다.)
```

![image](https://github.com/sonyrainy/TIL/assets/91364766/4bf10696-f678-4cd8-8f07-42dcb8f3e615)

```
일단 col의 값에 따라 transpose matrix에다가 본래 표에서의 row와 col가 swap된 형태로 startingPos 값에 맞는 index 값에 대입한다.
그리고는 해당 startingPos[i] 값은 ++한다.(이후 col값이 나오면 또 transpose matrix에 바로 대입하기 위함)
```

이런 식으로 진행하면, 시간복잡도는 O(columns + elements)가 된다.
