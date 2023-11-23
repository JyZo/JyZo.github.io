---
title: programmers heap
date: 2023-11-22 23:28 +0900
author: JyZo
categories: [Algorithm, Problem solving]
tags: [Algorithm, Problem solving]
math: true
---


# 힙(Heap)

<br/>

# 1. 더 맵게
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

>섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.


### 입출력 예

|scoville | K | return|
|----|----|----|
| [1, 2, 3, 9, 10, 12] |7 | 2 |


### 입출력 예 설명
1.  스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
- 새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
- 가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]

2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
- 새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
- 가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

<br/>

```java
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> PQ = new PriorityQueue<>();
        
        for(int scovilleNum : scoville){
            PQ.add(scovilleNum);
        }
        
        while(PQ.peek()<K){
            if(PQ.size() < 2){
                return -1;
            }
            // System.out.println("first PQ["+PQ.peek()+"]");
            int scovMin = PQ.poll();
            // System.out.println("second PQ["+PQ.peek()+"]");
            PQ.add(scovMin+(PQ.poll()*2));
            answer++;
        }
        
        return answer;
    }
}
```
- 힙이 우선순위 큐를 사용하기위한 자료구조인걸 기억했고 제한 사항의 -1을 리턴하는 걸 놓쳐 시간이 조금 오래걸렸다.
- 우선순위 큐는 기본적으로 자바의 경우 최소힙으로 return
- 최대힙의 경우 Collections.reversOrder() 를 사용해 변경가능
- comparator 인터페이스를 이용해 우선순위를 커스텀 할 수 있다고 한다. 간단 적용은 해보았지만 난이도가 올라가면 더 유용하게 쓸 일이 생길것 같다.

<br/>

# 2. 디스크 컨트롤러
