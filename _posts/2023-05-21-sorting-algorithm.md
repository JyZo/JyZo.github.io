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

![selection_sort1](/assets/img/post_img/selection_sort1.PNG "selection_sort1")

<br/>

![selection_sort2](/assets/img/post_img/selection_sort2.PNG "selection_sort2")

<br/>

![selection_sort3](/assets/img/post_img/selection_sort3.PNG "selection_sort3")

<br/>

![selection_sort4](/assets/img/post_img/selection_sort4.PNG "selection_sort4")

<br/>

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

![insertion_sorting1](/assets/img/post_img/insertion_sorting1.PNG "insertion_sorting1")

<br/>

![insertion_sorting2](/assets/img/post_img/insertion_sorting2.PNG "insertion_sorting2")

<br/>

![insertion_sorting3](/assets/img/post_img/insertion_sorting3.PNG "insertion_sorting3")

<br/>

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

<br/>

삽입정렬의 시간 복잡도 
----
- 선택정렬과 같이 반복문이 두번들어가며 O(N<sup>2</sup>) 이다.
- 현재의 리스트가 거의 정렬되어 있는 상태라면 매우 빠르게 동작

<br/>
<br/>

# 퀵 정렬(quice sorting)
- 기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법
- 일반적인 상황에서 가장 많이 사용
- 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간

![insertion_sorting1](/assets/img/post_img/insertion_sorting1.PNG "insertion_sorting1")

<br/>

![insertion_sorting1](/assets/img/post_img/insertion_sorting1.PNG "insertion_sorting1")

<br/>

![insertion_sorting1](/assets/img/post_img/insertion_sorting1.PNG "insertion_sorting1")

<br/>

![insertion_sorting1](/assets/img/post_img/insertion_sorting1.PNG "insertion_sorting1")

<br/>

```java
public class Practice {
    public static void main(String[] args) {
        int n = 10;
        int [] arr = {7,5,9,0,3,1,6,2,4,8};

        quickSort(arr,0,arr.length-1);
        for(int i = 0;i<n;i++){
            System.out.print(arr[i]+" ");
        }
    }
    public static void quickSort(int[] arr,int start,int end){
        if(start>=end) return;

        int pivot = start;
        int left = start+1;
        int right = end;

        while(left<=right){

            while(left<=end && arr[left] <= arr[pivot]) left++;

            while(right > start && arr[right] >= arr[pivot])right--;

            if(left > right){
                int temp = arr[pivot];
                arr[pivot] = arr[right];
                arr[right] = temp;
            }else{
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
            }
            quickSort(arr,start,right-1);
            quickSort(arr, right+1,end);
        }
    }
}
```

퀵정렬의 시간 복잡도
-----
- 이상적인 경우 분할이 절반씩 일어난다면 O(NlogN)가 기대되지만 최악의 경우 O(N<sup>2</sup>)이 된다.

<br/>
<br/>

# 계수정렬(counting sorting)
- 특정한 조건이 부합할 때만 사용할 수 있지만 **매우 빠르게** 동작하는 정렬 알고리즘
- 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을때 사용가능
- 최악의 경우에도 수행시간 O(N+K)를 보장

![contingsorting1](/assets/img/post_img/contingsorting1.PNG "contingsorting1")

<br/>

![contingsorting2](/assets/img/post_img/contingsorting2.PNG "contingsorting2")

<br/>

![contingsorting3](/assets/img/post_img/contingsorting3.PNG "contingsorting3")

<br/>

```java
public class Practice {
    public static final int MAX_VALUE = 9;

    public static void main(String[] args) {
        int n = 15;
        int [] arr = {7,5,9,0,3,1,6,2,9,1,4,8,0,5,2};
        int []  countingArr = new int[MAX_VALUE+1];

        for(int i = 0;i<arr.length;i++){
            countingArr[arr[i]] += 1;
        }

        for(int i = 0; i<countingArr.length;i++){
            for(int j = 0; j<countingArr[i];j++){
                System.out.print(i+" ");
            }
            System.out.print(" | ");
        }
    }
}
```
<br/>

계수정렬의 시간 복잡도
-----
- 시간 복잡도와 공간 복잡도는 모두 O(N+K)
- 동일한 값을 가지는 데이터가 여러개 등장할때 효과적으로 사용


정렬 알고리즘 비교
----

![compare_sorting](/assets/img/post_img/compare_sorting.PNG "compare_sorting")


