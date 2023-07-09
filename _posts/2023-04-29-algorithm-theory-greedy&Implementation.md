---
title: algorithm-theory-greedy&implementation
date: 2023-04-29 12:21 +0900
categories: [Algorithm, theory]
tags: [Algorithm, theory]
---

# 탐욕법(Greedy Algorithm)

**현재 상황에서 지금 당장 좋은 것만 고르는 방법!!**
--------------

<br/>

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
    public static void main(String[] args)  {
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
    public static void main(String[] args) {
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
    public static void main(String[] args)  {
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
    public static void main(String[] args) {
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


# 구현(Implementation Algorithm)
**머리속에 있는 알고리즘을 소스코드로 바꾸는 것!!**
----------

하지만 코딩테스트에서의 구현은 의미가 조금 다르다.

**풀이를 떠오르는 것은 쉽지만 소스코드로 옮기는 것은 어려운문제!**
---------
특히나 많은 연습이 필요한 유형이다. 많은 코드 및 라이브러리를 알수록 유리하기 때문

<br/>

## 구현 문제 1 - 상하좌우
> 여행가 A는 N x N 크기의 정사각형 공간 위에 서 있습니다. 이 공간은 1 x 1 크기의 정사각형으로 나누어져 있습니다. 가장 왼쪽 위 좌표는 (1,1)이며, 가장 오른쪽 아래 좌표는 (N,N)에 해당합니다. 여행가 A는 상,하,좌,우 방향으로 이동할 수 있으며, 시작 좌표는 항상 (1,1) 입니다. 우리 앞에는 여행가 A가 이동할 계획이 적힌 계획서가 놓여 있습니다.
계획서에는 하나의 줄에 띄어쓰기를 기준으로 L(왼쪽),R(오른쪽),U(위쪽),D(아래쪽)이며
이때 N x N 공간을 벗어나는 움직임은 무시됩니다. 여행가 A가 최종적으로 도착할 지점의 좌표(X,Y)를 출력하세요.

```java
public class Practice {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // N을 입력받기
        int n = sc.nextInt();
        sc.nextLine(); // 버퍼 비우기
        String[] plans = sc.nextLine().split(" ");
        int x = 1, y = 1;

        // L, R, U, D에 따른 이동 방향
        int[] dx = {0, 0, -1, 1};
        int[] dy = {-1, 1, 0, 0};
        char[] moveTypes = {'L', 'R', 'U', 'D'};

        // 이동 계획을 하나씩 확인
        for (int i = 0; i < plans.length; i++) {
            char plan = plans[i].charAt(0);
            // 이동 후 좌표 구하기
            int nx = -1, ny = -1;
            for (int j = 0; j < 4; j++) {
                if (plan == moveTypes[j]) {
                    nx = x + dx[j];
                    ny = y + dy[j];
                }
            }
            // 공간을 벗어나는 경우 무시
            if (nx < 1 || ny < 1 || nx > n || ny > n) continue;
            // 이동 수행
            x = nx;
            y = ny;
        }

        System.out.println(x + " " + y);
    }
}
```
이 문제도 처음 완전 노가다에 이방법이 아닌거 같아서 고민하다가 참고했다. 아이디어를 꼭 흡수하자.

## 구현문제2 - 시각
> 정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 구하는 프로그램을 작성하세요.

```java
public class Practice {
    public static void main(String[] args)  {
        int N;
        int count = 0;
        int HH=24,MM=60,SS=60;

        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();

        for(int h = 0;h<=N;h++){
            for(int m = 0;m<MM;m++){
                for(int s = 0;s<SS;s++){
                    if(String.valueOf(h).contains("3") || String.valueOf(m).contains("3") || String.valueOf(s).contains("3")) {
                        count++;
                    }
                }
            }
        }
        System.out.println(count);
    }
}
```

<br/>
<br/>

## 구현문제3 - 왕실의 나이트
> 왕실 정원은 체스판과 같은 8 X 8 좌표 평면이다. 나이트는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없다. 나이트는 특정 위치에서 다음과 같은 2가지경우로 이동할 수 있습니다.  
>1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
>2. 수직으로 두칸 이동한 뒤에 수평으로 한 칸 이동하기  
>이처럼 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 출력하는 프로그램을 작성하세요. 

```java
public class Practice {
    public static void main(String[] args) {
        String L;
        int count = 0;

        Scanner sc = new Scanner(System.in);
        L = sc.next();

        int move_x[] = {1,-1,2,-2,1,-1,2,-2};
        int move_y[] = {2,2,1,1,-2,-2,-1,-1};

        int x = L.charAt(0) - 'a';
        int y = L.charAt(1) - '1';

        for(int i = 0;i<8;i++){
                int nx = x;
                int ny = y;
                
                nx += move_x[i];
                ny += move_y[i];

                if(nx < 0 || ny < 0 || nx >8 || ny>8) continue;

                count++;
        }
        System.out.println(count);
    }
}
```
저번에 풀었던 문제에 응용이 아주 조금 더 들어간 문제였다. 코딩테스트 공부요령을 잡을 수 있었다.  
너무 오래 안 풀리는 문제는 빨리 학습하고 그 후 비슷한 문제를 풀며 학습하면 될것같다.

<br/>
<br/>

## 구현문제4 - 문자열 재정렬
> 알파벳 대문자와 숫자(0~9)로만 구성된 문자열이 입력으로 주어집니다. 이때 모든 알파벳을 오름차순으로 정렬하여 이어서 출력한 뒤에, 그 뒤에 모든 숫자를 더한 값을 이어서 출력합니다. 

```java
public class Practice {
    public static void main(String[] args) {
        String s;
        int numTotal = 0;
        Scanner sc = new Scanner(System.in);
        s = sc.next();

        ArrayList<Character> alphaArr = new ArrayList<>();
        ArrayList<Character> numArr = new ArrayList<>();

        for(int i = 0; i<s.length(); i++){
            if(Character.isDigit(s.charAt(i))){
                numArr.add(s.charAt(i));
            }else{
                alphaArr.add(s.charAt(i));
            }
        }

        Collections.sort(alphaArr);
        Collections.sort(numArr);

        for(int k=0;k<alphaArr.size();k++){
            System.out.print(alphaArr.get(k));
        }

        for(int j=0;j<numArr.size();j++){
            numTotal+=Integer.parseInt(numArr.get(j).toString());
        }
        System.out.println(numTotal);
    }
}
```

정답상 이문제는 마지막 줄에 숫자를 출력시에 조건이 하나 빠져있었다.
```java
if(numTotal != 0){
    System.out.println(numTotal);
}
```
실제로 숫자값 없이 실행시키니 위에 선언된 0이 찍혀나왔고 오답이라고 봐도 무방한 판단이었다. 더 생각하자
- 알고리즘 테스트에서는 수와 숫자를 구분하여야 한다.
  - 수 : 10,100,1000등의 실제 정수와 같은 데이터를 의미
  - 숫자 : 0~9 한자리 수를 의미


#

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]










