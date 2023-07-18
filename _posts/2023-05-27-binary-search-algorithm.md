---
title: binary search algorithm
date: 2023-05-27 18:20 +0900
author: JyZo
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---

# 이진 탐색 알고리즘(Binery Search Algorithm)

일반적으로 사람들에게 더 친숙한 순차 탐색(데이터를 앞에서부터 하나씩 확인) 하는 방법에 비해 상당히 이질적인 방법으로 탐색한다.  
이진탐색은 크게 두가지 포인트가 눈에 띈다.

**1.정렬되어 있는 리스트에서 탐색한다.**
---

**2.탐색범위를 절반씩 좁혀가며 데이터를 탐색한다**
---

- 이진 탐색은 시작점,끝점,중간점을 이용하여 탐색범위를 설정한다. 

![binary_search1](/assets/img/post_img/binary_search1.PNG "binary_search1")

![binary_search2](/assets/img/post_img/binary_search2.PNG "binary_search2")

![binary_search3](/assets/img/post_img/binary_search3.PNG "binary_search3")

```java
public class Practice {
    public static void main(String[] args) {
        int n, target;

        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        target = sc.nextInt();

        int[] arr = new int[n];
        for(int i = 0; i<n;i++){
            arr[i] = sc.nextInt();
        }

        int result = binarySearch(arr, target, 0, n-1);
        if(result == -1){
            System.out.println("no target");
        }else{
            System.out.println(arr[result]);
        }

    }
    public static int binarySearch(int[] arr, int target, int start, int end){

        while(start <= end){
            int mid = (start + end)/2;
            if(arr[mid] == target) return mid;
            else if(arr[mid] > target) end = mid -1;
            else start = mid +1;
        }
        return -1;
    }
}
```
<br/>



이진탐색 시간복잡도
---

- 연산횟수는 $ log_2 N $에 비례한다.
- 시간 복잡도는 O( $ logN$ ) 을 보장한다. 

파라메트릭 서치
-----

- 최적화 문제를 결정 문제(yes or no) 로 바꾸어 해결하는 기법
- 특정한 조건을 만족하는 가장 알맞은 값을 빠르게 찾는 최적화 문제
- 일반적으로 코딩 테스트에서 파라메트릭 서치 문제는 이진 탐색을 이용하여 해결
- 탐색 문제에서 문제의 범위가 몇억처럼 높을 경우 이진탐색 문제일 확률이 높음

<br/>
<br/>


# 이진탐색 문제1 - 떡볶이 떡 만들기
> 오늘 동빈이는 여행 가신 부모님을 대신해서 떡집 일을 하기로 했습니다. 오늘은 떡볶이 떡을 만드는 날입니다. 동빈이네 떡볶이 떡은 재밌게도 떡볶이 떡의 길이가 일정하지 않습니다. 대신에 한 봉지 안에 들어가는 떡의 총 길이는 절단기로 잘라서 맞춰줍니다.
절단기에 높이(H)를 지정하면 줄지어진 떡을 한 번에 절단합니다. 높이가 H 보다 긴 떡은 H 위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않습니다. 손님이 왔을 때 요청한 총 길이가 M일때 적어도 M 만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하세요.

```java
public class Practice {
    public static void main(String[] args) {
        int N,M;

        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        M = sc.nextInt();

        int[] arr = new int[N];
        int max = 0;
        for(int i = 0; i<N;i++){
            arr[i] = sc.nextInt();
            if(max <= arr[i]){
                max = arr[i];
            }
        }
        int totalResult = 0;
        int start = 0;
        int end = max;

        while(start <= end){
            long total = 0;
            int mid = (start + end)/2;

            for(int i = 0;i<N;i++){
                if(arr[i] > mid) total += arr[i] - mid;
            }
            if(total < M){
                end = mid - 1;
            }else{
                totalResult = mid;
                start = mid+1;
            }
        }
        System.out.println(totalResult);
    }
}
```

이번문제는 또 많이 어려웠다. 제한시간안에 풀이를 못봐서 참고를 하다 특이한 것을 발견했다. 난 최대값을 따로 구했는데  
```java
int end = (int) 1e9;  
```
이런 식으로 지수 표기법으로 10억을 애초에 입력하고 답을 구하셨는데 이렇게 한 이유를 아직은 잘 모르겠다. 
하다보니 문제를 많이 풀면서 깊게 이해해야할 유형들이 더 보이는것같다.

<br/>
<br/>


--------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]