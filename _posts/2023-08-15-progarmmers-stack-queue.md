---
title: progarmmers stack/queue
date: 2023-08-15 23:33 +0900
author: JyZo
categories: [Algorithm, Problem solving]
tags: [Algorithm, Problem solving]
math: true
---


# 스택

<br/>

# 1. 같은 숫자는 싫어

배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

- arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
- arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
- 배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

### 제한사항

- 배열 arr의 크기 : 1,000,000 이하의 자연수
- 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수


```java
public class Solution {
    public int[] solution(int []arr) {
        Stack<Integer> stack = new Stack<>();

        stack.push(arr[0]);
        for(int i = 1; i< arr.length; i++){
            if(arr[i] == stack.peek()){
                continue;
            }
            stack.push(arr[i]);
        }

        int stackcount = stack.size()-1;
        int[] answer = new int[stack.size()];
        while (!stack.empty()){
            answer[stackcount] = stack.pop();
            stackcount--;
        }
        return answer;
    }
}
```

>문제를 보다보니 스택을 꼭 사용해야하나?라는 생각은 했는데 스택 첫문제기도 하고 스택을 사용해서 풀고 풀이들을 봤더니 대다수가 그냥 리스트로 풀어버려서 허탈했다....아이디어는 맞았으니 뭐...

<br/>

# 2. 기능 개발

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

### 제한사항
- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

```java

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int[] answer = {};
        Queue<Integer> queue = new LinkedList<>();
        ArrayList<Integer> finResult = new ArrayList<>();
        Queue<Integer> finQueue = new LinkedList<>();
        int firstCount = 0;
        int secondCount = 0;
        
        for(int progresse : progresses){
            queue.offer(progresse);
        }
        
        for(int i = 0;i<progresses.length;i++){
            int peekVal = queue.peek();
            firstCount = 0;
            System.out.println("peekVal["+peekVal+"]");
            while(peekVal<100){
                peekVal+=speeds[i];
                firstCount++;
            }
            System.out.println("firstCount["+firstCount+"]");
            finQueue.add(firstCount);
            queue.poll();
        }

        // Iterator iter1 = result.iterator();
        // while(iter1.hasNext()){
        //     System.out.print(iter1.next() + " ");
        // }
        // System.out.println("\n");

        // int chk = finQueue.peek();
        // int finCount = 0;
        // System.out.println("first chk["+chk+"]");
        
//         while (!finQueue.isEmpty()){
//             System.out.println("chk["+chk+"]");
//             System.out.println("peek["+finQueue.peek()+"]");
//             if(chk>=finQueue.peek()){
//                 finCount++;
//                 System.out.println("finCount1["+finCount+"]");
//                 finQueue.poll();
//                 // continue;
//                 if(chk < finQueue.peek()){
//                     finResult.add(finCount);
//                     chk = finQueue.peek();
//                     finCount = 1;
//                 }
                
//             }else{
//                 finCount++;
//                 System.out.println("finCount2["+finCount+"]");
//                 chk = finQueue.poll();
//                 // finQueue.poll();
//                 finResult.add(finCount);
//                 finCount = 1;
//             }
//         }
        int x = q.poll();
        int count = 1;
        while (!q.isEmpty()) {
            if (x >= q.peek()) {
                count++;
                q.poll();
            } else {
                list.add(count);
                count = 1;
                x = q.poll();
            }
        }
        list.add(count);

        

        Iterator iter = finResult.iterator();
        while(iter.hasNext()){
            System.out.print(iter.next() + " ");
        }
        return finResult.stream().mapToInt(Integer::intValue).toArray();
    }
}
```
>정말 마지막 단계에서 조금 부족해서 정답을 깔끔히 맞추지 못했다. 풀릴듯 말듯 고민을 오래해 흔적을 남기고자 주석은 남겨본다.....ㅠ  
>내가 생각했던 부분에서 빠진부분을 채워넣은걸 정답으로 채택했으며 개인적으로 마지막 부분은 다른분의 풀이인

```java
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> queue = new LinkedList<>();
        for(int i=0; i<progresses.length; i++){
            queue.add((int) (Math.ceil((100.0 - progresses[i]) / speeds[i])));
        }
        
        List<Integer> answer = new ArrayList<>();
        while (!queue.isEmpty()){
            int day = queue.poll();
            int cnt = 1;
            
            while(!queue.isEmpty() && day >= queue.peek()){
                cnt++;
                queue.poll();
            }
            answer.add(cnt);
        }
        
        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```
> 이렇게 처리한게 굉장히 깔끔하고 본받고 싶다고 느꼈다. 
> 못풀었던 가장 중요한 이유는 마지막 개수 분별 할 로직 아이디어를 제대로 생각하지 못한것!

<br/>

# 3. 올바른 괄호

괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

- "()()" 또는 "(())()" 는 올바른 괄호입니다.
- ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.  

'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

### 제한사항
- 문자열 s의 길이 : 100,000 이하의 자연수
- 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

```java
import java.util.*;
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        Stack<Character> stack = new Stack<>();
        
        for(char item : s.toCharArray()){
            if(item == '('){
                stack.push('(');
            }
            else{
                if(!stack.isEmpty()){
                    stack.pop();
                }
                else {
                    return false;
                }
            }
        }

        return stack.isEmpty()?true : false;
    }
}
```
위 문제의 경우 순서에 따른 괄호의 짝을 정확히 맞출 방법을 생각하지 못하여 풀지 못하였고 여러 풀이를 보던 중 가장 깔끔하여 채탱하였다.

