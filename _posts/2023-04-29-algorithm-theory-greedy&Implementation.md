---
title: algorithm-theory-greedy&implementation
date: 2023-04-29 12:21 +0900
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---

# 탐욕법(Greedy Algorithm)

**현재 상황에서 지금 당장 좋은 것만 고르는 방법!!**

![greedy1](/assets/img/post_img/greedy1.PNG "greedy1")


위와 같은 이미지가 있을 시에 최적의 해는 5->7->9의 합인 21이 맞지만  

![greedy2](/assets/img/post_img/greedy2.PNG "greedy2")


다음 사진 처럼 현재 상황에서 요구되는 가장 큰 값을 고를 경우 5->10->4를 거쳐게  
되고 그렇게 될 경우 문제의 정답에 근접할 수 없게 된다. 

- 그리디 알고리즘은 일반적으로 최적의 해를 보장못하는 경우가 많다. 
- 하지만 코딩테스는 테스트기에 대부분의 문제는 탐욕법으로 얻은 해가 최선이  
되도록 설계하여 문제를 출제한다. 

다음과 같은 문제가 있을 때 이 문제는 그리디 알고리즘을 사용하여도 최적의 해가  
나오게 된다.  
그 이유는 가지고 있는 동전중에서 **큰 단위가 항상 작은 단위의 배수이므로 작은 동전들을 종합해 다른 해가 나올 수 없기 때문**이다. 
- ex) 800원의 경우 500원 400원 100원 짜리가 존재 할 때!  

<br/>
<br/>

## 탐욕법 문제 1 - 1이 될때까지

#

> 어떠한 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 합니다.  
단, 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있습니다.
 >1. N에서 1을 뺍니다.  
 >2. N을 K로 나눕니다.  
>
 >N과 K가 주어질 때 N이 1이 될 때까지 1번 혹은 2번의 과정을 수행히야 하는 최소 횟수를 구하는 프로그램을 작성하세요.

 ```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int n;
        int k;
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        k = scanner.nextInt();

        int count = 0;
        while (n != 1) {
            if (n % k == 0) {
                n /= k;
                count++;
            } else {
                n -= 1;
                count++;
            }
        }
        System.out.println(count);
    }
}
 ```
무난하게 풀고 정답강의가 뒤에 이어질때 꽤나 큰 충격을 받았다.  
정말 생각의 깊이가 다르다는게 어떤건지 느꼈다. 문제를 풀었다고 바로 넘어가지 말고 이 뛰어난 발상의 물고기를 잡는법을 배워야 함을 느낀다........  


```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int n;
        int k;
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        k = scanner.nextInt();
        int result = 0;

        while (true) {
            // N이 K로 나누어 떨어지는 수가 될 때까지만 1씩 빼기
            int target = (n / k) * k;
            result += (n - target);
            n = target;
            // N이 K보다 작을 때 (더 이상 나눌 수 없을 때) 반복문 탈출
            if (n < k) break;
            // K로 나누기
            result += 1;
            n /= k;
        }
        // 마지막으로 남은 수에 대하여 1씩 빼기
        result += (n - 1);
        System.out.println(result);
    }
}
```
<br/>
<br/>

## 탐욕법 문제 2 - 곱하기 혹은 더하기

#

>각 자리가 숫자(0부터 9)로만 이루어진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자사이에 'X' 혹은 '+' 연산자를 넣어 결과적으로 만들어질 수 있는 가장 큰 수를 구하는 프로그램을 작성하세요. 일반 사칙연산 수행순서와 달리 모든 연산은 왼쪽에서부터 오늘쪽으로 순서대로 이루어진다고 가정합니다.

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        String s;
        int result = 0;

        Scanner scanner = new Scanner(System.in);
        s = scanner.next();

        result = Character.getNumericValue(s.charAt(0));
        for(int i = 1; i<s.length();i++){
            if(result < 2 || Character.getNumericValue(s.charAt(i)) < 2){
                result += Character.getNumericValue(s.charAt(i));
            }else{
                result *= Character.getNumericValue(s.charAt(i));
            }
        }
        System.out.println(result);
    }
}
```

이 문제의 경우는 하다가 오랫동안 안 풀려서 정답을 참고하고 풀어 합쳤다. 로직자체의 문제보다는 char타입의 이해도 부족이 원인이었다.  
문자타입의 경우를 그저 단순하게 숫자로 형변환 하니 값이 아스키 코드가 나와버려 계산이 꼬여버린 것이다. 내가 쓴 방법은 정답과는 다른 방법의 변환방법인데 정답의 경우는
```java
result = s.charAt(0) - '0' //'0'은 아스키코드값으론 48
//정수 변환으로 볼 경우 정수값 1일경우 1 - '0' = 49-48 = 1처럼 변환
```
위처럼 캐릭터형에서 같은 아스키코드 값인 '0'을 빼는 방법을 사용하였으나 다른 방법이 있을까 찾아보다가  
기왕이면 라이브러리를 쓰는방법이 더 깔끔하다고 판단되어 난 이 문제를 풀때는 라이브러리를 썼고 두 방법  
모두 알아둘 필요는 있다고 생각되어 일단 적어두기로 했다.


<br/>
<br/>

## 탐욕법 문제 3 - 모험가 길드

#

> 한 마을에 모함가가 N명 있고 모험가들을 대상으로 공포도를 측정했는데, 공포도가 높은 모험가는 쉽게  
공포를 느껴 위험 상황에서 제대로 대처할 능력이 떨어집니다. 공포도가 X인 모험가는 반드시 X명  
이상으로 구성한 모험가 그룹에 참여해야 여행을 떠날 수 있습니다. N명의 모험가에 대한 정보가 주어졌을때 여행을 떠날 수 있는 그룹 수의 최댓값을 구하는 프로그램을 작성하세요.

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int N,X;

        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt();

        int arr[] = new int[N];

        for(int i = 0;i<N;i++){
            X = scanner.nextInt();
            arr[i] = X;
        }
        Arrays.sort(arr);

        int groupMemberCount = 0;
        int groupCount = 0;

        for(int k = 0;k<arr.length;k++){
            groupMemberCount+=1;
            if(arr[k] <= groupMemberCount){
                groupCount++;
                groupMemberCount = 0;
            }
        }
        System.out.println(groupCount);
    }
}
```
- Arrays.sort(arr) - 오름차순 배열 정렬
- Arrays.sort(arr, Collections.reverseOrder()) - 내림차순 배열 정렬
난 배열을 사용하였으나 정답상엔 ArrayList를 사용한 정도의 차이점이 있었다.
<br/>
<br/>









