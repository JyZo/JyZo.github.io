---
layout: post
title: programmers-sort
date: 2023-11-27 23:34 +0900
author: JyZo
categories: [Algorithm, Problem solving]
tags: [Algorithm, Problem solving]
math: true
---

# 1. K번째 수

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

### 입출력 예

|array | commands | return|
|----|----|----|
[1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

### 입출력 예 설명
- [1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
- [1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
- [1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.


```java
import java.util.*;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        ArrayList<Integer> arr = new ArrayList<Integer>();
        
        for(int a = 0; a<commands.length; a++){
            int start = commands[a][0];
            int end = commands[a][1];
            int from = commands[a][2];
            
            for(int i = start-1; i< end; i++){
                arr.add(array[i]);    
            }
            
            Collections.sort(arr);
            
            answer[a] = arr.get(from-1);
            arr.clear();
        }
        return answer;
    }
}
```
- 정렬 메소드를 활용해서 푸는건 어렵지 않았다.
- 다른사람 풀이를 보니 copyOfRange라는걸 써서 더 깔끔하게 푼게 있는데 이부분도 학습해봐야지

<br/>

# 2. 가장 큰 수
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.


### 입출력 예

|numbers | return | 
|----|----|
[6, 10, 2] | "6210" |
[3, 30, 34, 5, 9] | "9534330" |


```java
import java.util.*;
public class Solution {
    public String solution(int[] numbers) {
        String[] strnum = new String[numbers.length];

        for (int i = 0; i < strnum.length; i++) {
            strnum[i] = String.valueOf(numbers[i]);
        }

        Arrays.sort(strnum, new Comparator<String>(){
            @Override
            public int compare(String num1,String num2){
                return (num2+num1).compareTo(num1+num2);
            }
        });
        
        if (strnum[0].equals("0")) {
           return "0";
        }
        
        StringBuilder answer = new StringBuilder();
        for (int i = 0; i < strnum.length; i++) {
            answer.append(strnum[i]);
        }
        
        return answer.toString();
    }
}
```
- Arrays.sort를 사용해 정렬할 생각은 해 보았으나 comparator를 여기서도 적용가능할 생각을 못했고 처음엔 그냥 String 을 +=했으나 StringBuilder도 참고해 사용해보니 속도차가 꽤 나서 문자열은 순수 String은 덜 쓰는게 좋겠다.
- 문제를 풀며 comparator선언 방식 외에 IDE없이 치려고하니 간결한 람다식 이해도도 더 늘여야겠다.

<br/>

# 3. H-Index
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

### 입출력 예
|citations | return | 
|----|----|
[3, 0, 6, 1, 5] | 3

# 입출력 예 설명
이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

```java
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        
        Arrays.sort(citations);
		
		for(int i = 0; i < citations.length; i++) {
			int h = citations.length - i; 
			
			if(citations[i] >= h) {
				answer = h;
				break;
			}
		}
        
        return answer;
    }
}
```
- 이 문제는 최초 h-index가 무엇인지 이해가 어려웠지만 개념을 찾아낸후 내림차순으로 하던 중 단 하나의 테스트 케이스가 통과하지 못해 아쉬웠다
- 다른사람들을 참고한 결과 내림차순을 사용한 경우는 못 보았고 h-index설명 이해가 부족했던것 같다.


<br/>


-----------------------------------------------------------------
출처 - 2번문제 블로그[[https://bada744.tistory.com/93](https://bada744.tistory.com/93]  

출처 - 3번문제 블로그[[https://bada744.tistory.com/94](https://bada744.tistory.com/94]  
