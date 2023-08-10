---
title: programmers hash
date: 2023-08-10 01:01 +0900
author: JyZo
categories: [Algorithm, Problem solving]
tags: [Algorithm, Problem solving]
math: true
---


# 해시(Hash)

<br/>

# 1. 폰켓몬

 당신은 폰켓몬을 잡기 위한 오랜 여행 끝에, 홍 박사님의 연구실에 도착했습니다. 홍 박사님은 당신에게 자신의 연구실에 있는 총 N 마리의 폰켓몬 중에서 N/2마리를 가져가도 좋다고 했습니다.

홍 박사님 연구실의 폰켓몬은 종류에 따라 번호를 붙여 구분합니다. 따라서 같은 종류의 폰켓몬은 같은 번호를 가지고 있습니다. 예를 들어 연구실에 총 4마리의 폰켓몬이 있고, 각 폰켓몬의 종류 번호가 [3번, 1번, 2번, 3번]이라면 이는 3번 폰켓몬 두 마리, 1번 폰켓몬 한 마리, 2번 폰켓몬 한 마리가 있음을 나타냅니다. 이때, 4마리의 폰켓몬 중 2마리를 고르는 방법은 다음과 같이 6가지가 있습니다.

- 첫 번째(3번), 두 번째(1번) 폰켓몬을 선택
- 첫 번째(3번), 세 번째(2번) 폰켓몬을 선택
- 첫 번째(3번), 네 번째(3번) 폰켓몬을 선택
- 두 번째(1번), 세 번째(2번) 폰켓몬을 선택
- 두 번째(1번), 네 번째(3번) 폰켓몬을 선택
- 세 번째(2번), 네 번째(3번) 폰켓몬을 선택  

이때, 첫 번째(3번) 폰켓몬과 네 번째(3번) 폰켓몬을 선택하는 방법은 한 종류(3번 폰켓몬 두 마리)의 폰켓몬만 가질 수 있지만, 다른 방법들은 모두 두 종류의 폰켓몬을 가질 수 있습니다. 따라서 위 예시에서 가질 수 있는 폰켓몬 종류 수의 최댓값은 2가 됩니다.
당신은 최대한 다양한 종류의 폰켓몬을 가지길 원하기 때문에, 최대한 많은 종류의 폰켓몬을 포함해서 N/2마리를 선택하려 합니다. N마리 폰켓몬의 종류 번호가 담긴 배열 nums가 매개변수로 주어질 때, N/2마리의 폰켓몬을 선택하는 방법 중, 가장 많은 종류의 폰켓몬을 선택하는 방법을 찾아, 그때의 폰켓몬 종류 번호의 개수를 return 하도록 solution 함수를 완성해주세요.  

### 제한사항
- nums는 폰켓몬의 종류 번호가 담긴 1차원 배열입니다.
- nums의 길이(N)는 1 이상 10,000 이하의 자연수이며, 항상 짝수로 주어집니다.
- 폰켓몬의 종류 번호는 1 이상 200,000 이하의 자연수로 나타냅니다.
- 가장 많은 종류의 폰켓몬을 선택하는 방법이 여러 가지인 경우에도, 선택할 수 있는 폰켓몬 종류 개수의 최댓값 하나만 return 하면 됩니다.

----

>프로그래머스 문제는 정말 오랜만인데 자동완성이 안되어 당황했다. 아이디어 자체는 우선 배열안에 있는 폰켓몬을 정렬시키면 종류별로 우선 분류가 될 거라 판단하여 정렬부터 하였고...

```java
import java.util.Arrays;
class Solution {
    public int solution(int[] nums) {
        int answer = 0;
        int length = nums.length/2;
        
        Arrays.sort(nums);
        nums = Arrays.stream(nums).distinct().toArray();
        
        for(int i = 0; i<length ; i++){
            if(i<nums.length){
                answer++;
            }  
        }
        return answer;
    }
}
```
> 중복제거를 하고 수를 세면 될거라 생각하여 아이디어는 도출했는데, 중복제거 방법은 찾아보았고 테스트 결과 정답은 통과하였다.


<br/>

# 2. 완주하지 못한 선수

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한사항

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

-----
>왜 이문제만 풀려있었는지 모르겠다만 예전에 풀었던 문제고 1번문제를 풀며 기억나 복습한셈 쳤다. 

```java
import java.util.Arrays;
class Solution {
    public String solution(String[] participant, String[] completion) {
        int i; 

        Arrays.sort(participant); 
        Arrays.sort(completion); 

        
        for (i = 0; i < completion.length; i++) {
            if (!participant[i].equals(completion[i])) {
                return participant[i];
            }
        }
        return participant[i]; 
    }
}
```
> 오히려 1번문제보다 쉬운 느낌이었다만 복습이라 그런거 같기도 하고.....

<br/>


# 3. 전화번호 목록

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421  

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

### 제한 사항

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
    - 각 전화번호의 길이는 1 이상 20 이하입니다.
    - 같은 전화번호가 중복해서 들어있지 않습니다.

```java
import java.util.Arrays;
class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        
        Arrays.sort(phone_book);
        
        for(int i = 0;i<phone_book.length-1;i++){
            if(phone_book[i+1].startsWith(phone_book[i])){
                answer = false;
            }
        }
        return answer;
    }
}
```
> 로직 자체는 문제 없는듯 보였으나 효율적이지 못한 코드로 테스트에서 걸리며 실패를 많이 했고 참고하였다....공간복잡도를 실제로 따지는게 생각보다 어렵다
그리고 문제가 해시인데 배열로만 너무 푸는것 같아 다른 방법도 찾아봐야할듯하다

- str1.startsWith(str) - str로 str1이 시작되는지 확인, 존재는 알았지만 막상 문제 풀 때 떠올리지 못함

<br/>
