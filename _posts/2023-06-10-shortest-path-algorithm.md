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


<br/>
<br/>

------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]