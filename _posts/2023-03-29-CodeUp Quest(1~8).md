---
title: CodeUp Quest(1~8)
date: 2023-03-29 00:58 +0900
author: JyZo
categories: [Algorithm, CodeUp 100]
tags: [Algorithmm,CodeUp 100]
---


각종 공부를 하겠지만 꾸준히 논리력 향상을 위해 알고리즘 문제를 풀어보려고 한다.  
어떻게 시작을 할까? 고민하던 찰나 나동빈님의 강의를 듣고 커리큘럼을 따라가 보기로 했다.  
차이점이 있다면 파이썬이나 C++을 추천하셨지만 난 내가 쓰는 언어인 자바도 더 익숙해 질 겸  
자바를 사용할거라는 차이점 정도이다.
<br/>
<br/>

# 1001 : [기초-출력] 출력하기01
>C/C++언어에서 가장 기본적인 명령이 출력문이다.
>printf()를 이용해 다음 단어를 출력하시오.  
>Hello

```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
<br/>
<br/>

# 1002 : [기초-출력] 출력하기02
>이번에는 공백()을 포함한 문장을 출력한다.다음 문장을 출력해보자.  
>Hello World
(대소문자에 주의한다.)
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
<br/>
<br/>

# 1003 : [기초-출력] 출력하기03
>이번에는 줄을 바꿔 출력하는 출력문을 연습해보자.  
>다음과 같이 줄을 바꿔 출력해야 한다.  
>Hello  
>World  
>(두 줄에 걸쳐 줄을 바꿔 출력)
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("Hello \nWorld");
    }
}
```
<br/>
<br/>

# 1004 : [기초-출력] 출력하기04
>이번에는 작은 따옴표(single quotation mark)가 들어있는  
>특수한 형태의 출력문에 대한 연습을 해보자.  
>다음 문장을 출력하시오.  
>'Hello'
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("\'Hello\'");
    }
}
```
<br/>
<br/>

# 1005 : [기초-출력] 출력하기05
>이번에는 큰따옴표(double quotation mark)가 포함된 출력문을 연습해보자.  
>다음 문장을 출력하시오.  
>"Hello World"  
>(단, 큰따옴표도 함께 출력한다.)
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("\"Hello\"");
    }
}
```
<br/>
<br/>

# 1006 : [기초-출력] 출력하기06
>이번에는 특수문자 출력에 도전하자!!  
>다음 문장을 출력하시오.  
>"!@#$%^&*()"  
>(단, 큰따옴표도 함께 출력한다.)  
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("\"!@#$%^&*()\"");
    }
}
```
<br/>
<br/>

# 1007 : [기초-출력] 출력하기07
>윈도우 운영체제의 파일 경로를 출력하는 연습을 해보자.  
>파일 경로에는 특수문자들이 포함된다.  
>다음 경로를 출력하시오.  
>"C:\Download\hello.cpp"  
>(단, 큰따옴표도 함께 출력한다.)
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("\"C:\\Download\\hello.cpp\"");
    }
}
```
<br/>
<br/>

# 1008 : [기초-출력] 출력하기08
>이번에는 특수문자를 출력하는 연습을 해보자.  
>키보드로 입력할 수 없는 다음 모양을 출력해보자.  
>(** 참고 : 운영체제의 문자 시스템에 따라 아래와 같은 모양이 출력되지 않을 수 있다.)  
>┌┬┐  
>├┼┤  
>└┴┘  
```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("\u250C\u252C\u2510\n\u251C\u253C\u2524\n\u2514\u2534\u2518\n");
    }
}
```
<br/>
<br/>