<br/>

# 4. 프로세스

운영체제의 역할 중 하나는 컴퓨터 시스템의 자원을 효율적으로 관리하는 것입니다. 이 문제에서는 운영체제가 다음 규칙에 따라 프로세스를 관리할 경우 특정 프로세스가 몇 번째로 실행되는지 알아내면 됩니다.

1. 실행 대기 큐(Queue)에서 대기중인 프로세스 하나를 꺼냅니다.
2. 큐에 대기중인 프로세스 중 우선순위가 더 높은 프로세스가 있다면 방금 꺼낸 프로세스를 다시 큐에 넣습니다.
3. 만약 그런 프로세스가 없다면 방금 꺼낸 프로세스를 실행합니다.
  3.1 한 번 실행한 프로세스는 다시 큐에 넣지 않고 그대로 종료됩니다.
예를 들어 프로세스 4개 [A, B, C, D]가 순서대로 실행 대기 큐에 들어있고, 우선순위가 [2, 1, 3, 2]라면 [C, D, A, B] 순으로 실행하게 됩니다.

현재 실행 대기 큐(Queue)에 있는 프로세스의 중요도가 순서대로 담긴 배열 priorities와, 몇 번째로 실행되는지 알고싶은 프로세스의 위치를 알려주는 location이 매개변수로 주어질 때, 해당 프로세스가 몇 번째로 실행되는지 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- priorities의 길이는 1 이상 100 이하입니다.
    - priorities의 원소는 1 이상 9 이하의 정수입니다.
    - priorities의 원소는 우선순위를 나타내며 숫자가 클 수록 우선순위가 높습니다.
- location은 0 이상 (대기 큐에 있는 프로세스 수 - 1) 이하의 값을 가집니다.
    - priorities의 가장 앞에 있으면 0, 두 번째에 있으면 1 … 과 같이 표현합니다.

```java
import java.util.*;
class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
		
		for(int num : priorities) {
			pq.add(num);
		}
		while(!pq.isEmpty()) {
			for(int i=0; i<priorities.length; i++) {
				if(priorities[i] == pq.peek()) {
					pq.poll();
					answer++;
					if(i == location)
						return answer;
				}
			}
		}  
        return answer;
    }
}
```
문제를 풀면서 순서를 어떻게 하지 하며 방법들을 써봐도 뜻대로 안 되어서 찾아보니 이론 수업을 할 때 우선순위 큐라는 것이 존재하는 것을 너무 가볍게 봤는지 까맣게 잊고 있었다......

최근 전적이 조금 좋지 않아서 아쉬워지고 있다

<br/>

# 5. 다리를 지나는 트럭
트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다.

예를 들어, 트럭 2대가 올라갈 수 있고 무게를 10kg까지 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.


|경과 시간|다리를 지난 트럭|다리를 건너는 트럭|대기 트럭|  
|----|----|----|----|
|0|[]|[]|[7,4,5,6]|
|1~2|[]|[7]|[4,5,6]|
|3|[7]|[4]|[5,6]|
|4|[7]|[4,5]|[6]|
|5|[7,4]|[5]|[6]|
|6~7|[7,4,5]|[6]|[]|
|8|[7,4,5,6]|[]|[]|

<br/>
따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

### 제한사항
- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

<br/>

```java
import java.util.*;
class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        Queue<Integer> bridge_q = new LinkedList<>();
        int time = 0;
        int sum = 0;
        
        for(int i = 0;i<truck_weights.length;i++){
            int temp_truck = truck_weights[i];
            while(true){
                if(i == 0){
                bridge_q.offer(temp_truck);
                sum+=temp_truck;
                time++;
                break;
            }else if(bridge_length == bridge_q.size()){
                sum-=bridge_q.poll();
            }else{
                if(weight>=sum+temp_truck){
                    bridge_q.offer(temp_truck);
                    sum+=temp_truck;
                    time++;
                    break;
                }else{
                    bridge_q.offer(0);
                    time++;
                }
            }
          } 
        }
        return time+bridge_length;
    }
}
```

- 문제를 풀다 시간 좀 쓰고 넘어가야지 해도 자꾸 조금만 더하면 될거 같아 투자하는 시간이 너무 길어져서 빨리 구해지지 않을 경우 칼같이 넘어가는 쪽으로 방향을 전환했다.
- 이 문제에서 가장 큰 도움이 된 아이디어는 큐에 0을 넣어서 흐름을 만들어내지 못한것

--------------------------------------------

출처 - 2번문제 블로그[[https://velog.io/@kimmjieun/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EA%B8%B0%EB%8A%A5%EA%B0%9C%EB%B0%9C](https://velog.io/@kimmjieun/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EA%B8%B0%EB%8A%A5%EA%B0%9C%EB%B0%9C)]  

출처 - 2번문제 블로그[[https://haruple.tistory.com/205](https://haruple.tistory.com/205]  

출처 - 3번문제 블로그[[https://hy-ung.tistory.com/100](https://hy-ung.tistory.com/100]  

출처 - 5번문제 블로그[[https://minhamina.tistory.com/241](https://minhamina.tistory.com/241]  
