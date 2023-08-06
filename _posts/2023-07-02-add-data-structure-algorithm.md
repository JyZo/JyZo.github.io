---
title: add data structure & algorithm
date: 2023-07-02 22:51 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
math: true
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


# 바이너리 인덱스 트리(Binary Indexed Tree,BIT,펜윅 트리)
- 데이터 업데이트가 가능한 상황에서의 구간 합
- 2진법 인덱스 구조를 활용해 구간 합 문제를 효과적으로 해결해 줄 수 있는 자료구조, 펜윅트리라고도 불린다.

![BIT1](/assets/img/post_img/BIT1.PNG "BIT1")

<br/>

- 0이 아닌 마지막 비트를 찾는 방법
  - 특정한 숫자 K의 0이 아닌 마지막 비트를 찾기위해서 K AND -K 연산을 하면 된다.

![BIT2](/assets/img/post_img/BIT2.PNG "BIT2")

<br/>

> 어떤 N개의 수가 주어져 있다. 그런데 중간에 수의 변경이 빈번히 일어나고 그 중간에 어떤 부분의 합을 구하려 한다. 만약에 1,2,3,4,5라는 수가 있고, 3번째 수를 6으로 바꾸고 2번째부터 5번째까지 합을 구하라고 한다면 17을 출력하면 되는 것이다. 그리고 그 상태에서 다섯번째 수를 2로 바꾸고 3번째부터 5번째까지 합을 구하라고 한다면 12가 될 것이다.

- 데이터 개수 : N ( 1 <= N <= 1,000,000)
- 데이터 변경 횟수 : M(1 <= M <= 10,000)
- 구간 합 계산 횟수 : K(1 <= K <= 10,000)

## 바이너리 인덱스 트리 : 트리 구조 만들기
- 트리 구조 만들기 : 0이 아닌 마지막 비트 = 내가 저장하고 있는 값들의 개수

![BIT3](/assets/img/post_img/BIT3.PNG "BIT3")

<br/>

- 특정 값을 변경할 때 : 0이 아닌 마지막 비트만큼 더하면서 구간들의 값을 변경 (예시 = 3rd)

![BIT4](/assets/img/post_img/BIT4.PNG "BIT4")

<br/>

- 1부터 N까지의 합(누적 합) 구하기 : 0이 아닌 마지막 비트만큼 빼면서 구간들의 합 계산(예시 = 11rd)

![BIT5](/assets/img/post_img/BIT5.PNG "BIT5")

<br/>
<br/>

# 최소 공통 조상(Lowest Common Ancestor)
- 두 노드의 공통된 조상 중에서 가장 가까운 조상을 찾는 문제

![LCA1](/assets/img/post_img/LCA1.PNG "LCA1")

<br/>

> N(2 <= N <= 50,000) 개의 정점으로 이루어진 트리가 주어진다. 트리의 각 정점은 1번부터 N번까지 번호가 매겨져 있으며, 루트는 1번이다. 두 노드의 쌍 M(1 <= M <= 10,000)개가 주어졌을 때, 두 노드의 가장 가까운 공통 조상이 몇번인지 출력한다.

## 최소 공통 조상 찾기 알고리즘
1. 모든 노드에 대한 깊이(depth)를 계산합니다.
2. 최소 공통 소장을 찾을 두 노드를 확인합니다.
  1. 먼저 두 노드의 깊이가 동일하도록 거슬러 올라갑니다.
  2. 이후에 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라갑니다.
3. 모든 LCA(a,b)연산에 대하여 2번의 과정을 ㅏㄴ복합니다.

![LCA2](/assets/img/post_img/LCA2.PNG "LCA2")

<br/>

![LCA3](/assets/img/post_img/LCA3.PNG "LCA3")

<br/>

![LCA4](/assets/img/post_img/LCA4.PNG "LCA4")

<br/>

![LCA5](/assets/img/post_img/LCA5.PNG "LCA5")

<br/>

![LCA6](/assets/img/post_img/LCA6.PNG "LCA6")

<br/>

- 매 쿼리마다 부모 방향으로 거슬러 올라가기 위해 최악의 경우 O(N)의 시간 복잡도가 요구
  - 따라서 모든 쿼리를 처리할 때의 시간 복잡도는 O(NM)

## 알고리즘 개선
- 최소 공통 조상위의 문제에서 정점의 범위를 확장할 경우 시간초과 판정을 받기에 개선이 필요하다.
- 2의 제곱 형태로 거슬러 올라가도록 하면 O($ logN $)의 시간 복잡도를 보장
- 메모리를 조금 더 사용하여 각 노드에 대하여 $ 2^i $ 번째 부모에 대한 정보 기록

![LCA7](/assets/img/post_img/LCA7.PNG "LCA7")

<br/>

![LCA8](/assets/img/post_img/LCA8.PNG "LCA8")

<br/>

![LCA9](/assets/img/post_img/LCA9.PNG "LCA9")

<br/>

![LCA10](/assets/img/post_img/LCA10.PNG "LCA10")

<br/>

- 다이나믹 프로그래밍을 이용해 시간 복잡도 개선, 세그먼트 트리라는 것도 이용가능
- 매 쿼리마다 부모를 거슬러 올라가기 위해 O($ logN $)
 - 따라서 모든 쿼리를 처리할 때의 시간 복잡도는 O($ MlogN $)




# FIN
> 생각보다 오래 걸렸고 정말 공부를 쉬었음이 느껴진다. 머리가 너무 안 돌아간다. 1번만에 모든걸 알 수 있으리란 생각은 하지 않았지만 중간에 지쳐 쉬는 구간도 있고 이해를 명확하게 하지 않은 부분도 있었기에 한 번 빠르게 복습하고 난 뒤 문제 풀이를 하며 숙련도를 키워야겠다. 






------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]
