## 다익스트라(Dijkstra) 알고리즘
#### 공부 날짜: 2024/06/27

<br><br>
### 다익스트리 알고리즘이란?
> 특정 시작점에서 다른 모든 정점으로 가는 **최단거리**를 각각 구해주는 알고리즘이다.

<br>

다익스트라를 구현하기 위해서는 두 가지를 저장해야 한다. 
1. 해당 정점까지의 **최단 거리 저장**
2. 해당 정점을 방문했는지 저장 

<br>

### 시간 복잡도
> 인접 행렬로 구현: O(N^2)

>인접 리스트로 구현: O(N*logN)

<br>

### 알고리즘 순서(인접행렬)
1. distance(정점 v로부터 모든 정점까지의 최단거리)를 초기화 해준다.
2. 시작 노드가 1이므로 시작노드의 distance와 check값을 변경해준다.
3. 시작 노드와 연결되어 있는 distance값을 갱신한다.
4. 방문하지 않은 노드중 distance가 최소인 값을 찾는다.
5. distance가 최소인 노드의 check값을 true로 설정한다(방문).
6. distance가 최소인 노드를 선택된 노드라고 하자
7. 선택된 노드를 경유하여 다른 노드들의 distance 값을 갱신한다. 
8. 4 ~ 7번을 모든 노드를 방문할때까지 반복한다. 


<br>

### 구현 코드(인접행렬)
```java
class Graph {
    private int n; //노드 수
    private int maps[][]; //노드 들 간의 가중치를 저장
    
    public Graph(int n) {
        this.n = n;
        maps = new int[n + 1][n + 1];
    }
    
    public void input(int i,int j,int w) {
        maps[i][j] = w;
        maps[j][i] = w;
    }
    
    public void dijkstra(int v) {//v부터 다른 모든 노드까지 최단 거리를 계산한다. 
        int[] distance = new int[n + 1]; //각 정점까지의 최단 거리를 저장한다
        boolean[] check = new boolean[n + 1]; //해당 노드를 방문했는지 체크
        
        //distance 값 초기화
        for(int i = 1; i < n + 1; i++) {
            distance[i] = Integer.MAX_VALUE;
        }
        
        //시작 노드값 초기화
        distance[v] = 0;
        check[v] = true;
        
        //연결노드 distance 갱신
        for(int i = 1; i < n + 1; i++) {
            if (!check[i] && maps[v][i] != 0) {//방문하지 않았고 정점v랑 연결되어있는 노드
                distance[i] = maps[v][i];
            }
        }
        
        for(int a = 0; a < n - 1; a++) { //시작 노드를 제외한 모든 노드 처리 
            //원래 노드 거리 중 최솟값 찾기
            int min = Integer.MAX_VALUE; //방문하지 않은 노드 중 가장 작은 거리를 가진 노드를 저장
            int minIndex = -1; //그 노드의 인덱스 저장 
            
            for(int i = 1; i <= n; i++) {//가장 작은 거리를 가진 노드를 찾는다 
                if(!check[i] && distance[i] < min) {
                    min = distance[i];
                    minIndex = i;
                }
            }
            
            check[minIndex] = true;//해당 노드는 방문으로 표시 
            
            for(int i = 1; i <= n; i++) {//가장 작은 거리를 가진 노드를 시작 노드로 해서 또 최단 거리를 찾는 것. 
                if(!check[i] && maps[minIndex][i] != 0) {//방문하지 않았고 minIndex 노드와 연결된 노드의 거리 갱신 
                    if(distance[i] > distance[minIndex] + maps[minIndex][i]) {//v부터 minIndex까지 거리 + minIndex부터 i까지의 거리 
                        distance[i] = distance[minIndex] + maps[minIndex][i];
                    }
                }
            }
            
            //결과 출력
            for(int i = 1; i <= n; i++) {
                System.out.println("Node: " + v + " to Node" + i + " distance: " + distance[i]);
            }
        }
        
        
    }

    public static void main(String[] args) {
        Graph g = new Graph(8);
        g.input(1, 2, 3);
        g.input(1, 5, 4);
        g.input(1, 4, 4);
        g.input(2, 3, 2);
        g.input(3, 4, 1);
        g.input(4, 5, 2);
        g.input(5, 6, 4);
        g.input(4, 7, 6);
        g.input(7, 6, 3);
        g.input(3, 8, 3);
        g.input(6, 8, 2);
        g.dijkstra(1);
    }
}

```

<br><br>

#### 참고자료
[자료 1](https://bumbums.tistory.com/4)