---
layout: post
title: javascript-middle
date: 2024-06-09 10:30 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---

# 1. 호이스팅 & TDZ

## 1.1 호이스팅

- 스코프 내부 어디서든 변수선언은 최상위에 선언된 것처럼 행동

```javascript
var name; //undefined
console.log(name);
name = "hositing"; //할당

console.log(name); // undefined
var name = "hositing";

console.log(name); // ReferenceError
let name = "hositing";
```

- var의 경우 오류를 발생시키지 않지만 let의 경우 오류가 발생, 아래 개념으로 연결
- 할당되지 않은 변수 사용을 방지하기 위해 TDZ존 등장

## 1.2 TDZ(Temporal Dead Zone)

- var는 할당이 안 되어도 사용은 가능하나 let과 const는 TDZ의 영향을 받아 선언하더라도 할당되지 않으면 사용 불가
- 코드를 예측가능하게 하고 잠재적 버그를 줄 일 수 있음

## 1.3 변수의 생성단계

> 1.  선언단계
> 2.  초기화 단계
> 3.  할당단계

- 변수는 위와 같은 3단계의 생성단계를 가지는데
  변수 타입마다 이 단계가 다른다.

### 1.3.1 var

> 1.  선언 및 초기화 단계
> 2.  할당단계

- 선언과 초기화가 함께 일어나 undefined 가 나오되 사용은 가능한것

### 1.3.2 let

> 1.  선언단계
> 2.  초기화 단계
> 3.  할당단계

- 호이스팅 되어 선언처리 되더라도 초기화가 안되어 ReferenceError가 발생하는 것

### 1.3.3 const

> 1.  선언 & 초기화 & 할당

```javascript
const = gender;
getder = 'male'
```

- 동시에 일어나기에 할당을 분리시킬경우 에러발생

### 1.3.4 변수 스코프

- 함수 스코프 : 함수 내에서 선언된 변수만 지역변수가 된다. ex)var
- 블록 스코프 : 모든 코드 블록에서 선언된 변수는 코드 내에서만 유효하며 외부에서는 접근할 수 없다. ex)let,const

# 2. 생성자 함수(Intermediate Class)

```javascript
const man = {
  name: "john",
  age: 30,
};
```

- 다음처럼 선언된 객체를 객체 리터럴이라 한다.
- 객체 리터럴을 여러개 선언해 사용할 경우 일일이 생성해 사용하기 불편하여 사용

```javascript
function Man(name, age) {
  this.name = name;
  this.age = age;
}

let man = new Man("mike", 29);
```

- 생성자 함수의 첫글자는 대문자로 사용하는 관례가 있다.

```javascript
function Man(name,age){
    //1. 빈 객체 생성
    this = {};
    //2. 객체에 값 할당
    this.name = name;
    this.age = age;
    //3. 값 반환
    return this;
}
```

- 위와 같은 3단계로 생성자 함수는 동작한다. 보이는건 값 선언뿐

# 3. 객체 메소드 & computed property

# 3.1 computed property

- 객체를 선언할 때 일반적으로 정해서 선언했던 property를 동적으로 선언하는 방법

```javascript
let a = "age";

const man = {
  ["na" + "me"]: "Mike",
  [a]: 30,
};
```

# 3.2 객체 메소드

- Object.assign(원본객체,복사할객체) : 객체복사나 병합
- Object.key() : 객체의 key값 배열 반환
- Object.values() : 객체의 value값 배열 반환
- Object.entries() : 객체의 key,value값 모두 반환
- Object.formEntries() : key,value 배열을 객체로 반환

# 4. 심볼(Symbol)

- ES6에서 추가된 자바스크립트의 새로운타입
- 이름의 충돌위험이 없는 유일한 객체의 프로퍼티 키를 만들기 위해 사용

## 4.1 Symbol

```javascript
const a = Symbol();
const b = Symbol();

console.log(a);
symbol();

console.log(b);
symbol();

a === b;
false;

a == b;
false;
```

- new 생성자를 사용하지 않고 만들며 유일성이 보장됨
- 일반적인 객체의 프로퍼티키의 경우 문자열로 만들어져 반환 및 비교가 쉽지만 심볼은 형변환도 자바스크립트 자체에서 막아준다.
- 심볼을 선언하는 순간 이건 private 필드라고 프로그래머에게 가독성을 높여줄 뿐만 아니라, 인스턴스 중복을 피할 수 있습니다.

## 4.2 Symbol.for

