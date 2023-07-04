---
title: add data structure & algorithm
date: 2023-07-02 22:51 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---


# 추가 자료구조 및 알고리즘

- 나동빈 개발자님이 묶어놓은 이코테 인강에 빠진 추가적으로 필요하다고 여긴 개념 몇가지를 추가해 놓으셨고 그걸 마무리로 인강을 마무리 해보도록 한다.


# 우선순위 큐(Primary Queue)
- 우선순위 큐는 **우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조** 이다.
- 우선순위 큐는 데이터를 우선순위에 따라 처리하고 싶을 때 사용
- 이 우선순위 큐는 실제로 최단경로 알고리즘의 다익스트라 알고리즘에서 소스개선에 사용하였다.

<br/>

![add_priority_queue1](/assets/img/post_img/add_priority_queue1.PNG "add_priority_queue1")

<br/>
<br/>

## 우선순위 큐 구현 방법
= 단순히 리스트를 이용하여 구현
- 힙을 이용하여 구현
- 데이터의 개수가 N개일 때, 구현 방식에 따라서 시간 복잡도를 비교한 내용은 다음과 같다.

![add_priority_queue2](/assets/img/post_img/add_priority_queue2.PNG "add_priority_queue2")
<br/>

- 단순히 N개의 데이터를 힙에 넣었다가 모두 꺼내는 작업은 정렬과 동일, 이경우 시간 복잡도는 O($ NlogN $)이다.


## 힙의 특정
- 힙은 완전 이진 트리 자료구조의 일종
  - 완전 이진 트리란 루트 노드부터 시작하여 왼쪽 자식 노드, 오른쪽 자식 노드 순서대로 데이터가 차례대로 삽입되는 트리
  
  ![complete_binary_tree1](/assets/img/post_img/complete_binary_tree1.PNG "complete_binary_tree1")
  <br/>

- 힙에서는 항상 루트 노드(root node)를 제거
- 최소 힙(min heap)
  - 루트 노드가 가장 작은 값을 가진다.
  - 따라서 값이 작은 데이터가 우선적으로 제거
- 최대 힙(max heap)
  - 루트 노드가 가장 큰 값을 가진다.
  - 따라서 값이 큰 데이터가 우선적으로 제거


- ### 최소 힙을 예로 들어 힙에 데이터를 넣었을때 절차
- (상향식)부모 노드로 거슬러 올라가며, 부모보다 자신의 값이 더 작은 경우 위치를 교체

![min_heapify1](/assets/img/post_img/min_heapify1.PNG "min_heapify1")

<br/>

 - 새로운 원소가 삽입되었을 때 O( $ logN $)의 사간복잡도로 힙 성질을 유지시킽 수 있다.

![min_heapify2](/assets/img/post_img/min_heapify2.PNG "min_heapify2")

<br/>

- 반대로 힙에서 원소가 제거되었을 때 O($ logN $)의 시간 복잡도로 힙 성질을 유지하도록 할 수 있다.

![min_heapify3](/assets/img/post_img/min_heapify3.PNG "min_heapify3")

<br/>

![min_heapify4](/assets/img/post_img/min_heapify4.PNG "min_heapify4")

<br/>


# 트리(Tree)
- 트리는 가계도와 같은 **계층적인 구조**를 표현할 때 사용할 수 있는 자료구조이다
- 힙은 이 트리를 기반으로 구성되어 있다.


![tree1](/assets/img/post_img/tree1.PNG "tree1")

<br/>

# 이진 탐색 트리(Binary Search Tree)
- **이진 탐색**이 동작할 수 있도록 고안된 효율적인 탐색이 가능한 자료구조
- 이진 탐색트리의 특징 : 왼쪽 자식 노드< 부모노드 < 오른쪽 자식 노드
  - 부모 노드보다 왼쪽 자식 노드가 작다.
  - 부모 노드보다 오른쪽 자식 노드가 크다.

## 트리의 탐색방법

![tree2](/assets/img/post_img/tree2.PNG "tree2")

<br/>

![tree3](/assets/img/post_img/tree3.PNG "tree3")

<br/>

![tree4](/assets/img/post_img/tree4.PNG "tree4")

<br/>

## 트리의 순회(Tree Traversal)
- 트리 자료구에 포함된 노드를 특정한 방법으로 한 번씩 방문하는 방법
  - 트리의 정보를 시각적으로 확인 가능
- 대표 트리 순회 방법
  - 전위 순회(pre-order traverse): 루트를 먼저 방문
  - 중위 순회(in-order traverse): 왼쪽 자식을 방문한 뒤에 루트를 방문
  - 후위 순회(post-order traverse):오른쪽 자식을 방문한 뒤에 루트를 방문

![tree5](/assets/img/post_img/tree5.PNG "tree5")

<br/>

# 벨만 포드 알고리즘(Bellman-Ford Algorithm)
- 음수 간선이 포함된 상황에서의 최단 거리 문제

> N개의 도시가 있다. 그리고 한 도시에서 출발하여 다른 도시에 도착하는 버스가 M개 있다. 각 버스는 A,B,C로 나타낼 수 있는데, A는 시작도시, B는 도착도시, C는 버스를 타고 이동하는데 걸리는 시간이다. 시간 C가 양수가 아닌 경우가 있다. C = 0인 경우는 순간 이동을 하는 경우, C<0인 경우는 타임머신으로 시간을 되돌아가는 경우이다. 1번 도시에서 출발해서 나머지 도시로 가는 가장 빠른 시간 프로그램을 작성하시오.

- 도시의 개수 : N(1<=N <= 500)
- 버스 노선의 개수 : M(1 <= M <= 6,000 )

![bellman1](/assets/img/post_img/bellman1.PNG "bellman1")

<br/>

![bellman2](/assets/img/post_img/bellman2.PNG "bellman2")

<br/>

![bellman3](/assets/img/post_img/bellman3.PNG "bellman3")

<br/>

- 음수 간선의 순환이 발생할 경우 벨만포드 알고리즘을 사용할수 있다.

<br/>
<br/>

- 음수 간선에 관하여 최단 경로 문제는 다음과 같이 분류
  - 1)모든 간선이 양수인 경우
  - 2)음수 간선이 있는 경우
    - 1)음수 간선 순환은 없는 경우
    - 2)음수 간선 순환이 있는 경우

- 벨만 포드 최단경로 알고리즘은 **음의 간선이 포함된 상황에서도 사용**
  - 음수 간선의 순환 감지 가능
  - 시간 복잡도는 O(VE)로 다익스트라 알고리즘에 비해 느리다

<br/>
<br/>

### 벨만 포드 알고리즘 동작 원리
1. 출발 노드를 설정
2. 최단 거리 테이블을 초기화
3. 다음의 과정을 N-1번 반복
  1. 전체 간선 E개를 하나씩 확인
  2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신

- 만약 **음수 간선 순환이 발생하는지 체크하려면 3번 과정을 한 번 더 수행**
- 이때 최단 거리 테이블이 갱신된다며 음수 간선 순환 존재

### 다익스트라 알고리즘과의 비교

- 다익스트라 알고리즘
  - 매번 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택
  - 음수 간선이 없다면 최적의 해를 찾을 수 있다.

- 벨만 포드 알고리즘
  - 매번 모든 간선을 전부 확인
    - **다익스트라 알고리즘에서의 최적의 해를 항상 포함**
  - 다익스트라 알고리즘에 비해서 시간이 오래 걸리지만 음수 간선 순환을 탐지








































------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]
