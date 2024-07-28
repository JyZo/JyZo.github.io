---
layout: post
title: javascript_basic
date: 2024-06-04 01:24 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---

# 1. 변수

- 정보에 이름을 붙여 저장

## 1.1 let

- 변할 수 있는 값을 선언할 때 사용, 동일한 변수명으로 선언하면 에러가 발생하여 중복 방지
- 아직 옛날 방식인 var로 선언하는 경우가 있는데 var은 동일변수명 선언이 되어 비추

## 1.2 const

- 변할 수 없는 값인 상수를 선언할 때 사용
- 대문자로 사용하는걸 권장

# 2. 자료형

- 변수나 값이 가질 수 있는 데이터 종료
- typeof 메소드로 확인 가능

## 2.1 문자형

- ",',`등으로 표현 가능
- 문자중에 위값을 표현하려면 \'를 써서 표현
- `은 문자열 내부 변수를 표현할 때 사용 권장

## 2.2 숫자형

- 일반적인 숫자 사용하듯이 사용하면 됨, 사칙연산까지

## 2.3 Boolean

- true,false 참거짓 을 표현

## 2.4 null && undefined

- null은 값이 실제로 없는 경우, null은 객체(Object)가 아님
- undefined는 선언은 되었으나 할당되지 않은 경우

# 3 대화상자

## 3.1 alert

- 알림창 띄워줌

## 3.2 prompt

- 사용자에게 입력창 띄워줌, 입력받은 값의 타입은 문자형

## 3.3 confirm

- 사용자에게 확인창을 띄워줌

# 4 형변환

## 4.1 자동 형변환

- js 내부에서 자동으로 타입을 변환해 주는데 의도와 다르게 변환 될 때도 있기에 명시적 형변환이 필요

## 4.2 명시적 형변환

- String() : 문자형으로 변환
- Number() : 숫자형으로 변환, 문자형과 함께 들어갈 경우 NaN이 발생하니 주의, Number(null) - 0, Number(undefined) - NaN
- Boolean() : Boolean형으로 변환, 0, null, undefined, NaN, " " 의 경우들만 false 나머진 true

# 5. 연산자

- +,-,\*,/ : 사칙연산
- \*\* : 거듭제곱
- 우선순위가 존재
- ++,-- : 증가,감소 연산자

# 6. 비교 연산자, 조건문

## 6.1 비교연산자

- 일반적인 수학의 부등호를 사용해 사용
- 항상 Boolean값만 반환
- == , != : 동등, 부정 인데 ===으로 타입까지 고려하여 비교하므로 동등은 ===을 권장

## 6.2 조건문

- if : 조건에 따라 분기
- 자바와 동일해보임

# 7. 논리연산자

## 7.1 || (OR)

- 하나의 값이라도 true일때 true반환, 첫번째 true를 발견하면 평가를 멈춤

## 7.2 &&(AND)

- 모든 값이 true일 때 true반환, 첫번째 false를 발견하면 평가를 멈춤
- 평가 알고리즘에 따라 조건의 적절한 순서 사용 권장

## 7.3 !(NOT)

- true와 false를 반댓값으로 반환

# 8. 반복문

- 일반적으로 C,JAVA등에서 쓰이는 방식과 동일

## 8.1 for

```javascript
for (let i = 0; i < 10; i++) {}
```

## 8.2 while

```javascript
let i = 0;
while (i < 10) {}
```

## 8.3 do..while

```javascript
let i = 0;
do {
  i++;
} while (i < 10);
```

## 8.4 break,continue

- break : 반복문 탈출
- continue : 반복문 건너뜀

## 8.5 switch

- 반복문으로 동일하지만 케이스가 많을 땐 쓰는게 더 좋을때가 있음
- 조건이 만족되면 아래로 내려가므로 필요에따라선 break로 탈출해줘야함

```javascript
let fruit = prompt("select fruit");
switch (fruit) {
  case "apple":
    break;
  case "banana":
    break;
  case "melon":
    break;
  default:
}
```

# 9 함수(function)

- 비슷한 동작등을 하는 기능을 재활용하기 위해 분리해 놓음

```javascript
//함수 선언문
function 함수명(매개변수 = "없을때") {
  let value = 매개변수;
  console.log(value);
  return value;
}

//함수 표현식
let 함수명 = function (매개변수) {
  let value = 매개변수;
  console.log(value);
  return value;
};
```

- 기본값 없을 때 default 값 설정가능
- 반환값이 없거나 return;만 있을땐 일반적으로 undefined를 반환
- 한번에 한작업에만 집중
- 읽고 이해쉬운 함수명 짓기

## 9.1 함수 선언문 vs 함수 표현식

- 함수 선언문 : 어디서든 호출가능
- 함수 표현식 : 코드에 도달하면 생성, 고로 실행 전 선언이 먼저 되어있어야함

# 10. 화살표 함수

```javascript
let 함수명 = (매개변수) => {
  let value = 매개변수;
  console.log(value);
  return value;
};
```

- 규칙들이나 축약법이 자잘하게 있긴한데 이건 쓰면서 익히자

# 11. 객체(Object)

- 중괄호를 이용해 만들며, 데이터타입에 구애받지 않고 작성가능
- 중괄호를 통해 만들어지며 key:value 쌍으로 구성된 프로퍼티로 구성

## 11.1 선언

```javascript
const man = {
  name: "john",
  age: 30,
};
```

- const는 선언하면 바꿀 수 없는 값인 상수선언이지만 객체는 const로 선언되어도 수정이 가능하다.

## 11.2 접근, 추가, 삭제

- 접근 : man.name, man[name]
- 추가 : man.hobby
- 삭제 : delete man.hobby

## 11.3 method

- 객체 프로퍼티로 할당 된 함수

```javascript
const man = {
  name : "john",
  age : 30
  move:function(){
    console.log('move!');
  }
};
```

- 화살표 함수는 일반 함수와 달리 자신만의 this가 없다
- 고로 화살표 함수가 this를 사용하면 외부에서 값을 가져온다.
- 화살표 함수는 this가 없기에 window같은 전역객체를 가르키게 된다.

# 12. 배열(Array)

- 순서가 있는 리스트, 대괄호로 묶고 쉼표로 끊어 표기
- 고유번호인 index를 두어 탐색

```javascript
const arr = ["haha", "hoho", "hehe"];
console.log(arr[0]);
```

- push() : 맨뒤에 추가
- pop() : 맨뒤에 제거
- unshift : 맨앞에 추가
- shift : 맨앞에 제거
