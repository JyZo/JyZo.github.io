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
하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어

>- 0ms 시점에 3ms가 소요되는 A작업 요청
>- 1ms 시점에 9ms가 소요되는 B작업 요청
>- 2ms 시점에 6ms가 소요되는 C작업 요청

와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.

![heapquest1](/assets/img/post_img/heapquest1.PNG "heapquest1")

<br/>

한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.

![heapquest2](/assets/img/post_img/heapquest1.PNG "heapquest2")

<br/>

>- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
>- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
>- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면

![heapquest3](/assets/img/post_img/heapquest3.PNG "heapquest3")

<br/>

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

### 제한 사항

- jobs의 길이는 1 이상 500 이하입니다.
- jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
- 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
- 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

### 입출력 예

|jobs | return |
|----|----|
[[0, 3], [1, 9], [2, 6]] | 	9

입출력 예 설명
문제에 주어진 예와 같습니다.

- 0ms 시점에 3ms 걸리는 작업 요청이 들어옵니다.
- 1ms 시점에 9ms 걸리는 작업 요청이 들어옵니다.
- 2ms 시점에 6ms 걸리는 작업 요청이 들어옵니다.

```java
class Solution {
    public int solution(int[][] jobs) {
        PriorityQueue<Job> wait = new PriorityQueue<>((o1, o2) -> o1.start - o2.start);
        PriorityQueue<Job> ready = new PriorityQueue<>((o1, o2) -> o1.cost - o2.cost);
        int waitTime = 0;
        int costTime = 0;
        int idle = 0;
        int count = 0;
        
        for (int i = 0; i < jobs.length; i++) {
            wait.add(new Job(jobs[i][0], jobs[i][1]));
        }
        
        while (count < jobs.length) {
            while (!wait.isEmpty() && wait.peek().start <= costTime) {
                ready.offer(wait.poll());
            }
            
            if (ready.isEmpty()) {
                idle += wait.peek().start - costTime;
                costTime = wait.peek().start;
            }
            else {
                Job job = ready.poll();
                waitTime += costTime - job.start;
                costTime += job.cost;
                System.out.println(job.start + " " + job.cost);
                count++;
            }
        }
        
        return (waitTime + costTime - idle) / jobs.length;
    }
    
    class Job {
        int start;
        int cost;
        
        public Job(int start, int cost) {
            this.start = start;
            this.cost = cost;
        }
    }
}
```
- 문제가 아이디어만 놓고 보면 해 볼만 했으나 막상 구현하다보니 문제점들이 보였음
- comparator관련 커스텀이 막상 적용해보려니 생각보다 안되는 부분이 많았고 이부분은 따로 찾아 공부해야할 것 같다
- class로 생성하여 하려던 내 아이디어와 가장 비슷한 아이디어를 채택 소스코드 자체는 심플했다
- 람다식 참조[https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95]

