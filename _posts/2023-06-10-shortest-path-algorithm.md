---
title: Shortest Path algorithm
date: 2023-06-10 15:11 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---


# 최단경로 알고리즘(Shortest Algorithm)

## **뜻 그대로 가장 짧은 경로를 찾는 알고리즘!!**

- ## 다양한 문제상황 존재
   - ### 한 지점에서 다른 한 지점까지의 최단 경로
   - ### 한 지점에서 다른 모든 지점까지의 최단 경로
   - ### 모든 지점에서 다른 모든 지점까지의 최단 경로

![shortest_path1](/assets/img/post_img/shortest_path1.PNG "shortest_path1")

- ## 각 지점은 그래프에서 노드로 표현
- ## 지점 간 연결된 도로는 그래프에서 간선으로 표현

---------------------

<br/>
<br/>

# 다익스트라 알고리즘(Dijkstra Algorithm)

- 특정한 노드에서 출발하여 다른 모든 노드로 가는 최단 경로를 계산
- 다익스트라 최단 경로 알고리즘은 음의 간선이 없을 때 정상적으로 동작
    - 현실 세계의 도로(간선)은 음의 간선으로 표현되지 않습니다.
- 다익스트라 최단 경로 알고리즘은 그리디 알고리즘으로 분류
   - **매 상황에서 가장 비용이 적은 노드를 선택**해 임의의 과정 반복

- 알고리즘의 동작과정
   - 1. 출발 노드를 설정합니다.
   - 2. 최단 거리 테이블을 초기화합니다. 
   - 3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택합니다.
   - 4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단거리 테이블을 갱신합니다.
   - 5. 위 과정에서 3번과 4번을 반복합니다.


![dijkstra1](/assets/img/post_img/dijkstra1.PNG "dijkstra1")
<br/>
<br/>

![dijkstra2](/assets/img/post_img/dijkstra2.PNG "dijkstra2")
<br/>
<br/>

![dijkstra3](/assets/img/post_img/dijkstra3.PNG "dijkstra3")
<br/>
<br/>

![dijkstra4](/assets/img/post_img/dijkstra4.PNG "dijkstra4")
<br/>
<br/>

![dijkstra5](/assets/img/post_img/dijkstra5.PNG "dijkstra5")
<br/>
<br/>

![dijkstra6](/assets/img/post_img/dijkstra6.PNG "dijkstra6")
<br/>
<br/>

![dijkstra7](/assets/img/post_img/dijkstra7.PNG "dijkstra7")
<br/>
<br/>


```java
public class Practice {
    public static final int INF = (int)1e9;
    public static int n,m,start;
    public static ArrayList<ArrayList<Node>> graph = new ArrayList<ArrayList<Node>>();
    public static boolean[] visted = new boolean[100001];
    public static int[] d = new int[100001];
    public static int getSmallestNode(){
        int min_value = INF;
        int index = 0;
        for(int i = 1; i <= n; i++){
            if(d[i] < min_value && !visted[i]){
                min_value = d[i];
                index = i;
            }
        }
        return index;
    }
    public static void dijkstra(int start){
        d[start] = 0;
        visted[start] = true;

        for(int j = 0; j<graph.get(start).size(); j++){
            d[graph.get(start).get(j).getIndex()] = graph.get(start).get(j).getDistance();
        }

        for(int i = 0;i<n-1; i++){
            int now = getSmallestNode();
            visted[now] = true;

            for(int j = 0; j<graph.get(now).size(); j++){
                int cost = d[now] + graph.get(now).get(j).getDistance();

                if(cost < d[graph.get(now).get(j).getIndex()]){
                    d[graph.get(now).get(j).getIndex()] = cost;
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        n = sc.nextInt();
        m = sc.nextInt();
        start = sc.nextInt();

        for(int i = 0; i<= n;i++){
            graph.add(new ArrayList<Node>());
        }

        for(int i = 0; i<m;i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();

            graph.get(a).add(new Node(b,c));
        }

        Arrays.fill(d,INF);

        dijkstra(start);

        for(int i = 1; i<=n;i++){
            if(d[i] == INF){
                System.out.println("Infinity");
            }else{
                System.out.println(d[i]);
            }
        }
    }
}
class Node{
    private int index;
    private int distance;

    public Node(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }

    public int getIndex() {
        return index;
    }

    public int getDistance() {
        return distance;
    }
}
```


## 다익스트라 알고리즘의 특징
- 그리디 알고리즘 : ** 매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택해 임의의 과정을 반복
- 단계를 거치며 **한 번 처리된 노드의 최단 거리는 고정**되어 더 이상 바뀌지 않습니다.
    - ** 한 단계당 하나의 노드에 대한 최댄 거리를 확실히 찾는것**
