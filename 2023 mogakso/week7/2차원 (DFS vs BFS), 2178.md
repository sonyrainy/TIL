일단 업로드 하고 오후에 다시 정리...하기
---

일단 DFS로 접근은 시간초과 야무지게 발생한다.
dfs는 완전탐색 후 가장 작은 값을 선택
경로가 아주 많을 수 잇음.
시간복잡도 커짐

![2차원 배열 탐색 TIP](https://github.com/sonyrainy/TIL/assets/91364766/c3b7c27f-8c26-4b5a-a034-e4c1c366336a)

![DFSvsBFS](https://github.com/sonyrainy/TIL/assets/91364766/6a0f4328-899f-431c-9f07-9c25118ac0c9)


근데 bfs는 최단거리 보장으로 볼 수 있음.
최단인 부분에 제일 먼저 도착하면 끝내면 그만이기 때문

https://nulls.co.kr/graph/141

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
