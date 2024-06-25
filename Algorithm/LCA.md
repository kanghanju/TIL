## LCA(Lowest Common Ancestor) 최소 공통 조상 
#### 공부 날짜: 2024/06/25

<br><br>
### LCA(Lowest Common Ancestor) 최소 공통 조상 알고리즘이란?
> 트리 구조에서 두 노드의 공통 조상 중 가장 낮은 조상을 찾는 알고리즘이다. 

<br>

LCA 알고리즘을 구현하는 방법에는 여러 가지가 있다.<br>
각 방법의 시간 복잡도는 다르며, 다양한 상황에 따라 적합한 방법이 달라질 수 있다.

<br>

### 관련 문제 
[백준11437](https://www.acmicpc.net/problem/11437)


[백준11438](https://www.acmicpc.net/problem/11438)


희소 테이블, 세그먼트 트리 등을 이용해서 효율적으로 푸는 방법도 있지만, 먼저 단순한 풀이를 찾아봤다. 

<br>

### 구현 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

    static List<Integer>[] list;
    static int[] parent, depth;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());//n개의 정점

        parent = new int[n + 1];
        depth = new int[n + 1];
        list = new ArrayList[n + 1];
        for (int i = 1; i < n + 1; i++) {
            list[i] = new ArrayList<>();
        }

        StringTokenizer st;
        //트리 구성 
        for (int i = 0; i < n - 1; i++) {//n-1개의 줄에 트리 상에서 연결된 두 정점이 주어진다.
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            list[a].add(b);
            list[b].add(a);
        }

        init(1, 1, 0); //1번째 노드는 높이가 1이고 부모 노드가 0이다.

        StringBuilder sb = new StringBuilder();
        int m = Integer.parseInt(br.readLine());
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            sb.append(LCA(a,b) + "\n");
        }
        System.out.println(sb.toString());

    }

    static void init(int cur, int h, int pa) {//현재노드,높이,부모노드
        depth[cur] = h;
        parent[cur] = pa;
        for (int next : list[cur]) {//현재 노드와 연결된 다른 노드들을 찾는다
            if (next != pa) {
                init(next, h + 1, cur);//연결된 노드가 부모 노드가 아니라 자식 노드라면 자식노드 초기화 
            }
        }
    }
    
    static int LCA(int a,int b) {
        int aHeight = depth[a];
        int bHeight = depth[b];
        
        while(aHeight > bHeight) {//두 노드의 깊이를 맞춘다.
            a = parent[a];
            ah--;
        }
        
        while(bHeight > aHeight) {
            b = parent[b];
            bh--;
        }
        
        while(a != b) {//두 노드의 깊이가 같아지면 두 노드가 같아질때까지( = 같은 부모를 찾을 때까지 ) 부모 노드로 올라가며 공통 조상을 찾는다. 
            a = parent[a];
            b = parent[b];
        }
        
        return a;
    }
}

```

<br>

### 알고리즘 설명 
1. 입력값을 받아 트리를 구성한다. 이때 인접 리스트를 활용했다 !!
2. DFS를 통해 각 노드의 깊이와 부모를 설정한다.
3. LCA를 계산한다. 

<br>

#### 참고 자료 
[자료1](https://loosie.tistory.com/360)
