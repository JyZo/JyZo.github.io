---
title: algorithm-theory-DFS&BFS
date: 2023-05-09 22:03 +0900
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---

# 그래프 탐색 알고리즘

**탐색이란 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정!!**
--------------
<br/>

- 그 중 DFS/BFS는 매우 자주 등장하는 유형으로 충분히 숙지할 것!
- 탐색 알고리즘 숙지 전 먼저 알아야할 자료구조 두가지부터 알아 보자

<br/>

# 스택(Stack)

1. 먼저 들어 온 데이터가 나중에 나가는 형식(선입후출)의 자료구조
2. **입구와 출구가 동일한 형태**로 스택을 시각화

![stack1](/assets/img/post_img/stack1.PNG "stack1")



![stack2](/assets/img/post_img/stack2.PNG "stack2")

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        Stack<Integer> stack = new Stack<>();

        stack.push(5);
        stack.push(7);
        stack.push(4);
        stack.pop();
        stack.push(4);
        stack.push(1);
        stack.pop();

        while (!stack.empty()){
            System.out.println(stack.peek());
            stack.pop();
        }
    }
}
```
- push()로 값을 넣고 pop()으로 나중에 들어온 값을 빼낸다.
- peek()로 빼내기 전 최상단에 있는 값을 알 수 있다.

<br/>
<br/>

# 큐(Queue)

1. 먼저 들어 온 데이터가 먼저 나가는 형식(선입선출)의 자료구조
2. **입구와 출구가 모두 뚫려있는 터널과 같은 형태**로 큐를 시각화

![queue1](/assets/img/post_img/queue1.PNG "queue1")



![queue2](/assets/img/post_img/queue2.PNG "queue1")

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        Queue<Integer> queue = new LinkedList<>();

        queue.offer(5);
        queue.offer(4);
        queue.offer(7);
        queue.poll();
        queue.offer(1);
        queue.offer(3);
        queue.poll();

        while (!queue.isEmpty()){
            System.out.println(queue.poll());
        }
    }
}
```
- offer()로 값을 넣고 poll()로 먼저 들어온 값을 빼낸다.

<br/>
<br/>

# 재귀함수

1. **자기 자신을 다시 호출하는 함수**를 의미한다.
2. 재귀 함수를 풀이에서 사용할 때는 재귀함수의 종료조건을 반드시 명시

EX) 최대 공약수 계산(유클리드 호제법) 예제

- 두 자연수 A,B에 대하여 (A>B) A를 B로 나눈 나머지를 R이라고 한다.
- 이 때 A와 B의 최대공약수는 B와 R의 최대 공약수와 같다.

![GCD1](/assets/img/post_img/GCD1.PNG "GCD1")

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int A, B;
        int numTotal = 0;
        Scanner sc = new Scanner(System.in);
        A = sc.nextInt();
        B = sc.nextInt();

        System.out.println(GCD(A, B));
    }
    static int GCD(int A, int B){
        if( A % B == 0){
            return B;
        }else{
            return GCD(B, A % B);
        }
    }
}
```
- 모든 재귀함수는 반복문을 이용해 동일 기능 구현 가능
- 반복문보다 유리한 경우도 있고 불리한 경우도 있다.
- 컴퓨터가 함수를 연속호출하면 메모리의 스택프레임에 쌓이기에 스택을 사용해야 할 때 라이브러리 대신 이용하는  
경우가 많다. 

<br/>
<br/>

# DFS(Depth-First Search)

1. **깊이 우선 탐색**이라고도 하며 그래프에서 깊은 부분을 우선탐색하는 알고리즘
2. 스택 자료구조(혹은 재귀 함수)를 이용하며, 구체적인 동작 과정은 아래와 같다.  
    1) 탐색 시작 노드를 스택에 삽입하고 방문처리를 한다.  
    2) 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리합니다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냅니다.  
    3) 더이상 2번의 과정을 수행할 수 없을 때까지 반복합니다.  

![DFS1](/assets/img/post_img/DFS1.gif "DFS1")

```java
public class Practice {
    public static boolean[] visited = new boolean[9];
    public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

