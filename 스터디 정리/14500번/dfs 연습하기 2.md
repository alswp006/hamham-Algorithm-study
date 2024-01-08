# 미로 탈출
[문제]

N x M 크기의 직사각형 형태의 미로에 여러 마리의 괴물이 있어 이를 피해 탈출해야 한다. 현재 위치는 (1, 1)이고 미로의 출구는 (N,M)의 위치에 존재하며 한 번에 한 칸씩 이동할 수 있다. 괴물이 있는 부분은 0으로, 괴물이 없는 부분은 1로 표시되어 있다. 미로는 반드시 탈출할 수 있는 형태로 제시된다. 탈출하기 위해 움직여야 하는 최소 칸의 개수를 구하라. 칸을 셀 때는 시작 칸과 마지막 칸을 모두 포함해서 계산한다.

### 구현 코드
``` python
import sys
from collections import deque
input = sys.stdin.readline

n, m = map(int, input().split())
arr = [list(map(int,input().rstrip())) for i in range(n)]
q = deque()
q.append((0,0))
move_type = [(0,1), (1,0), (0,-1), (-1,0)]

while q:
    x,y = q.popleft()
    for i in range(4):
        nx = x + move_type[i][0]
        ny = y + move_type[i][1]
        if nx < 0 or nx >= n or ny < 0 or ny >= m:
            continue
        if arr[nx][ny] == 1 and nx + ny != 0 :
            arr[nx][ny] = arr[x][y] + 1
            q.append((nx, ny))
print(arr[n-1][m-1])
```
