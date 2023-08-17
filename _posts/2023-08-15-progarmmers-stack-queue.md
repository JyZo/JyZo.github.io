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

```



--------------------------------------------

출처 - 2번문제 블로그[[https://velog.io/@kimmjieun/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EA%B8%B0%EB%8A%A5%EA%B0%9C%EB%B0%9C](https://velog.io/@kimmjieun/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EA%B8%B0%EB%8A%A5%EA%B0%9C%EB%B0%9C)]  

출처 - 2번문제 블로그[[https://haruple.tistory.com/205](https://haruple.tistory.com/205]  