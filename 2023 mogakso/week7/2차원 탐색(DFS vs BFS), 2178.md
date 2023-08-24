백준 2차원 탐색 DFS 문제를 풀어보다가 시간초과가 발생한 김(BFS로 접근하는 문제였다.)에 해당 문제에서 DFS, BFS 접근방식을 정리해보려고 한다.

---

푼 문제와 정답 코드는 해당 [링크](https://github.com/sonyrainy/baekjoon/tree/main/%EB%B0%B1%EC%A4%80) 참고 <br>

## 5. 2차원 탐색 DFS, BFS
**문제**) [백준 2178](https://www.acmicpc.net/problem/2178)

>2차원 배열 형태의 미로에서 끝까지 도착하는 최단 거리를 구하는 문제이다.

해당 문제에서 **DFS로의 접근은 시간초과가 발생한다.**

DFS는 모든 경우를 탐색하며 끝을 찍은 깊이 값을 min=2147000000 값과 비교하여 최단 거리의 깊이를 구한다. **즉, 경로가 아주 많을 수 있다.**

**그렇지만 아래 이미지를 통해 BFS는 최단거리의 값을 찾으면 탐색을 종료하면 그만인 것을 알 수 있다. 최단거리를 구할 때는 BFS를 사용하면 된다.**

![DFSvsBFS](https://github.com/sonyrainy/TIL/assets/91364766/6a0f4328-899f-431c-9f07-9c25118ac0c9)

### 1) DFS로의 2178 해결(시간초과 error)
```
#include <iostream>
#include <queue>
#include <vector>
#include <stdio.h>

using namespace std;

int Min = 2147000000;
int n, m;
//int map[n][m], visited[n][m];
//map의 값을 받을 때, 숫자가 붙은 상태로 받기 때문에 char로 받아 하나하나 뜯는다.

//vector<vector<char>> map(n,vector<char>(n, '0'));
//vector<vector<int>> visited(n, vector<int>(m, 0));
char map[101][101];
int visited[101][101];

int dx[4] = { -1, 0, 1, 0 };
int dy[4] = { 0, 1, 0 , -1 };

void DFS(int x, int y, int depth) {
    int xx, yy;

    // 도착했고, 깊이가 min보다 작을 때 min과 depth를 교체한다.
    if (x == n - 1 && y == m - 1) {
        if (depth < Min) {
            Min = depth;

        }
        return;//또 해당 stack에서 차지하는 부분은 넘기면 된다.

    }
    for (int i = 0; i < 4; i++) {
        xx = x + dx[i];
        yy = y + dy[i];

        if (xx<0 || yy<0 || xx>n - 1 || yy>m - 1) { continue; }

        if (map[xx][yy] == '1' && visited[xx][yy] == 0) {
            visited[xx][yy] = 1;
            DFS(xx, yy, depth + 1);
            visited[xx][yy] = 0;
        }
    }


}


int main() {
    cin >> n >> m;

    //map 생성
    //for (int i = 0; i < n; i++) {
    //    for (int j = 0; j < m; j++) {
    //        cin >> map[i][j];
    //    }
    //}
    for (int i = 0; i < n; i++) {
        cin >> map[i];
    }
    visited[0][0] = 1;
    DFS(0, 0, 1);
    cout << Min;
    return 0;
}

```
<br>

### 2) BFS로의 2178 해결(정답)
```
#include <iostream>
#include <queue>
#include <vector>
#include <stdio.h>

using namespace std;

int Min = 2147000000;
int n, m;
//int map[n][m], visited[n][m];
//map의 값을 받을 때, 숫자가 붙은 상태로 받기 때문에 char로 받아 하나하나 뜯는다.

//vector<vector<char>> map(n,vector<char>(n, '0'));
//vector<vector<int>> visited(n, vector<int>(m, 0));
char map[101][101];

//방문 여부용
int visited[101][101];

//방문 횟수용
int check[101][101];

int dx[4] = { -1, 0, 1, 0 };
int dy[4] = { 0, 1, 0 , -1 };

void BFS(int x, int y) {
    int xx, yy;
    visited[x][y] = 1;

    queue<pair<int, int>> q;
    q.push(make_pair(x, y));

    // 큐가 비어있을 때까지 반복
    while (q.empty() == false) {
        x = q.front().first;
        y = q.front().second;

        q.pop();
        for (int i = 0; i < 4; i++) {
            xx = x + dx[i];
            yy = y + dy[i];

            // 미로의 내부 안에서
            if (xx >= 0 && xx < n && yy >= 0 && yy < m) {

                // 방문된 적 없고, 지나갈 수 있는 곳이라면
                if (visited[xx][yy] == 0 && map[xx][yy] == '1') {
                    check[xx][yy] = check[x][y] + 1;
                    visited[xx][yy] = 1;
                    q.push(make_pair(xx, yy));
                }
            }
        }
    }
}

int main() {
    cin >> n >> m;

    for (int i = 0; i < n; i++) {
        cin >> map[i];
    }

    BFS(0, 0);

    cout << check[n-1][m-1]+1;

    return 0;
}

```

---
#### +) 2차원 배열 형태 미로에서 상하좌우 탐색 TIP

![2차원 배열 탐색 TIP](https://github.com/sonyrainy/TIL/assets/91364766/c3b7c27f-8c26-4b5a-a034-e4c1c366336a)
