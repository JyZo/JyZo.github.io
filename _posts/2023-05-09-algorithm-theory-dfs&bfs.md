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

# DFS(Depth-First Search)

1. **깊이 우선 탐색**이라고도 하며 그래프에서 깊은 부분을 우선탐색하는 알고리즘
2. 스택 자료구조(혹은 재귀 함수)를 이용하며, 구체적인 동작 과정은 아래와 같다.
    1) 탐색 시작 노드를 스택에 삽입하고 방문처리를 한다.
    2) 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리합니다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냅니다.
    3) 더이상 2번의 과정을 수행할 수 없을 때까지 반복합니다. 





![DFS1](/assets/img/post_img/DFS1.gif "DFS1")








   

   # BFS(Breadth-First Search)

   1. **너비 우선 탐색**이라고도 부르며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘
   2. 큐 자료구조를 이용하며, 구체적인 동작과정은 아래와 같다. 
        1) 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
        2) 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리합니다.
        3) 더 이상 2번의 과정을 수행할 수 없을 때까지 반복합니다.
    


![BFS1](/assets/img/post_img/BFS1.gif "BFS1")
<br/>
https://www.codesdope.com/course/algorithms-dfs/

