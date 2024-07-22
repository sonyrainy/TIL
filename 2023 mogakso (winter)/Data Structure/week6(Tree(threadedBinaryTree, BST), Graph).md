- Binary Tree(이진 트리) : 이진트리는 각 노드가 최대 2개(1개만 있을 수도, 없을 수도 있다.)의 자식을 가질 수 있는 트리 구조이다. 각 노드는 왼/오 방향의 자식 노드를 가리킬 수 있고, 해당 구조를 통해 데이터를 효율적으로 저장/탐색 할 수 있다.

이진트리를 연결리스트로 표현하면 각 노드당 2개의 링크필드를 갖는다. n개의 노드가 있는 이진 트리는 총 2n개의 링크 필드를 가지게 된다. 모두 연결된 이진트리라고 보자.

이 때, null 링크는 n+1개, null이 아닌 링크는 n-1개이다.

ex) 노드가 7개라고 했을 때, 가장 마지막 노드는 4개이고, 해당 노드만이 null을 가지니까, null인 링크는 8(n+1)개, 연결된 링크는 6(n-1)개로 볼 수 있다.

<br>

- BST(Binary Search Tree) : 각 노드의 왼쪽 자식 노드가 해당 노드 값보다 작고, 오른쪽은 해당 노드의 값보다 크다. 데이터 삽입, 삭제, 탐색 등의 작업을 효율적으로 수행 가능하다.

ex) 50, 15, 62, 80, 7, 54, 11

<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/646640c2-efc1-4fe0-8887-bef37b2f92b8" width= "650" />

<br>
<br>

- Threaded Binary Tree(스레드 이진트리) : 스택을 사용하지 않고, 포인터를 이용해 순회 시간을 단축시키는 이진 트리이다.
>각 노드에는 추가적인 포인터로 이전 노드나 다음 노드를 가리키는 스레드가 포함된다. 이를 통해서 in-order traversal(중위 순회)를 수행 시, 스택 사용하지 않고 순회가 가능하다.
>
>각 노드에는 추가적인 포인터로 이전 노드나 다음 노드를 가리키는 쓰레드가 포함된다.

+) Binary Tree의 가장 아래 노드에서 null을 가리키던 링크필드들이 특정 노드를 가리키도록 하는 조정 방법을 만드는데, 여기서 조정된 null 링크를 스레드(thread)라고 한다. 즉 스레드 이진트리는 기존 이진트리 구조에 2개의 스레드를 추가하여 만든 것으로 볼 수 있다.
<p align="center"><img src="https://github.com/sonyrainy/TIL/assets/91364766/b6429ea3-343e-4c92-b618-178eaa5daeea" width="550" />

위 그림에서 가장 아래의 노드를 볼 때, 스레드를 통해 값이 참인 것을 (선행자(어떤 노드의 바로 앞에 방문되는 노드), 후속자(다음에 방문하는 노드)를 가리키고), 거짓(링크가 자식을 가리키는 경우)이면 (자식을 가리키는 링크)로 구분한다.

그렇지만, 문제가 발생하는데, 처음 노드의 선행자와 마지막 노드의 후속자를 가리킬 수가 없게 된다. 이 때, 헤드 노드를 추가해 이를 가리키도록 해서 문제를 해결할 수 있다(헤드 노드의 왼쪽 자식은 원래 이진트리의 헤드 노드를 가리키고, 오른쪽 자식은 자기 자신을 가리키도록 한다.).

+) 중위 순회 수행 과정 : 1) 왼쪽 자식이 있으면 해당 자식 노드로 이동, 2) 왼쪽 자식이 없으면 현재 노드 출력 후 오른쪽 자식 노드로 이동, 3) 이 때 오른쪽 자식이 없으면 이전 노드로 이동, 4) 이전 노드로 이동 후, 1)부터 반복

---

- Graph

+) Dijkstra(다익스트라) : 그래프의 한 노드에서 다른 노드까지의 최단 경로를 구하는 알고리즘 중 하나이다. 음이 아닌 가중치를 지닌 그래프에서 사용한다.

>1. 출발 정점을 선택
>2. 출발 정점에서 각 정점까지의 거리를 저장하는 배열을 초기화하고, 출발 정점을 거리 0, 나머지는 무한대로 초기화한다.
>3. 우선순위 큐로 아직 방문하지 않은 정점 중 최소 거리를 갖는 정점을 선택한다.
>4. 선택한 정점으로부터 인접한 정점에 대한 거리를 업데이트 한다. 선택된 정점이 경유지가 되어 인접한 정점으로 가는 거리와 현재까지의 최단 거리를 비교해서 더 짧은 거리로 업데이트 한다.
>5. 3, 4 과정을 반복한다.

+) Bellman-Ford Algorithm(벨만포드) : 최단 경로를 구하는 알고리즘(음수 간선 순환을 탐지할 수 있다.)이다.

>1. 시작 정점으로부터 다른 모든 정점까지의 거리를 무한대로 초기화 하고, 시작 정점의 거리는 0으로 한다.
>2. 해당 정점으로부터 도달 가능한 정점과 그 간선의 값을 파악하고 추가한다.
>3. 새로 들어온 노드에서 도달할 수 있는 원래 있던 노드 간의 거리를 재비교한다.
>4. 반복하며 해당 간선을 이용해 도달할 수 있는 정점들의 거리를 갱신한다.
>5. 위 과정을 모든 정점에 대해 반복한다((정점의 수-1)번 반복)

→ 수행 시간은 O(V*E)인데, vertex가 하나 추가될 때마다 모든 edge를 한 번씩 다 비교해보니까 그렇다고 볼 수 있다.


+) Prim's Algorithm(프림) : minimum spanning tree를 구하기 위한 알고리즘이다(모든 정점을 포함하며 간선의 가중치 합이 최소가 되는 부분 그래프를 찾는 알고리즘).

>1. 임의의 시작 노드을 선택하고, 현재 트리에 추가한다.
>2. 선택된 노드과 연결된 간선 중 가장 가중치가 작은 간선을 선택해 해당 간선의 도착 노드를 트리에 추가한다.
>3. 트리에 추가된 노드와 연결된 간선 중 가장 작은 가중치를 갖는 간선을 선택해 해당 간선의 도착 노드을 트리에 추가한다.
>4. 모든 노드가 트리에 포함될 때까지 2, 3 과정을 반복한다.

(생성된 영역에서 가장 가까운 간선을 가지고 있는 노드로 점점 넓어지는 느낌으로 볼 수 있다.)
