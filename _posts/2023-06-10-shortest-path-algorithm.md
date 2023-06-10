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