    // DFS 함수 정의
    public static void dfs(int x) {
        // 현재 노드를 방문 처리
        visited[x] = true;
        System.out.print(x + " ");
        // 현재 노드와 연결된 다른 노드를 재귀적으로 방문
        for (int i = 0; i < graph.get(x).size(); i++) {
            int y = graph.get(x).get(i);
            if (!visited[y]) dfs(y);
        }
    }

    public static void main(String[] args) {
        // 그래프 초기화
        for (int i = 0; i < 9; i++) {
            graph.add(new ArrayList<Integer>());
        }

        // 노드 1에 연결된 노드 정보 저장
        graph.get(1).add(2);
        graph.get(1).add(3);
        graph.get(1).add(8);

        // 노드 2에 연결된 노드 정보 저장
        graph.get(2).add(1);
        graph.get(2).add(7);

        // 노드 3에 연결된 노드 정보 저장
        graph.get(3).add(1);
        graph.get(3).add(4);
        graph.get(3).add(5);

        // 노드 4에 연결된 노드 정보 저장
        graph.get(4).add(3);
        graph.get(4).add(5);

        // 노드 5에 연결된 노드 정보 저장
        graph.get(5).add(3);
        graph.get(5).add(4);

        // 노드 6에 연결된 노드 정보 저장
        graph.get(6).add(7);

        // 노드 7에 연결된 노드 정보 저장
        graph.get(7).add(2);
        graph.get(7).add(6);
        graph.get(7).add(8);

        // 노드 8에 연결된 노드 정보 저장
        graph.get(8).add(1);
        graph.get(8).add(7);

        dfs(1);
    }
}
```
<br/>
<br/>

# BFS(Breadth-First Search)

1. **너비 우선 탐색**이라고도 부르며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘
2. 큐 자료구조를 이용하며, 구체적인 동작과정은 아래와 같다.  
    1) 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.  
    2) 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리합니다.  
    3) 더 이상 2번의 과정을 수행할 수 없을 때까지 반복합니다.  


![BFS1](/assets/img/post_img/BFS1.gif "BFS1")

```java
public class Practice {
    public static boolean[] visited = new boolean[9];
    public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();
    // BFS 함수 정의
    public static void bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        // 현재 노드를 방문 처리
        visited[start] = true;
        // 큐가 빌 때까지 반복
        while(!q.isEmpty()) {
            // 큐에서 하나의 원소를 뽑아 출력
            int x = q.poll();
            System.out.print(x + " ");
            // 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
            for(int i = 0; i < graph.get(x).size(); i++) {
                int y = graph.get(x).get(i);
                if(!visited[y]) {
                    q.offer(y);
                    visited[y] = true;
                }
            }
        }
    }
    public static void main(String[] args) {
        // 그래프 초기화
        for (int i = 0; i < 9; i++) {
            graph.add(new ArrayList<Integer>());
        }
        // 노드 1에 연결된 노드 정보 저장
        graph.get(1).add(2);
        graph.get(1).add(3);
        graph.get(1).add(8);

        // 노드 2에 연결된 노드 정보 저장
        graph.get(2).add(1);
        graph.get(2).add(7);

        // 노드 3에 연결된 노드 정보 저장
        graph.get(3).add(1);
        graph.get(3).add(4);
        graph.get(3).add(5);

        // 노드 4에 연결된 노드 정보 저장
        graph.get(4).add(3);
        graph.get(4).add(5);

        // 노드 5에 연결된 노드 정보 저장
        graph.get(5).add(3);
        graph.get(5).add(4);

        // 노드 6에 연결된 노드 정보 저장
        graph.get(6).add(7);

        // 노드 7에 연결된 노드 정보 저장
        graph.get(7).add(2);
        graph.get(7).add(6);
        graph.get(7).add(8);

        // 노드 8에 연결된 노드 정보 저장
        graph.get(8).add(1);
        graph.get(8).add(7);

        bfs(1);
    }
}
```

<br/>
<br/>

## DFS문제1 - 음료수 얼려먹기 
> N X M 크기의 얼음 틀이 있습니다. 구멍이 뚫려 있는 부분은 0, 칸막이가 존재하는 부분은 1로 표시됩니다. 구멍이 뚫려있는 부분끼리 상,하,좌,우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주합니다. 이때 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을 작성하세요. 다음의 4 X 5 얼음 틀 예시에서는 아이스크림이 총 3개 생성됩니다. 

![DFSquest1](/assets/img/post_img/DFSquest1.PNG "DFSquest1")

```java
public class Practice {
    public static int N, M;
    public static String ICE;
    public static int ICEPACK[][] = new int[1000][1000];
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        M = sc.nextInt();

