### 깊이 우선 탐색(DFS)
**스택**을 기반으로 구현한다.

시작 정점으로부터 한 방향으로 갈 수 있을 때까지 계속 가다가 **더 이상 갈 수 없게 될 때 backtracking을 하여 다시 가장 가까운 곳으로 연결하여 다른 방향으로 다시 탐색을 진행**하는 방법이다.


```c
void DFS(int v){
    int i;
    visit[v] = 1;
    for(i = 1; i < n; i++){
        if(map[v][i] == 1 && !visit[i]){
            printf("%d에서 %d로 이동\n", v, i);
            DFS(i);
        }
    }
}
```
### 너비 우선 탐색(BFS)
**큐**를 기반으로 구현한다.

**시작 정점으로부터 가까운 정점을 먼저 방문**하고 멀리 떨어져 있는 정점(오름차순)을 나중에 방문하는 순회 방법이다.

```c
void BFS(int v){
    int i;
    visit[v] = 1;
    printf("%d에서 시작\n", v);
    queue[rear++] = v;
    while(front < rear){
        v = queue[front++];
        for(i = 1; i < n; i++){
            if(map[v][i] == 1 && !visit[i]){
                visit[i] = 1;
                printf("%d에서 %d로 이동\n", v, i);
                queue[rear++] = i;
            }
        }
    }
}
```