- 쉽게 비유하자면 전역변수
- Symbol()로 심볼을 생성하면 매번 유일한 고유의 심볼을 생성하지만 Symbol.for()을 사용할 경우 공유되는 고유 값을 생성한다

```javascript
const sf1 = Symbol.for("for");
const sf2 = Symbol.for("for");

sf1 == sf2;
//true
```

- 전역 Symbol 없으면 등록하고 있으면 가져온다.
- 생성 할 때도 Symbol.for('id')의 경우 Symbol()과 달리 반드시 생성을 위한 키값을 가져야 한다

# 5. Number,Math

- 개발을 위해 10진수가 아닌 2진수,16진수등 다른 수 및 수학적 계산이 필요할 때 사용

## 5.1 Number

```javascript
let num = 16;

num.toString(2);
num.toString(16);
```

- toString()안에 변환진수값을 넣어 변환

## 5.2 Math

- 수학관련 프로퍼티와 메소드 보유, Math.메소드로 호출
- .ceil() : 올림
- .floor() : 내림
- .round() : 반올림
- .toFixed() : 소수점 자리수 표기, 문자열을 반환하기에 숫자로 변환이 필요할 수 있음
- .isNaN() : NaN 판단 메소드
- .parseInt() : 문자열을 숫자로 변환
- .parseFloat() : 부동소수점 실수로 변환
- .random() : 임의 숫자 생성
- .max()/.min() : 인수중 최대/최소값 반환
- .abs() : 절대값
- .pow() : 제곱
- .sqrt() : 제곱근

- 찾아서 하게 될태니 존재여부만 알자

# 6. 문자열 메소드

- .length : 길이 반환
- .[index] : 배열처럼 특정 문자열 값에 접근
- .toUpperCase()/toLowerCase() : 대문자/소문자로 변환
- .indexOf(asdf) : 인수 문자열의 위치 반환
- .slice(n,m) : 특정 범위 문자열 반환
- .substring(n,m) : n과 m사이 문자열 반환
- .substr(n,m) : 특정 개수개를 반환
- .trim() : 공백 제거
- .repeat(count) : count번 반복
- .codePointAt() : 문자열을 아스키 코드 10진법으로 반환
- .fromCodePoint() : 아스키코드를 문자열로 반환
- .include() : 포함여부 반환

# 7. 배열 메소드

- .splice() : 배열의 요소를 삭제, 추가, 요소반환 등 다양히 쓰인다
- .spice(n,m) : n부터 m까지 반환
- .concat(arr1,arr2 ...) : 원본배열이랑 합친다
- .forEach(fn) : 배열 반복
- .indexOf/lastIndexOf : 인수 배열의 위치 반환/끝에서 붙어 역순 위치 반환
- .includes() : 포함여부 확인
- .find(fn)/findIndex(fn) : indexOf처럼 배열 요소를 찾지만 함수를 사용해 조건있게 찾을 수 있다.
- .filter(fn) : find와 달리 조건에 맞는 배열 모든 요소 반환
- .reverse() : 역순 재정렬
- .map(fn) : 배열을 순회하며 콜백함수가 적용된 값을 새로운 배열로 반환
- .join() : 배열의 요소를 합친다.
- .split() : 배열요소를 나누어 배열로 만든다
- .isArray() : typeof로 배열은 객체인지 판단이 불가해 배열인지 확인
- .sort(fn) : 배열을 재정렬 해주며, 배열자체가 변경된다.
- .reduce(fn) : 배열의 요소를 순회하며 하나의 값을 반환

## 7.1 차이

1. map : forEach와 유사하지만 forEach는 단순 반복문, map은 콜백 적용된 새로운 배열을 생성해준다.
2. reduce : 배열의 모든 요소를 순회하며, 하나의 값을 반환
3. find : 배열에서 일치하는 요소를 발견하면 true에 해당되는 첫번째 요소를 반환
4. filter : 자신을 호출한 배열의 모든 요소를 살펴보며, 검색기능을 수행 특정 조건을 만족하는 여러개의 요소를 선택할 때 사용

# 8. 구조분해할당

- 배열이나 객체의 속성을 본해해서 그 값을 변수에 담을 수 있게 하는 표현식

```javascript
//배열
let users = ["mike", "tom", "jane"];

let [user1, user2, user3, user4] = users;
// let user1 = user[0] mike
// user4처럼 모자랄땐 undefined, 기본값을 줘도 좋음
let [user1, , user2] = users;
// 공백도 인정이 되어 user2는 jane이 들어가게된다

//객체
let user = { name: "mike", age: 30 };
let { name, age } = user;
```

