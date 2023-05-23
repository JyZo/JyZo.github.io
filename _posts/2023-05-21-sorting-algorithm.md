---
title: sorting algorithm
date: 2023-05-21 21:29 +0900
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---


# 정렬 알고리즘

**정렬이란 데이터를 특정한 기준에 따라 순서대로 나열하는 것!!**
-----------------
<br/>
- 일반적으로 문제 상황에 따라 공식처럼 사용 = 이해는 하되 외울 부분은 외워야 한다.

<br/>

# 선택 정렬(Selection Sort)
- 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복

```java
public class Practice {
    public static void main(String[] args) {
        int n = 10;
        int [] arr = {7,5,9,0,3,1,6,2,4,8};

        for(int i = 0; i<n; i++){
            int min_index = i;
            for(int j = i+1; j<n; j++){
                if(arr[min_index] > arr[j]){
                    min_index = j;
                }
            }
            int temp = arr[i];
            arr[i] = arr[min_index];
            arr[min_index] = temp;
        }

        for(int i = 0;i<n;i++){
            System.out.print(arr[i]+" ");
        }
    }
}
```

#

선택정렬의 시간 복잡도 
----
- N번만큼 가장 작은 수를 찾아서 맨 앞으로 보낸다. 
- 구현 방식에 따라서 오차는 있을 수 있지만 N + (N - 1) + (N - 2) + ...+2
- (N<sup>2</sup> + N - 2)/2 로 표현할 수 있으므로 빅오표기법으로 O(N<sup>3</sup>)

<br/>
<br/>

# 삽입정렬(insertion sorting)
- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입
- 선택 정렬에 비해 구현난이도가 높지만, 일반적으로 효율적으로 동작

```java
public class Practice {
    public static void main(String[] args) {
        int n = 10;
        int [] arr = {7,5,9,0,3,1,6,2,4,8};

        for(int i = 1; i<n; i++){
            for(int j = i; j>0; j--){
                if(arr[j] < arr[j-1]){
                    int temp = arr[j];
                    arr[j] = arr[j-1];
                    arr[j-1] = temp;
                }
                else break;
            }
        }
        for(int i = 0;i<n;i++){
            System.out.print(arr[i]+" ");
        }
    }
}
```

삽입정렬의 시간 복잡도 
----
- 선택정렬과 같이 반복문이 두번들어가며 O(N<sup>2</sup>) 이다.
- 현재의 리스트가 거의 정렬되어 있는 상태라면 매우 빠르게 동작




