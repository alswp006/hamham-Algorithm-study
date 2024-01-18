# 특정 거리의 도시 찾기
## 문제
어떤 나라에는 1번부터 N번까지의 도시와 M개의 단방향 도로가 존재한다. 모든 도로의 거리는 1이다.
이 때 특정한 도시 X로부터 출발하여 도달할 수 있는 모든 도시 중에서, 최단 거리가 정확히 K인 모든 도시들의 번호를 출력하는 프로그램을 작성하시오. 또한 출발 도시 X에서 출발 도시 X로 가는 최단 거리는 항상 0이라고 가정한다.
예를 들어 N=4, K=2, X=1일 때 다음과 같이 그래프가 구성되어 있다고 가정하자.
이 때 1번 도시에서 출발하여 도달할 수 있는 도시 중에서, 최단 거리가 2인 도시는 4번 도시 뿐이다.  2번과 3번 도시의 경우, 최단 거리가 1이기 때문에 출력하지 않는다.

## 구현 코드
``` python
import sys
from collections import deque

input = sys.stdin.readline

n, m, distance, start = map(int, input().split())
graph = [[] for _ in range(n + 1)]
answer = [-1 for _ in range(n + 1)]
answer[start] = 0
q = deque()
q.append(start)

for _ in range(m):
    a, b = map(int,input().split())
    graph[a].append(b)

while q:
    x = q.popleft()
    for node in graph[x] :
        if answer[node] == -1:
            answer[node] = answer[x] + 1
            q.append(node)
print(answer if distance in answer else -1)
```

## 구현 코드 2
``` python
n, m, k, x = map(int, input().split())
dis = [[] for i in range(n + 1)]

for i in range(m):
    start, end = map(int, input().split())
    dis[start].append(end)

answer = [99999999 for i in range(n + 1)]
answer[1] = 0
for i in range(len(dis)):
    for j in dis[i] :
        answer[j] = min(answer[j], answer[i] + 1)

print(answer)
```

- 구현 코드 1과 구현 코드 2의 차이점은?
  -> 코드 1은 bfs를 사용하여 시간 복잡도가 O(V+E)이다.(V : 노드 수, E : 간선 수) 하지만 코드 2는 모든 노드 간의 거리를 다 계산하므로 노드가 n개일 때 최악의 시간 복잡도는 O(n^2)이다. 자료구조가 괜히 있는 것이 아니니 시간 복잡도를 잘 생각하여 쓰자.
