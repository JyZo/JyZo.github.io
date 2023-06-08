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
개미 전사를 위해 식량창고 N개에 대한 정보가 주어졌을 때 얻을 수 있는 식량의 최댓값을 구하는 프로그램을 작성하세요.

```java
public class Practice {
    public static int[] d = new int[100];

    public static void main(String[] args) {
        int N;

        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();

        int arr[] = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = sc.nextInt();
        }

        d[0] = arr[0];
        d[1] = Math.max(arr[0], arr[1]);

        for (int i = 2; i < N; i++) {
            d[i] = Math.max(d[i - 1], d[i - 2] + arr[i]);
        }

        System.out.println(d[N - 1]);
    }
}
```
- Math라이브러리의 max는 두 인자중 큰 값을 기턴,작은값을 리턴하는 min도 있음
- 점화식을 규칙성이 보이면 다이나믹 프로그래밍을 쓰는 법을 생각하자

어렵다.....

<br/>
<br/>

# 다이나믹 프로그래밍 문제 2 - 1로 만들기

>- 정수 X가 주어졌을 때, 정수 X에 사용할 수 있는 연산은 다음과 같이 4가지
>    1. X가 5로 나누어 떨어지면, 5로 나눕니다.
>    2. X가 3으로 나누어 떨어지면, 3으로 나눕니다.
>    3. X가 2로 나누어 떨어지면, 2로 나눕니다.
>    4. X에서 1을 뺍니다.
>- 정수 X가 주어졌을 때, 연산 4개를 적절히 사용해서 값을 1로 만들고자 한다. 연산을 사용하는 횟수의 최솟값을 출력하세요
>

```java
public class Practice {
    public static int[] d = new int[30001];

    public static void main(String[] args) {
        int X;
        Scanner sc = new Scanner(System.in);
        X = sc.nextInt();

        for (int i = 2; i <= X; i++) {
            d[i] = d[i - 1] + 1;

            if (i % 2 == 0) {
                d[i] = Math.min(d[i], d[i / 2] + 1);
            }
            if (i % 3 == 0) {
                d[i] = Math.min(d[i], d[i / 3] + 1);
            }
            if (i % 5 == 0) {
                d[i] = Math.min(d[i], d[i / 5] + 1);
            }
        }
        System.out.println(d[X]);
    }
}
```
- 아이디어는 생각나서 풀었는데 접근방식이 전혀 잘못되었다.

<br/>
<br/>


# 다이나믹 프로그래밍 문제 3 - 효율적인 화폐 구성
> N가지 종류의 화폐가 있습니다. 이 화폐들의 개수를 최소한으로 이용해서 그 가치의 합이 M원이 되도록 하려고 합니다. 이때 각 종류의 화폐는 몇 개라도 사용할 수 있습니다.  
M원을 만들기 위한 최소한의 화폐 개수를 출력하는 프로그램을 작성하세요.  
첫째 줄에 N,M이 주어지며 이후 N개의 줄에는 각 화폐의 가치가 주어진다. 


```java
public class Practice {
    public static int[] d = new int[10001];
    public static void main(String[] args) {
        int N,M;
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        M = sc.nextInt();

        int arr[] = new int[N];
        for(int i = 0; i<arr.length;i++){
            arr[i] = sc.nextInt();
        }

        int d[] = new int[M+1];
        Arrays.fill(d,10001);
        d[0] = 0;
        
        for(int i = 0;i<N;i++){
            for(int j = arr[i]; j<=M;j++){
                
                if(d[j - arr[i]] != 10001){
                    d[j] = Math.min(d[j],d[j - arr[i]]+1);
                }
            }
        }
        if(d[M] == 10001){
            System.out.println(-1);
        }else{
            System.out.println(d[M]);
        }
    }
}
```

- Arrays.fill(arr[],n)의 경우 처음 사용해본다. 배열(arr[])과 값(n)을 인자로 넣으면 배열안의 값을 모두 n값으로 초기화 해주며 Arrays.fill(arr[],start,end,n)처럼 특정 범위의 값을 초기화도 가능하다. 

