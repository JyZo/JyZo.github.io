---
title: Dynamic programming
date: 2023-05-30 23:26 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---


# 다이나믹 프로그래밍(Dynamic Programming)

## **메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 법!!**


- 이미 계산된 결과는 별도의 메모리 영역에 저장하여 다시 계산하지 않음
- 일반적으로 탑다운, 바텀업 두가지 방식으로 구성되며 전형적인 방식은 바텀업이다.
- 동적 계획법이라고도 불리며 자료구조에서 동적 할당은 **프로그램이 실행되는 도중에 필요한 메모리를 할당하는 기법**을 의미
- 하지만 패턴으로서 다이나믹 프로그램의 다이나믹은 별 의미없이 사용


## 다이나믹 프로그래밍은 두가지 조건을 만족할 때 사용
1. 최적 부분 구조(Optimal Substructure)
    - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결

2. 중복되는 부분 문제(Overlapping Subproblem)
    - 동일한 작은 문제를 반복적으로 해결

<br/>
<br/>

# 피보나치 수열
- 다이나믹 프로그래밍을 이용하기 좋은 예시로서 위의 두 가지 조건을 모두 만족한다. 

피보나치 수열은 다음과 같은 형태의 수열이며  
>1,1,2,3,5,8,13,21,34,55..........

점화식으로 표현하자면 
> $ a_n$ = $a_{n-1}$ + $a_{n-2} $
이 된다.

![fibo1](/assets/img/post_img/fibo1.PNG "fibo1")


1. 최초의 큰 문제인 f(6)에서 작은 문제들로 나뉘어 진다.
2. f(2)라는 동일한 작은 문제가 반복적으로 나타난다.

<br/>
<br/>

# 메모이제이션(Memoization)
- __한 번 계산한 결과를 메모리 공간에 메모하는 기법__
    - 같은 문제를 다시 호출하면 메모했던 결과를 가져온다
    - 값을 기록해 놓는다는 점에서 캐싱(Caching) 이라고도 한다. 
- 탑다운,바텀업 두가지 방식중에서 탑다운에 속한다.

<br/>
<br/>

# 탑다운 vs 바텀업
- 코드로 보면 직관적으로 잘 구분된다.

>탑다운
```java
public class Practice {
    public static long[] d = new long[100];
    public static long fibo(int x) {
        if (x == 1 || x == 2) {
            return 1;
        }
        if (d[x] != 0) {
            return d[x];
        }
        d[x] = fibo(x - 1) + fibo(x - 2);
        return d[x];
    }
    public static void main(String[] args) {
        System.out.println(fibo(50));
    }
}
```

>바텀업
```java
public class Practice {
    public static long[] d = new long[100];
    public static void main(String[] args) {
        d[1] = 1;
        d[2] = 1;
        int n = 50; 
        
        for (int i = 3; i <= n; i++) {
            d[i] = d[i - 1] + d[i - 2];
        }
        System.out.println(d[n]);
    }
}
```

![memoization](/assets/img/post_img/memoization.PNG "memoization")

여기서 얼마전 배웠던 퀵정렬과 비교점도 비교해 보고자 한다. 생각해보니 퀵 정렬 또한 pivot을 두고 비교 한 뒤 나누는 것을 반복한다. 이 부분까지는 동적 프로그래밍 1번 조건을 만족하나.....애석하게도

![def_quick](/assets/img/post_img/def_quick.PNG "def_quick")

분할을 완료하고 2번조건인 중복되는 부분문제를 호출하지 않는다는 큰 차이점이 존재해버린다.  
분할 정복은 퀵정렬 외에도 병합정렬등도 존재한다. 

<br/>
<br/>

# 다이나믹 프로그래밍 접근 방법
- 주어진 문제가 다이나믹 유형임을 파악하는 것이 중요
- 가장 먼저 그리디, 구현, 완전탐색등으로 해결 시도
    - 다른 풀이 방법이 떠오르지 않으면 다이나믹 고려
- 일단 재귀함수로 완전탐색 프로그램을 작성 후 작은 문제 값이 그대로 사용될 수 있으면 개선 시도


<br/>
<br/>



# 다이나믹 프로그래밍 문제 1 - 개미전사
>개미 전사는 부족한 식량을 충당하고자 메뚜기 마을의 식량창고를 공격하려고 합니다. 메뚜기 마을에는 여러 개의 식량창고가 있는데 식량창고는 일직선으로 이어져 있습니다.  
각 식량창고에는 정해진 수의 식량을 저장하고 있으며 개미 전사는 식량창고를 선택적으로 약탈하여 식량을 빼앗을 예정입니다. 이때 메뚜기 정찰병들은 일직선상에 존재하는 식량창고 중에서 서로 인접한 식량창고가 공격받으면 바로 알아챌 수 있습니다.  
따라서 개미 전사가 정찰병에게 들키지 않고 식량창고를 약탈하기 위해서는 최소한 한 칸 이상 떨어진 식량창고를 약탈해야 합니다.


#

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]