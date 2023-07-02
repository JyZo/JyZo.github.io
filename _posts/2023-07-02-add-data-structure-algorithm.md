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










































------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]
