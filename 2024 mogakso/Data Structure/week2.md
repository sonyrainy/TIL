> 시간복잡도, 포인터, Sparse Matrix, Transpose Operation, Fast Matrix Transpose, Array(StringPatternMatching_KMP 알고리즘), queue, stack 등에 대해 복습하였습니다.
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