<br/>
<br/>

# 다이나믹 프로그래밍 문제 4 - 금광
>n x m 크기의 금광이 있습니다. 금광은 1 X 1크기의 칸으로 나누어져 있으며 금이 들어있습니다.  
채굴자는 첫번째 열부터 출발하여 금을 캐기 시작합니다. 맨 처음에는 첫번째 열의 어느 행에서든 출발할 수 있습니다. 이후에 m - 1번에 걸쳐서 매번 오른쪽 위, 오른쪽, 오른쪽 아래 3가지 중 하나의 위치로 이동, 채굴자가 얻을 수 있는 금의 최대 크기를 출력하는 프로그램을 작성하세요.  
첫째 줄에 테스트 케이스 T가 입력, 매 테스트 케이스 첫째 줄이 n과 m이 공백으로 구분되어 입력, 둘째 줄에 매장된 금의 개수가 공백으로 구분되어 입력한다.

```java
public class Practice {
    static int t, n, m;
    static int[][] arr = new int[20][20];
    static int[][] dp = new int[20][20];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        t = sc.nextInt();
        for (int tc = 0; tc < t; tc++) {
            n = sc.nextInt();
            m = sc.nextInt();
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    arr[i][j] = sc.nextInt();
                }
            }

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    dp[i][j] = arr[i][j];
                }
            }

            for (int j = 1; j < m; j++) {
                for (int i = 0; i < n; i++) {
                    int leftUp, leftDown, left;

                    if (i == 0) leftUp = 0;
                    else leftUp = dp[i - 1][j - 1];

                    if (i == n - 1) leftDown = 0;
                    else leftDown = dp[i + 1][j - 1];

                    left = dp[i][j - 1];
                    dp[i][j] = dp[i][j] + Math.max(leftUp, Math.max(leftDown, left));
                }
            }
            int result = 0;
            for (int i = 0; i < n; i++) {
                result = Math.max(result, dp[i][m - 1]);
            }
            System.out.println(result);
        }
    }
}
```
- 동적프로그래밍이 문제가 많기도 한데 체감상 난이도가 정말 쉽지않다....
이번 문제의 경우 그래도 아이디어를 어느정도 내는 것에는 성공, 구현부분에서 조금 버벅였다.

<br/>
<br/>


# 다이나믹 프로그래밍 문제 5 - 병사 배치하기
> N명의 병사가 무작위로 나열되어 있습니다. 각 병사는 특정한 값의 전투력을 보유하고 있습니다.  
병사를 배치할 때는 전투력이 높은 병사가 앞쪽에 오도록 내림차순으로 배치를 하고자 합니다.  
또한 배치 과정에서는 특정한 위치에 있는 병사를 열외시키는 방법을 용합니다. 그러면서도 남아 있는 병사의 수가 최대가 되도록 하고 싶습니다.  
첫째 줄에 병사 N이 주어지고 둘째 줄에 병사들의 전투력이 주어진다.

```java
public class Practice {
    static int n;
    static ArrayList<Integer> v = new ArrayList<Integer>();
    static int[] dp = new int[2000];
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            v.add(sc.nextInt());
        }
        
        Collections.reverse(v);
        
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
        }
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (v.get(j) < v.get(i)) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        int maxValue = 0;
        for (int i = 0; i < n; i++) {
            maxValue = Math.max(maxValue, dp[i]);
        }
        System.out.println(n - maxValue);
    }
}
```
- 기본 아이디어는 가장 긴 증가하는 부분수열(Longest Increasing Subsequence,LIS) 라고 알려진 전형적인 다이나믹 프로그래밍 문제의 아이디어와 같다. 
- LIS알고리즘을 이용해 배열을 뒤집어 계산하는게 키포인트
- Collections.reverse(list)는 인자로 받은 리스트의 순서를 뒤집는다. 

<br/>
<br/>

------

출처 - 나동빈 개발자님 유튜브[[https://www.youtube.com/@dongbinna](https://www.youtube.com/@dongbinna)]