---
title: etc algorithm
date: 2023-06-29 00:25 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
math: true
---

# 기타 알고리즘
- 그 외 코딩테스트에서 빈도있게 출제되는 알고리즘들을 다뤄보는 마무리챕터


# 소수(Prime Number)
- 소수란 1보다 큰 자연수 중에서 1과 자기 자신을 제외한 자연수로는 나누어떨어지지 않는 자연수
- 코딩 테스트에서는 어떠한 자연수가 소수인지 아닌지 판별해야 하는 문제 출제

```java
public class Practice {
    public static boolean isPrimeNumber(int x){
        for(int i = 2;i<x;i++){
            if(x % i == 0){
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPrimeNumber(4));
        System.out.println(isPrimeNumber(7));
    }
}
```

<br/>

## 기본알고리즘 성능분석
- 2부터 X-1까지의 모든 자연수에 대하여 연산을 수행
- 모든 수를 하나씩 확인한다는 점에서 시간 복잡도는 O(X)이다.
- 다만 약수에 있는 성질로 인해 개선 가능

## 약수의 성질
- **모든 약수가 가운데 약수를 기준으로 곱셈 연산에 대해 대칭**을 이룬다. 
- 따라서 특정한 자연수의 모든 약수를 찾을 때 **가운데 약수(제곱근)까지만 확인** 하면 된다.

![etc_algorithm1](/assets/img/post_img/etc_algorithm1.PNG "etc_algorithm1")

<br/>

```java
for(int i = 2;i<=Math.sqrt(x);i++)
```
- for문의 조건만 제곱근값으로 변경해 주면 된다
- 2부터 X의 제곱근까지 모든 자연수의 연산을 수행해야 한다.
- 시간복잡도는 O($ N^\frac{1}{2} $) 이다.
- 하나의 수에 대해서 판별하는 알고리즘 


## 에라토스테네스의 체

### - 하나의 수에 대해서 소수를 판별하는 것이 아닌 **특정한 범위 안에 존재하는 모든 소수**를 찾는 알고리즘

- 에라토스테네스의 체는 N보다 작거나 같은 모든 소수를 찾을 때 사용
- 에라토스테네스의 체 알고리즘의 동작과정
  - 1.2부터 N까지의 모든 자연수를 나열한다.
  - 2.남은 수 중에서 아직 처리하지 않은 가장 작은 수 i를 찾는다.
  - 3.남은 수 중에서 i의 배수를 모두 제거한다.
  - 4.더 이상 반복할 수 없을 때까지 2번과 3번의 과정을 반복한다.

```java
public class Practice {
    public static int n = 1000;
    public static boolean[] arr = new boolean[n + 1];
    public static void main(String[] args) {
        Arrays.fill(arr, true);
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (arr[i] == true) {
                int j = 2;
                while (i * j <= n) {
                    arr[i * j] = false;
                    j += 1;
                }
            }
        }
        for (int i = 2; i <= n; i++) {
            if (arr[i]) System.out.print(i + " ");
        }
    }
}
```
<br/>

- 에라토스테네스의 체 알고리즘의 시간 복잡도는 선형에 가까울 정도로 빠르다.
- 시간 복잡도는 O($ NloglogN $)이다.
- 다수의 소수를 찾아야 할때 효과적으로 사용되나 각 자연수에 대한 소수 여부를 저장해야 하므로 메모리가 많이 필요

<br/>
<br/>

# 투 포인터(Two Pointers)
- **리스트에 순차적으로 접근해야 할 때 두개의 점의 위치를 기록하면서 처리**하는 알고리즘
- 2,3,4,5,6,7일때 2~7과 비슷한 개념
- 리스트에 담긴 데이터에 순차적으로 접근해야 할 때는 시작점과 끝점 2개의 점으로 접근할 데이터의 범위를 표현


<br/>

![two_pointer1](/assets/img/post_img/two_pointer1.PNG "two_pointer1")

<br/>

![two_pointer2](/assets/img/post_img/two_pointer2.PNG "two_pointer2")

<br/>

```java
public class Practice {
    public static int n = 5; 
    public static int m = 5;
    public static int[] arr = {1, 2, 3, 2, 5}; 

    public static void main(String[] args) {
        int cnt = 0;
        int intervalSum = 0;
        int end = 0;
        
        for (int start = 0; start < n; start++) {
            while (intervalSum < m && end < n) {
                intervalSum += arr[end];
                end += 1;
            }
            if (intervalSum == m) {
                cnt += 1;
            }
            intervalSum -= arr[start];
        }
        System.out.println(cnt);
    }
}
```

<br/>

# 구간 합(Interval Sum)

- 연속적으로 나열된 N개의 수가 있을 때 **특정 구간의 모든 수를 합한 값을 계산**하는 문제

![interval_sum1](/assets/img/post_img/interval_sum1.PNG "interval_sum1")

<br/>

![interval_sum2](/assets/img/post_img/interval_sum2.PNG "interval_sum2")

<br/>

```java
public class Practice {
    public static int n = 5;
    public static int arr[] = {10, 20, 30, 40, 50};
    public static int[] prefixSum = new int[6];
    public static void main(String[] args) {
        int sumValue = 0;
        for (int i = 0; i < n; i++) {
            sumValue += arr[i];
            prefixSum[i + 1] = sumValue;
        }
        
        int left = 3;
        int right = 4;
        System.out.println(prefixSum[right] - prefixSum[left - 1]);
    }
}
```


------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]