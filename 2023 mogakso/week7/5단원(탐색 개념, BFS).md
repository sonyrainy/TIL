## 1. 너비 우선 탐색(BFS)
> **시간 복잡도 : O(V+E), V : 노드 수, E : 에지 수** 

큐의 특징인 FIFO를 활용하여 BFS를 구현한다.


### gif script)
>시작 노드에서 연결된 노드 중 방문되지 않은 노드를 방문하고 차례대로 큐에 삽입되는 식으로 진행된다.

아래 추가 설명 有

![](https://velog.velcdn.com/images/blueshj610/post/0115e90b-8f9d-4a80-94b9-1ca5b3cf1d8f/image.gif)


### ex_1) BFS 구현 설명(재귀함수 이용)
> **1. queue(FIFO)에서 하나의 노드를 꺼낸다.**
> 
> **2. 해당 노드에 연결된 노드 중 방문하지 않은 노드를 방문하고 차례대로 queue에 삽입한다.**

위의 1.과 2.를 반복하는 것으로 볼 수 있다.

![](https://velog.velcdn.com/images/blueshj610/post/d5af5a20-fd26-406e-bcb5-6a9577504543/image.png)
>- 1을 방문한다. 1이 방문처리되며 2, 3이 q에 들어온다.
q : [1] -> q : [2, 3]
>
>
>- 1의 주변 노드인 2, 3은 방문된 적 없으니까 큐에 들어왔고, 방문처리 되었다. 2가 q에서 나온 후, 3뒤에 4, 5가 대입된다(2와 3, 4, 5가 붙어있었으나, 3은 이미 방문처리되어 4, 5만 대입된다.).
q :[2, 3] -> q : [3, 4, 5]
>
>
>- 위 내용을 반복한다.
>q : [3, 4, 5] -> q: [4, 5, 6, 7]

큐에서 꺼낸 실행된 순서를 보면 [1, 2, 3, 4, 5, 6, 7] 이다.

즉, 해당 BFS 구현 코드는 시작 노드부터 가까운 노드들부터 탐색이 이루어지는 것을 파악할 수 있다.


```
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int number = 7;

// 방문 여부 체크하는 부분
int check[7];
vector<int> a[8];

void bfs(int start) {
	queue<int> q;
	q.push(start);
	check[start] = true;
	while (q.empty() == false) {
		// queue의 front에 있는 노드를 x에 대입
		int x = q.front();

		// queue의 front에 있던 노드를 삭제
		q.pop();

		cout << x << " ";
		for (int i = 0; i < a[x].size(); i++) {
			int y = a[x][i];
			if (check[y] == false){
				q.push(y);
				check[y] = true;
			}
		}
	}
}

int main(void) {

	a[1].push_back(2);
	a[2].push_back(1);

	a[1].push_back(3);
	a[3].push_back(1);


	a[2].push_back(3);
	a[3].push_back(2);

	a[2].push_back(4);
	a[4].push_back(2);

	a[2].push_back(5);
	a[5].push_back(2);

	a[3].push_back(6);
	a[6].push_back(3);

	a[3].push_back(7);
	a[7].push_back(3);

	a[4].push_back(5);
	a[5].push_back(4);

	a[6].push_back(7);
	a[7].push_back(6);

	bfs(1);
	return 0;
}
```
<br>

### ex_2) DFS와 BFS 프로그램([백준 1260](https://www.acmicpc.net/problem/1260))
```
#include <iostream>
#include <queue>
using namespace std;
#define MAX 1001

int N, M, V; //정점개수, 간선개수, 시작정점
vector<vector<int>> g(MAX, vector<int>(MAX, 0));//인접 행렬 그래프
//int g[MAX][MAX]; 
vector<bool> visit(MAX, false); //정점 방문 여부
queue<int> q;


void DFS(int v) {
    visit[v] = true;
    cout << v << " ";

    for (int i = 1; i <= N; i++) {
        if (g[v][i] == 1 && visit[i] == 0) { //현재 정점과 연결되어있고 방문되지 않았으면
            DFS(i);
        }
    }
}

void BFS(int v) {
    q.push(v);
    visit[v] = true;
    cout << v << " ";

    while (!q.empty()) {
        v = q.front();
        q.pop();

        for (int w = 1; w <= N; w++) {
            if (g[v][w] == 1 && visit[w] == 0) { //현재 정점과 연결되어있고 방문되지 않았으면
                q.push(w);
                visit[w] = true;
                cout << w << " ";
            }
        }
    }
}

int main() {
    cin >> N >> M >> V;

    for (int i = 0; i < M; i++) {
        int a, b;
        cin >> a >> b;
        g[a][b] = 1;
        g[b][a] = 1;
    }

    DFS(V);

    cout << '\n';
    fill(visit.begin(), visit.end(), false);


    BFS(V);

    return 0;
}

```

---
DFS, BFS 유형은 익숙하게 만들 필요가 있을 것 같다.

**+) BFS 개념설명 참고 : https://m.blog.naver.com/ndb796/221230944971**
