---
title: Markdown Guide
author: JyZo
date: 2023-03-26 16:57 +0900
categories: [Tip, Blog]
tags: [Tip]
math: true
---


우여곡절 끝에 미루었던 생에 첫 블로그를 만들었다.  

사실 블로그를 만들 도구는 티스토리, 네이버 블로그 등 여러가지가 있었으나 나는 개발자이고 개발자가 사용하기엔 익히기 어렵더라도 깃허브 블로그가 여러가지 장점을 가지고 있다고 생각해 깃허브 블로그를 만들기로 했다.  

그런데 진짜 만들면서 고생을 꽤 많이했다....ㅠ  
특히 이 테마를 윈도우에서 적용하다보니 여러 문제가 많아서 더 힘들었던것 같다.  리눅스 환경에서 더 최적화가 잘 되어있기에....

이 글은 최초의 포스팅이며 첫 포스팅인 만큼 블로그를 포스팅 하는데 꼭 필요하면서 한번도 안 써본 마크다운 문법을 써보면서 문법을 앞으로의 포스팅을 위해 정리하려고 한다.  
<br/>
<br/>

# Headers

제목의 경우 "#" 기호를 사용 후 개수(1~6)를 이용해 크기조절을 한다. 

```
# 제목1
## 제목2
### 제목3
```

# 제목1
## 제목2
### 제목3

"-------", "======="을 이용해서도 만들 수 있다. 

```
제목1
============
제목2
------------
```

제목1
============
제목2
------------


개인적으로는 위의 "#"형식을 사용을 더 많이 할듯하고 그냥 "#"만 써서 줄을 만드는 방법도 사용할듯 하다. 
<br />
<br />

# Line Breaks
```
띄우기  
띄우기    
띄우기
```
 띄우기  
 띄우기    
     띄우기

 문장을 작성하고 엔터로 줄을 바꿔도 줄이 바뀌진 않는다 
 
 스페이스바 두칸으로 공백을 만들어줘야 줄이 띄워진다.
<br />
<br />

# Emphasis
## 1. bold

```
**진하게**
__진하게__
```
**진하게**  
__진하게__
<br/>

## 2. Italic
```
*기울어*
_기울어_
```
*기울어*  
_기울어_
<br/>

응용으로 두 기호를 세개 붙이면 두 가지가 다 적용된다.
```
***합치기***
```
***합치기***
<br/>
<br/>

# Blockquote
```
> 인용구래요
>
>> 인용구래요
> - 점찍기  
> *기울고*  
> **진하게**
>
>***끝***
```
> 인용구래요
>
>> 인용구래요
> - 점찍기  
> *기울고*  
> **진하게**
>
>***끝***
<br/>
<br/>

# List
```
1. 하나
2. 둘
3. 셋
    1. 하나
    3. 셋
    5. 다섯
4. 넷
```

1. 하나
2. 둘
3. 셋
    1. 하나
    3. 셋
    5. 다섯
4. 넷

양식만 지키면 내가 입력하는 숫자는 상관없이 정리된다. 
<br/>
<br/>

# Unordered Lists
```
- 하나
* 둘
+ 셋
    - 하나
    * 둘
    + 셋    
요렇게
    >이렇게
- 넷
```
- 하나
* 둘
+ 셋
    - 하나
    * 둘
    + 셋    
요렇게
    >이렇게
- 넷

 특정기호만 사용하면 알아서 리스트화 되는데 "-" 를 제일 많이쓸거 같은 기분이 든다....
 추가적으로 리스트 기호 없이 줄 맞추려면 공백4 칸 또는 탭키로 만들면 된다.
 <br/>
 <br/>

# Image

```
![cute_ant](/assets/img/favicons/android-chrome-192x192.png "cute_ant"){: width="200" height="500" .w-75 .normal}  
<img src="/assets/img/favicons/android-chrome-192x192.png" height="500px" width="200px" style="border:20px solid #eaeaea; border-radius: 15px; padding: 0px">
```
![cute_ant](/assets/img/favicons/android-chrome-192x192.png "cute_ant"){: width="200" height="500" .w-75 .normal}  
<img src="/assets/img/favicons/android-chrome-192x192.png" height="500px" width="200px" style="border:20px solid #eaeaea; border-radius: 15px; padding: 0px" align="left">


이미지 같은 경우 사실 마크다운 문법보다 익숙한 html 문법을 더 자주 사용할 것 같다. 
속성들 중 몇가지가 왜 안 먹히나 했는데 테마 디렉토리 내부의 다른 디렉토리에서 css파일에 있는 설정을 사용하고 있어서 그랬다. 나중에 바꿀일 있으면 바꿔야지......
<br/>
<br/>

# Links

```
google [Google](https://www.google.com/).
<https://www.google.com/>
```
google [Google gogo](https://www.google.com/).  
<https://www.google.com/>
<br/>
<br/>

# Fenced Code Blocks
```
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

마크다운 문법 적용이 되지 않게 순수하게 텍스트만 출력하기에 편하며 json,java등 문법에 따른 가시성 까지 적용시킬 수 있는 굉장히 편리하고 많이 쓸거같은 문법이다.

#

여기까지 일차적으로 자주 쓸것 같은 문법들을 정리하고 사용해 보았고 드디어 대망의 첫 포스팅이 끝났다. 뭔가 뿌듯하다....