- 다익스트라 알고리즘을 수행한 뒤에 ** 테이블에 각 노드까지의 최단 거리 정보가 저장**
  - 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가기능 추가
- 총 O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형탐색해야한다.
- 전체 시간 복잡도는 O($ V^2$)이다.(V는 노드개수)
- 일반적인 최단경로 문제에서 전체 노드가 5000개 이하라면 코드로 해결할 수 있다. 하지만 아닐 경우 시간 판정초과를 받을 우려가 있기에 개선이 필요하다.


## 우선순위 큐(Priority Queue)
- **우선순위가 가장 높은 데이터를 가장 먼저 삭제**하는 자료구조

<br/>

![priority_queue](/assets/img/post_img/priority_queue.PNG "priority_queue")


### 힙(Heap)
- 최솟값 또는 최댓값을 빠르게 찾아내기 위해 완전이진트리 형태로 만들어진 자료구조
- 우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나
- 최소 힙과 최대 힙이 존재
- 최소힙은 부모노드의 값이 자식보다 적은 경우고 최대힙은 반대
- 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용


## 개선된 다익스트라 알고리즘

![dijkstra_improve1](/assets/img/post_img/dijkstra_improve1.PNG "dijkstra_improve1")
<br/>
<br/>

![dijkstra_improve2](/assets/img/post_img/dijkstra_improve2.PNG "dijkstra_improve2")
<br/>
<br/>

![dijkstra_improve3](/assets/img/post_img/dijkstra_improve3.PNG "dijkstra_improve3")
<br/>
<br/>

![dijkstra_improve4](/assets/img/post_img/dijkstra_improve4.PNG "dijkstra_improve4")
<br/>
<br/>

![dijkstra_improve5](/assets/img/post_img/dijkstra_improve5.PNG "dijkstra_improve5")
<br/>
<br/>

![dijkstra_improve6](/assets/img/post_img/dijkstra_improve6.PNG "dijkstra_improve6")
<br/>
<br/>

![dijkstra_improve7](/assets/img/post_img/dijkstra_improve7.PNG "dijkstra_improve7")
<br/>
<br/>

![dijkstra_improve8](/assets/img/post_img/dijkstra_improve8.PNG "dijkstra_improve8")
<br/>
<br/>

![dijkstra_improve9](/assets/img/post_img/dijkstra_improve9.PNG "dijkstra_improve9")
<br/>
<br/>



```java
public class Practice {
    public static final int INF = (int)1e9;
    public static int n,m,start;
    public static ArrayList<ArrayList<Node>> graph = new ArrayList<ArrayList<Node>>();
    public static boolean[] visted = new boolean[100001];
    public static int[] d = new int[100001];
    public static int getSmallestNode(){
        int min_value = INF;
        int index = 0;
        for(int i = 1; i <= n; i++){
            if(d[i] < min_value && !visted[i]){
                min_value = d[i];
                index = i;
            }
        }
        return index;
    }
    public static void dijkstra(int start) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0));
        d[start] = 0;
        while(!pq.isEmpty()) {

            Node node = pq.poll();
            int dist = node.getDistance();
            int now = node.getIndex();

            if (d[now] < dist) continue;

            for (int i = 0; i < graph.get(now).size(); i++) {
                int cost = d[now] + graph.get(now).get(i).getDistance();
                if (cost < d[graph.get(now).get(i).getIndex()]) {
                    d[graph.get(now).get(i).getIndex()] = cost;
                    pq.offer(new Node(graph.get(now).get(i).getIndex(), cost));
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        n = sc.nextInt();
        m = sc.nextInt();
        start = sc.nextInt();

        for(int i = 0; i<= n;i++){
            graph.add(new ArrayList<Node>());
        }

        for(int i = 0; i<m;i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();

            graph.get(a).add(new Node(b,c));
        }

        Arrays.fill(d,INF);

        dijkstra(start);

        for(int i = 1; i<=n;i++){
            if(d[i] == INF){
                System.out.println("Infinity");
            }else{
                System.out.println(d[i]);
            }
        }
    }
}
class Node implements Comparable<Node> {
    private int index;
    private int distance;
    public Node(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }
    public int getIndex() {
        return this.index;
    }
    public int getDistance() {
        return this.distance;
    }
    @Override
    public int compareTo(Node other) {
        if (this.distance < other.distance) {
            return -1;
        }
        return 1;
    }
}
```
- 개선된 다익스트라 알고리즘의 시간복잡도는 O(E $logV$ )
- E는 간선의 수,V는 노드의 개수