        for(int i = 0;i<N;i++){
            for(int j = 0;j<M;j++){
                ICE = sc.next();
                ICEPACK[i][j] = Integer.parseInt(ICE);
            }
        }

        int result = 0;
        for(int i = 0;i<N;i++){
            for(int j = 0;j<M;j++){
                if(dfs(i,j)){
                    result++;
                };
            }
            System.out.println();
        }
        System.out.println("result:"+result);
    }
    public static boolean dfs(int x,int y){

        if(x <= -1 || x>= N || y<= -1 || y>= M){
            return false;
        }

        if(ICEPACK[x][y] == 0){
            ICEPACK[x][y] = 1;

            dfs(x,y+1);
            dfs(x,y-1);
            dfs(x+1,y);
            dfs(x-1,y);
            return true;
        }
    return false;
    }
}
```

- 이문제 같은 경우 아이디어는 어느정도 떠올렸으나 구현을 제대로 하지 못한 케이스 복습은 당연히 필수

<br/>
<br/>

## BFS문제1 - 미로탈출 문제
> 동빈이는 N X M 크기의 직사각형 형태의 미로에 갇혔습니다. 미로에는 여러 마리의 괴물이 있어 이를 피해 탈출해야 합니다. 동빈이의 위치는 (1,1)이며 미로의 출구는 (N,M)의 위치에 존재하며 한번에 한칸씩 이동할 수 있습니다. 이때 괴물이 있는 부분은 0으로, 괴물이 없는 부분은 1로 표시되어 있습니다. 이때 동빈이가 탈출하기 위해 움직여야 하는 최소 칸의 개수를 구하시오 

```java
public class Practice {
    public static int N, M;
    public static String LOAD;
    public static int MAZE[][] = new int[1000][1000];
    public static int dx[] = {-1,1,0,0};
    public static int dy[] = {0,0,-1,1};

    public static int bfs(int x, int y){
        Queue<Node> q = new LinkedList<>();
        q.offer(new Node(x,y));

        while(!q.isEmpty()){
            Node node = q.poll();
            x = node.getX();
            y = node.getY();

            for(int i = 0; i<4; i++){
                int nx = x+dx[i];
                int ny = y+dy[i];

                if(nx < 0 || nx >= N || ny <0 || ny >= M) continue;

                if(MAZE[nx][ny] == 0) continue;

                if(MAZE[nx][ny] == 1){
                    MAZE[nx][ny] = MAZE[x][y] + 1;
                    q.offer(new Node(nx,ny));
                }
            }
        }
        return MAZE[N-1][M-1];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        M = sc.nextInt();
        sc.nextLine();

        for(int i = 0;i<N;i++){
            for(int j = 0;j<M;j++){
                LOAD = sc.next();
                MAZE[i][j] = Integer.parseInt(LOAD);
            }
        }
        System.out.println(bfs(0,0));
    }
}
class Node{
    private int x;
    private int y;
    public Node(int x, int y) {
        this.x = x;
        this.y = y;
    }
    public int getX() {
        return x;
    }
    public int getY() {
        return y;
    }
}
```


- BFS는 간선의 비용이 같을 때 최단거리 판단가능, 상하좌우 모든 거리가 1로 동일
- 따라서 모든 노드의 최단거리 값을 기록하여 해결


복습들이랑 공부가 많이 필요할 듯 하다...이전의 100제나 구현처럼 특별한 알고리즘이 들어가지 않을때와 비교해 난이도가 확 올랐다. 아무 힌트나 참고없이 구현을 점차 못하고 있다. 수학이라고 생각하고 빨리 이론들 끝내고 문제풀면서 숙련도들을 올려야 겠다. 


<br/>
<br/>

------------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]  
사진 출처 - 외국 알고리즘 사이트[[https://www.codesdope.com/course/algorithms-introduction/](https://www.codesdope.com/course/algorithms-introduction/)]


