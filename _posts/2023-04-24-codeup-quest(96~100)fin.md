---
title: codeup quest(96~100)fin
date: 2023-04-24 20:16 +0900
author: JyZo
categories: [Algorithm, CodeUp 100]
tags: [Algorithmm,CodeUp 100]
---


# 1096 : [기초-2차원배열] 바둑판에 흰 돌 놓기
>바둑판에 올려 놓을 흰 돌의 개수(n)가 첫 줄에 입력된다.  
둘째 줄 부터 n+1 번째 줄까지 힌 돌을 놓을 좌표(x, y)가 n줄 입력된다.  
n은 10이하의 자연수이고 x, y 좌표는 1 ~ 19 까지이며, 같은 좌표는 입력되지 않는다.  

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int arr[][] = new int[19][19];
        int n,x,y;

        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();

        for(int i = 0;i<n;i++){
            x = scanner.nextInt();
            y = scanner.nextInt();
            arr[x-1][y-1]=1;
        }

        for(int k = 0;k<19;k++){
            for(int j = 0;j<19;j++){
                System.out.print(arr[k][j]+" ");
            }
            System.out.println();
        }
    }
}
```

<br/>
<br/>

# 1097 : [기초-2차원배열] 바둑알 십자 뒤집기
>바둑알이 깔려 있는 상황이 19 * 19 크기의 정수값으로 입력된다.  
십자 뒤집기 횟수(n)가 입력된다.  
십자 뒤집기 좌표가 횟수(n) 만큼 입력된다. 단, n은 10이하의 자연수이다.  
십자 뒤집기란 그 좌표값을 제외한 나머지 x,y축 값을 모두 반전시키는것  

```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int arr[][] = new int[19][19];
        int m,n,x,y;
        Scanner scanner = new Scanner(System.in);

        for(int k = 0;k<19;k++){
            for(int j = 0;j<19;j++){
                m = scanner.nextInt();
                arr[k][j] = m;
            }
            System.out.println();
        }

        n = scanner.nextInt();

        for(int i = 0;i<n;i++){
            x = scanner.nextInt();
            y = scanner.nextInt();

            for(int a = 0;a<19;a++){
                if(arr[x-1][a]==0){
                    arr[x-1][a] = 1;
                }else{
                    arr[x-1][a] = 0;
                }
            }
            for(int b = 0;b<19;b++){
                if(arr[b][y-1]==0){
                    arr[b][y-1] = 1;
                }else{
                    arr[b][y-1] = 0;
                }
            }
        }
        for(int k = 0;k<19;k++){
            for(int j = 0;j<19;j++){
                System.out.print(arr[k][j]+" ");
            }
            System.out.println();
        }
    }
}
```

<br/>
<br/>

# 1098 : [기초-2차원배열] 설탕과자 뽑기
> 격자판의 세로(h), 가로(w), 막대의 개수(n), 각 막대의 길이(l),막대를 놓는 방향(d:가로는 0, 세로는 1)과
막대를 놓는 막대의 가장 왼쪽 또는 위쪽의 위치(x, y)가 주어질 때,  
격자판을 채운 막대의 모양을 출력하는 프로그램을 만들어보자.  


```java
public class Practice {
    public static void main(String[] args) throws ParseException {
        int w,h,n,l,d,x,y;

        Scanner scanner = new Scanner(System.in);
        w = scanner.nextInt();
        h = scanner.nextInt();
        int arr[][] = new int[w][h];
        System.out.println();

        n = scanner.nextInt();
        System.out.println();

        for(int i= 0;i<n;i++) {
            l = scanner.nextInt();
            d = scanner.nextInt();
            x = scanner.nextInt();
            y = scanner.nextInt();

            for(int k = 0;k<l;k++){
                if(d==1){
                    arr[x-1][y-1]=1;
                    x++;
                }else{
                    arr[x-1][y-1]=1;
                    y++;
                }
            }
        }
        for(int o = 0;o<w;o++){
            for(int p = 0;p<h;p++){
                System.out.print(arr[o][p]+" ");
            }
            System.out.println();
        }
    }
}
```
<br/>
<br/>

# 1099 : [기초-2차원배열] 성실한 개미
> 미로 상자에 넣은 개미는 먹이를 찾았거나, 더 이상 움직일 수 없을 때까지
오른쪽 또는 아래쪽으로만 움직였다.  
미로 상자의 구조가 0(갈 수 있는 곳), 1(벽 또는 장애물)로 주어지고,
먹이가 2로 주어질 때, 성실한 개미의 이동 경로를 예상해보자.  
단, 맨 아래의 가장 오른쪽에 도착한 경우, 더 이상 움직일 수 없는 경우, 먹이를 찾은 경우에는 더이상 이동하지 않고 그 곳에 머무른다고 가정한다.  
미로 상자의 테두리는 모두 벽으로 되어 있으며,
개미집은 반드시 (2, 2)에 존재하기 때문에 개미는 (2, 2)에서 출발한다.  

```java

```