<br/>
<br/>

# 플로이드 워셜 알고리즘(Floyd-Warsharr Algorithm)
- **모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산**
- 다익스트라 알고리즘과 마찬가지로 단계별로 **거쳐가는 노드를 기준으로** 알고리즘을 수행
   - 다만 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요없음
- 2차원 테이블에 최단 거리 정보를 저장
- 다이나믹 프로그래밍 유형에 속함
- 각 단계마다 **특정한 노드 k를 거쳐 가는 경우를 확인**
   - a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사

- 점화식은 
>$ D_{ab} = min(D_{ab},D_{ak} + D_{kb}) $

<br/>
<br/>

![floyd1](/assets/img/post_img/floyd1.PNG "floyd1")
<br/>
<br/>

![floyd2](/assets/img/post_img/floyd2.PNG "floyd2")
<br/>
<br/>

![floyd3](/assets/img/post_img/floyd3.PNG "floyd3")
<br/>
<br/>

![floyd4](/assets/img/post_img/floyd4.PNG "floyd4")
<br/>
<br/>

![floyd5](/assets/img/post_img/floyd5.PNG "floyd5")
<br/>
<br/>


```java
public class Practice {
    public static final int INF = (int) 1e9; 
    public static int n, m;
    public static int[][] graph = new int[501][501];
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        n = sc.nextInt();
        m = sc.nextInt();
        
        for (int i = 0; i < 501; i++) {
            Arrays.fill(graph[i], INF);
        }
        
        for (int a = 1; a <= n; a++) {
            for (int b = 1; b <= n; b++) {
                if (a == b) graph[a][b] = 0;
            }
        }
        
        for (int i = 0; i < m; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();
            graph[a][b] = c;
        }
        
        for (int k = 1; k <= n; k++) {
            for (int a = 1; a <= n; a++) {
                for (int b = 1; b <= n; b++) {
                    graph[a][b] = Math.min(graph[a][b], graph[a][k] + graph[k][b]);
                }
            }
        }
        
        for (int a = 1; a <= n; a++) {
            for (int b = 1; b <= n; b++) {
                if (graph[a][b] == INF) {
                    System.out.print("INFINITY ");
                } else {
                    System.out.print(graph[a][b] + " ");
                }
            }
            System.out.println();
        }
    }
}
```

# 최단 경로 알고리즘 문제 1 - 전보
>어떤 나라에는 N개의 도시가 있다. 그리고 각 도시는 보내고자 하는 메시지가 있는 경우, 다른 도시로 전보를 보내서 다른 도시로 해당 메시지를 전송할 수 있다.  
X라는 도시에서 Y라는 도시로 전보를 보내고자 한다면 X에서 Y로 통하는 통로는 있지만 Y에서 X로 향하는 통로가 없다면 메시지를 보낼 수 없다.
도시 C에서 위급상황이 발생했다. 최대한 많은 도시로 메시지를 보내고자 한다. 메시지는 도시 C에서 출발하여 각 도시 사이에 설치된 통로를 거쳐, 최대한 많이 퍼져나갈 것이다.  
각 도시의 번호와 통로가 설치되어 있는 정보가 주어졌을 때, 도시 C에서 보낸 메시지를 받게 되는 도시의 개수는 총 몇개이며 도시들이 모두 메시지를 받는 데까지 걸리는 시간은 얼마인지 계산하는 프로그램을 작성하시오.  

- 첫째 줄에 도시의 개수N, 통로의 개수 M, 메시지를 보내고자 하는 도시 C가 주어진다.
- 둘째 줄부터 M+1번째 줄에 걸쳐서 통로에 대한 정보 X,Y,Z가 주어진다.이는 특정 도시 X에서 다른 특정 도시 Y로 이어지는 통로가 있으며, 메시지가 전달되는 시간이 Z라는 의미다.
- 첫째 줄에 도시 C에서 보낸 메시지를 받는 도시의 총 개수와 총 걸리는 시간을 공백으로 구분하여 출력