- comparator 참조[https://velog.io/@robolab1902/Java-Priority-Queue-%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EC%97%90-%EB%9E%8C%EB%8B%A4%EC%8B%9D-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0%EA%B0%80-%EB%AD%90%EC%95%BC]



<br/>

# 3. 이중우선순위큐
이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

|명령어 | 수신 탑(높이) |
|----|----|
I  숫자 | 큐에 주어진 숫자를 삽입합니다.|
D 1	 | 큐에서 최댓값을 삭제합니다.|
D -1 | 큐에서 최솟값을 삭제합니다.

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

### 제한사항
- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
- 원소는 “명령어 데이터” 형식으로 주어집니다.
  - 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

### 입출력 예

	
|operations | return |
|----|----|
["I 16", "I -5643", "D -1", "D 1", "D 1", "I 123", "D -1"] | [0,0]
["I -45", "I 653", "D 1", "I -642", "I 45", "I 97", "D 1", "D -1", "I 333"]	 | [333, -45]

입출력 #1
- 16과 -5643을 삽입합니다.
- 최솟값을 삭제합니다. -5643이 삭제되고 16이 남아있습니다.
- 최댓값을 삭제합니다. 16이 삭제되고 이중 우선순위 큐는 비어있습니다.
- 우선순위 큐가 비어있으므로 최댓값 삭제 연산이 무시됩니다.
123을 삽입합니다.
- 최솟값을 삭제합니다. 123이 삭제되고 이중 우선순위 큐는 비어있습니다.

따라서 [0, 0]을 반환합니다.

임출력 #2
- 45와 653을 삽입후 최댓값(653)을 삭제합니다. -45가 남아있습니다.
- 642, 45, 97을 삽입 후 최댓값(97), 최솟값(-642)을 삭제합니다. -45와 45가 남아있습니다. 333을 삽입합니다.

이중 우선순위 큐에 -45, 45, 333이 남아있으므로, [333, -45]를 반환합니다.


```java
import java.util.*;
class Solution {
    public int[] solution(String[] operations) {
        int[] answer = new int[2];
        
        PriorityQueue<Integer> minPQ = new PriorityQueue<>();
        PriorityQueue<Integer> maxPQ = new PriorityQueue<>(Collections.reverseOrder());
        
        for(int i = 0; i<operations.length; i++){
            String[] parse = operations[i].split(" ");
            
            if(minPQ.isEmpty() && parse[0].equals("D")){
                continue;
            }
            
            if(parse[0].equals("I")){
                minPQ.add(Integer.parseInt(parse[1]));
                maxPQ.add(Integer.parseInt(parse[1]));
            }else{
                if(parse[1].equals("-1")){
                    int min = minPQ.poll();
                    maxPQ.remove(min);
                }else{
                    int max = maxPQ.poll();
                    minPQ.remove(max);
                }
            }
        }
        
        if(minPQ.isEmpty() && maxPQ.isEmpty()){
            answer[0] = 0;
            answer[1] = 0;
        }else{
            answer[0] = maxPQ.poll();
            answer[1] = minPQ.poll();
        }
        return answer;
    }
}
```
- 최소와 최대를 우선순위 큐 하나로만 해결하려다가 안되어서 두개를 이용하는 방식을 사용했고 초기 remove 함수의 존재를 잊어 두개를 이용하는데 잠깐 애를 먹었다.

- 답을 찾던 중 Comparator를 사용한 답중 정말 처음 생각해봤던 방향의 코드가 있어 아래에 따로 기재

```java

class Solution {
    public int[] solution(String[] operations) {
        int[] answer = new int[2];

        PriorityQueue<Pair> maxHeap = new PriorityQueue<>(new ComparatorDescending());
        PriorityQueue<Pair> minHeap = new PriorityQueue<>(new ComparatorAscending());
        boolean[] visited = new boolean[operations.length];

        for(int i=0; i<operations.length; i++) {
            String[] operationWord = operations[i].split(" ");
            String op = operationWord[0];
            int n = Integer.parseInt(operationWord[1]);
            Pair p;

            switch(op) {
                case "I":
                    p = new Pair(i, n);
                    maxHeap.add(p);
                    minHeap.add(p);
                    break;
                case "D":
                    if(n == 1) {
                        if(!maxHeap.isEmpty()) {
                            p = maxHeap.peek();
                            if(!visited[p.index]) {
                                maxHeap.poll();
                                visited[p.index] = true;
                            } else {
                                minHeap.poll();
                            }
                        }
                    } else {
                        if(!minHeap.isEmpty()) {
                            p = minHeap.peek();
                            if(!visited[p.index]) {
                                minHeap.poll();
                                visited[p.index] = true;
                            } else {
                                maxHeap.poll();
                            }
                        }
                    }
                    break;
                default:
                    break;
            }
        }

        while(!maxHeap.isEmpty()) {
            if(!visited[maxHeap.peek().index]) {
                break;
            } else {
                maxHeap.poll();
            }
        }

        while(!minHeap.isEmpty()) {
            if(!visited[minHeap.peek().index]) {
                break;
            } else {
                minHeap.poll();
            }
        }

        answer[0] = !maxHeap.isEmpty() ? maxHeap.peek().value : 0;
        answer[1] = !minHeap.isEmpty() ? minHeap.peek().value : 0;

        return answer;
    }
}

class Pair {
    int index;
    int value;

    Pair(int index, int value) {
        this.index = index;
        this.value = value;
    }
}

class ComparatorDescending implements Comparator<Pair> {
    @Override
    public int compare(Pair p1, Pair p2) {
        if(p1.value < p2.value) {
            return 1;
        } else {
            return -1;
        }
    }
}

class ComparatorAscending implements Comparator<Pair> {
    @Override
    public int compare(Pair p1, Pair p2) {
        if(p1.value < p2.value) {
            return -1;
        } else {
            return 1;
        }
    }
}
```

<br/>



-----------------------------------------------------------------
출처 - 2번문제 블로그[[https://easybrother0103.tistory.com/119](https://easybrother0103.tistory.com/119]  