# 9. 나머지 매개변수(Rest parameters), 전개 구문(Spread syntax)

## 9.1 나머지 매개변수

- 자바스크립트의 경우 함수의 인자로 넘기는 값에 제약은 존재하지 않음
- 함수의 인자를 얻는 방법은 두 가지
  - arguments로 접근
  - 나머지 매개변수
- 편의에 의해 지금은 나머지 매개변수를 선호하는 추세

### 9.1.1 arguments

```javascript
function showName(name) {
  console.log(arguments.length);
  console.log(arguments[0]);
  console.log(arguments[1]);
}
showName("mike", "tom");
```

- 배열처럼 index를 이용해 값에 접근할 수 있다.
- arguments는 실제 배열이 아닌 Array형태의 객체이기에 map,sort등의 배열 메소드를 사용 못함
- 화살표 함수는 arguments를 지원하지 않음

### 9.1.2 나머지 매개변수

```javascript
function showName(name, age, ...hobby) {
  console.log(name);
  console.log(age);
  console.log(hobby);
}

showName(); // []
showName("mike", 30, "soccer"); // ['Mike',30,soccer]
showName("tom", 40, "dance", "game", "music");
// ['Mike', 40, dance,game,music]
```

- 여분의 매개변수는 그 값들을 담을 배열 이름을 마침표 세 개 ...뒤에 붙여주면 함수 선언부에 포함시킬 수 있다.
- 나머지 매개변수는 항상 마지막에 있어야한다.
- argument와 달리 배열 메소드들 사용 가능

## 9.2 전개 구문(Spread syntax) : 배열

- 나머지 매개변수와 반대의 역할을 하며 매개변수 목록을 배열로 가져오는게 아닌 배열을 통째로 매개변수에 넘겨주는 것 같은것을 할 때 사용
- 배열이나 문자열 같은 반복가능한 부분을 펼치게 해준다

```javascript
let arr = [3, 5, 1];
let arr2 = [8, 9, 15];

let merged = [0, ...arr, 2, ...arr2];
```

# 10. 클로저(Closer)

- 렉시컬 환경 : 코드 block, function, script를 실행하기 앞서 생성되는 특별한 객체로, 실행할 스코프 범위 안에 있는 변수와 함수를 프로퍼티로 저장하는 객체
- 함수와 렉시컬 환경의 조합, 함수가 생성될 당시의 외부변수를 기억, 생성 이후에도 계속 접근가능

```javascript
function makeCounter() {
  let count = 0; //접근불가 은닉화

  return function () {
    return count++;
  };
}

let counter = makeCounter();
console.log(counter()); //0
console.log(counter()); //1
console.log(counter()); //2
```

# 11. call, apply, bind

## 11.1 call

- call 메서드는 모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있다.

```javascript
const mike = {
  name: "mike",
};

function showname() {
  console.log(this.name);
}
showname(); //window.name
showname.call(mike); //mike.name
function update(birthday, age) {
  this.birthday = birthday;
  this.age = age;
}
update.call(mike, 20000101, 30); //this로사용할객체,매개변수들
console.log(mike);
```

## 11.2 apply

- 함수 매개변수를 처리하는 방법을 제외하면 call과 같으며 단지 매개변수를 배열로 받는다.

```javascript
const mike = {
  name: "mike",
};

function showname() {
  console.log(this.name);
}
showname(); //window.name
showname.apply(mike); //mike.name
function update(birthday, age) {
  this.birthday = birthday;
  this.age = age;
}
update.apply(mike, [20000101, 30]); //this로사용할객체,매개변수들
console.log(mike);
const nums = [1, 2, 3, 4, 5];
//const maxNum = Math.max(...nums);
const maxNum = Math.max.apply(this, nums);
const maxNum2 = Math.max.call(this, ...nums);
console.log(maxNum);
```

## 11.3 bind

- 함수의 this 값을 영구히 바꿀 수 있다.

```javascript
const mike = {
  name: "mike",
};

function update(birthday, age) {
  this.birthday = birthday;
  this.age = age;
}
const updatemike = update.bind(mike);
updatemike(19990909, 10);
console.log(mike);

const user = {
  name: "mike",
  showname: function () {
    console.log(`hi ${this.name}`);
  },
};
let fn = user.showname;
console.log("--------------------------------");
fn(); //fn을 할당할 때 this가 비어 window.name이 나옴
fn.call(user); //hi mike
fn.apply(user); //hi mike
let bindfn = user.showname.bind(mike);
bindfn(); //hi mike bind로 할당되어 this를 보관함
```