```java
class Node implements Comparable<Node> {
    private int index;
    private int distance;

    public Node(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }

    public int getIndex() {
        return this.index;
    }

    public int getDistance() {
        return this.distance;
    }

    @Override
    public int compareTo(Node other) {
        if (this.distance < other.distance) {
            return -1;
        }
        return 1;
    }
}

public class Practice {
    public static final int INF = (int) 1e9;
    public static int n, m, start;
    public static ArrayList<ArrayList<Node>> graph = new ArrayList<ArrayList<Node>>();
    public static int[] d = new int[30001];

    public static void dijkstra(int start) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0));
        d[start] = 0;
        while(!pq.isEmpty()) { 
            Node node = pq.poll();
            int dist = node.getDistance();  
            int now = node.getIndex(); 
        
            if (d[now] < dist) continue;

            for (int i = 0; i < graph.get(now).size(); i++) {
                int cost = d[now] + graph.get(now).get(i).getDistance();
                if (cost < d[graph.get(now).get(i).getIndex()]) {
                    d[graph.get(now).get(i).getIndex()] = cost;
                    pq.offer(new Node(graph.get(now).get(i).getIndex(), cost));
                }
            }
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        start = sc.nextInt();

        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<Node>());
        }
        
        for (int i = 0; i < m; i++) {
            int x = sc.nextInt();
            int y = sc.nextInt();
            int z = sc.nextInt();
            graph.get(x).add(new Node(y, z));
        }

        Arrays.fill(d, INF);
        dijkstra(start);

        int count = 0;
        int maxDistance = 0;
        for (int i = 1; i <= n; i++) {
            if (d[i] != INF) {
                count += 1;
                maxDistance = Math.max(maxDistance, d[i]);
            }
        }
        System.out.println((count - 1) + " " + maxDistance);
    }
}
```

- 문제는 어려웠지만 정작 중요한건 다익스트라 알고리즘 구현에서 약간의 응용만 들어갔을 뿐이다. 다익스트라 알고리즘을 백지구현이 가능해 져야할 것 같다.......
<br/>
<br/>


# 최단 경로 알고리즘 문제 2 - 미래도시
>미래 도시에는 1번부터 N번까지의 회사가 있는데 특정 회사끼리는 서로 도로를 통해 연결되어 있다. 방문판매원 A는 현재 1번 회사에 위치해 있으며, X번 회사에 방문해 물건을 판매하고자 한다.   
미래 도시에서 특정 회사에 도착하기 위한 방법은 회사끼리 연결되어 있는 도로를 이용하는 방법이 유일하다. 또한 연결된 2개의 회사는 양방향으로 이동할 수 있다. 공중 미래 도시에서 특정회사와 다른 회사가 도로로 연결되어 있다면, 정확히 1만큼의 시간으로 이동할 수 있다.  
또한 오늘 방문 판매원 A는 기대하던 소개팅에도 참석하고자 한다. 소개팅의 상대는 K번 회사에 존재한다. 방문판매원 A는 X번 회사에 가서 물건을 판매하기 전에 먼저 소개팅 상대의 회사에 찾아가서 함께 커피를 마실 예정이다. 따라서 방문 판매원 A는 1번 회사에서 출발하여 K번 회사를 방문한 뒤에 X번 회사로 가는 것이 목표다.  
방문 판매원이 회사 사이를 이동하게 되는 최소시간을 계산하는 프로그램을 작성해라
- 첫째 줄에 전체 회사의 개수 N과 경로의 개수 M이 공백으로 구분되어 차례대로 주어진다.
- 둘째 줄부터 M+1번째 줄에는 연결된 두 회사의 번호가 공백으로 구분되어 주어진다. 
- M+2번째 줄에는 X와 K가 공백으로 구분되어 차례대로 주어진다.
- 첫째 줄에 방문 판매원 A가 K번 회사를 거쳐 X번 회사로 가는 최소 이동시간을 출력한다.
- 만약 X번 회사에 도달할 수 없다면 -1을 출력한다.

```java
public class Practice {
    public static final int INF = (int) 1e9;
    public static int n, m, x, k;
    public static int[][] graph = new int[101][101];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        n = sc.nextInt();
        m = sc.nextInt();

        for (int i = 0; i < 101; i++) {
            Arrays.fill(graph[i], INF);
        }

        for (int a = 1; a <= n; a++) {
            for (int b = 1; b <= n; b++) {
                if (a == b) graph[a][b] = 0;
            }
        }

        for (int i = 0; i < m; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            graph[a][b] = 1;
            graph[b][a] = 1;
        }

        x = sc.nextInt();
        k = sc.nextInt();

        for (int k = 1; k <= n; k++) {
            for (int a = 1; a <= n; a++) {
                for (int b = 1; b <= n; b++) {
                    graph[a][b] = Math.min(graph[a][b], graph[a][k] + graph[k][b]);
                }
            }
        }
        int distance = graph[1][k] + graph[k][x];

        if (distance >= INF) {
            System.out.println(-1);
        }else {
            System.out.println(distance);
        }
    }
}
```
- 최단경로 알고리즘은 모두 알고리즘 자체를 구현하고 이해하고 익숙해지면 문제상 응용은 그렇게 많이 들어가지 않는 느낌이다. 더 이해를 높이고 익숙해지자

------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]