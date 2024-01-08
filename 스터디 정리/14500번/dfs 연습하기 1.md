## 음료수 얼려먹기
[문제]

N × M 크기의 얼음 틀이 있다. 구멍이 뚫려 있는 부분은 0, 칸막이가 존재하는 부분은 1로 표시된다. 
구멍이 뚫려 있는 부분끼리 상, 하, 좌, 우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주한다. 
이때 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을 작성하라. 
다음의 4 × 5 얼음 틀 예시에서는 아이스크림이 총 3개가 생성된다.

<img width="783" alt="image" src="https://github.com/alswp006/hamham-Algorithm-study/assets/102672547/d354e7ff-4cc4-48c1-8982-b796359c74ed">

### 구현 코드
``` python
import sys

input = sys.stdin.readline

n, m = map(int, input().split())
arr = [list(map(int,input().rstrip())) for i in range(n)]
answer = 0

def dfs(x, y):
    if x < 0 or x >= n or y < 0 or y >= m:
        return False

    if arr[x][y] == 1:
        return False

    arr[x][y] = 1
    dfs(x + 1, y)
    dfs(x - 1, y)
    dfs(x, y + 1)
    dfs(x, y - 1)

for i in range(len(arr)) :
    for j in range(len(arr[i])) :
        if arr[i][j] == 0:
            dfs(i, j)
            answer+=1
print(answer)
```