# 11. 상속, prototype

- 자바스크립트는 java와 달리 클래스 객체가 아닌 프로토타입 객체지향 언어
- class 없이도 객체 생성 가능
- Prototype 객체는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용
- 자바스크립트의 모든 객체는 프로토타입 *proto*객체를 가진다.

```javascript
const car = {
  wheels: 4,
  drive() {
    console.log("drive..");
  },
};

const bmw = {
  color: "red",
  // wheels: 4,
  navigation: 1,
  // drive() {
  //     console.log("drive..")
  // },
};

const benz = {
  color: "black",
  // wheels: 4,
  // drive() {
  //     console.log("drive..")
  // },
};

bmw.__proto__ = car;
benz.__proto__ = car;

const x5 = {
  name: "x5",
  color: "white",
};
x5.__proto__ = bmw;
```

- 공통적인 부분은 따로 빼 상속받는 형식으로 처리가능
- 상속의 상속또한 가능 프로토타입 체인이라 부른다.
- keys(),values() 메소드로는 직전 상속만 확인 가능
- **개념이나 특징 복습필요**

# 12. 클래스(Class)

```javascript
const User1 = function (name, age) {
  this.name = name;
  this.age = age;
  // this.showname(){
  //   console.log(this.name);
  // }
};
User1.prototype.showname = function () {
  console.log(this.name);
};
const man1 = new User1("mike", 30);

class User2 {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  showname() {
    console.log("User2");
  }
}
const man2 = new User2("dike", 20);

class EXuser3 extends User2 {
  constructor(name, age) {
    super(name, age);
    this.test = "test";
  }
  showlook() {
    console.log("LOOK");
  }
}
const man3 = new EXuser3("pike", 30);
```

- es6에 추가된 스펙
- 생성자 함수와 비교하여 new 를 통해 호출될때 객체생성은 동일
- 클래스는 내부에 생성자가 존재
- 클래스 내부에 정의한 메소드는 프로토타입에 저장 , 생성자 함수는 객체 내부에 존재
- 생성자 함수는 new 를빼고 선언해도 동작은 이상없지만 클래스는 프로토타입안에 class라고 명시되어있어 에러발생
- 상속 시 생성자 함수의 경우는 프로토타입을 클래스는 extends키워드 사용
- 타 클래스에서 상속받은게 클래스 내부에 들어가 있고 클래스에서 선언한것은 프로토타입에 들어가있음
- 상속 시 constructor를 만들어 호출하기전 부모 생성자를 반드시 호출 해야함,인자가 있을경우 안주면 undefined발생

# 12. Promise

- 자바스크립트의 비동기 처리의 고질적 문제인 콜백지옥을 해결하기 위해 나온 문법

```javascript
const pr = new Promise((resolve, reject) => {
  // code
  setTimeout(() => {
    // resolve("OK");   //성공시
    reject("ERR"); //실패시
  }, 3000);
});
pr.then((result) => {
  console.log(result);
})
  .catch((err) => {
    console.log(err);
  })
  .finally(() => {
    console.log("finally");
  });
```

- 기본적인 사용법은 콜백시 성공 실패 여부에 따라 분기되어 처리된다

# 13. async, await

```javascript
async function getName() {
  return "mike";
}
async function getErrName() {
  throw new Error("err");
}
getName().then((name) => {
  console.log(name);
});
getErrName().catch((name) => {
  console.log(name);
});

function getAsyncName() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("OK");
    }, 3000);
  });
}

async function asyncshow() {
  const result = await getAsyncName();
  console.log(result);
}
console.log("start");
asyncshow();
```

## 13.1 async

- 이 키워드를 붙이면 항상 Promise객체를 반환한다
- 내부에서 예외발생시 reject 반환

## 13.2 await

- async 내부에서만 사용가능
- async가 반환하는 Promise가 반환될 때까지 기다림

# 14. generator

- 함수의 실행을 중간에 멈추었다가 재개하는 기능

```javascript
function* generator() {
  yield 1;
  yield 2;
  yield 3;
  return "finish";
}
const a = generator();
```

- 함수옆에 \*을 붙여서 사용
- 반환된 객체는 value와 done값을 지니는데 value는 yield의 오른쪽값,done은 끝남여부를 체크한다
- 값을 미리 만들어두지 않고 필요한 순간에 연산해서 값을 준다.
