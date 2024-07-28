---
layout: post
title: React-BASIC
date: 2024-07-02 18:15 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---

> 책 외에 인강을 한번 더 들으면서 가볍게 개념 및 팁 정리, 몽고디비는

# 1. JSX

- class를 사용할 땐 className
- 변수명을 사용할 땐 {변수명}
- style을 사용할 땐 style={{이름 : '값'}}

# 2. STATE

- 변수 등이 변동 시 자동으로 html을 재랜더링하며 사용할때 사용

```javascript
const [state명, state변경함수] = useState("초기값");

const state변경함수 = () => {
  state명[0] = "바꿔보자";
  setTitle(state명);
};
```

- state 변경함수 특징
  - 기존 state == 신규 state 일 경우 변경해주지않음
- array/object 특징
  - 변수에 값이 담기는게 아니라 메모리 주소값만 저장됨
  - 그래서 위처럼 단순 값만 바꾸어도 값은 바뀌지만 주소값이 안 바뀌므로 같다라고 판단하여 변경하지않음

# 컴포넌트

- 컴포넌트 사용 시기
  - 반복적 html 축약할 때
  - 큰 페이지들
  - 자주 변경되는 페이지들
- const 선언으로 만드는이유 : 향후 다른곳에서 수정될 때 에러 출력, 상수이기에
- 동적인 UI 만드는 요령
  - 1. html,css디자인 미리 완성
  - 2. UI의 현재 상태를 state로 저장
  - 3. state에 따라 UI가 어떻게 보일지 작성

# props

- 반드시 부모 -> 자식으로만 전송가능
- 변수뿐만 아니라 함수까지 가능
- event버블링 복습

# Router

- 일반적인 페이지 분리

  - html 파일 생성 후 페이지 채움
  - /경로 로 접속하면 파일 내보냄

- 리액트 페이지 분리
  - index.html 유일한 페이지사용
  - 컴포넌트 생성 후 상세페이지 채움
  - /경로 에 접속하면 그 컴포넌트를 보여줌

# styled-components

- CSS파일 사용없이 js파일에서 css 디자인을 끝낼 수 있게 해줌
- 장점

  - CSS파일을 열지 않아도 된다
  - 스타일이 분리되어 다른 js파일에 오염되지 않는다
  - 컴포넌트.module.css로 오염없이 특정 파일에 종속시키기도 가능
  - 페이지 로딩시간 단축

- 단점
  - JS파일 매우 복잡해짐
  - 중복 스타일은 컴포넌트간 import하게되는데 그럼 CSS파일과 다른점이 없다
  - 협업시 CSS담당이 있을경우 불편 야기

# 컴포넌트 Lifecycle

- 페이지에 장착(mount)
- 업데이트(update)
- 필요없을 시 제거(unmount)

  > 크게 위와 같은 라이프 사이클들이 있는데 이 라이프사이클들에 간섭하기위해 아래 hook 등을 사용

- useEffect
  - 어려운 연산
  - 서버에서 데이터 가져오는 작업
  - 타이머 등등
- 리액트 18부터 automatic batching기능이 새로 생김
  - state 변경 함수들의 위치가 가까울 경우 하나로 합쳐서 한번만 state를 변경해준다.

# Context API

- SPA 의 단점으로 부모자식간을 제외하고 state 공유가 어렵다.
- 그래서 공유를 위해 존재
  - Context API 리액트 기본문법
    - state 변경시 잡다한거까지 다 렌더링하여 덜 씀
    - 다른페이지 재사용이 어려움
  - Redux등의 외부라이브러리를 이용해 상태관리

# Redux

- props없이 state를 공유가능하게 해주는 라이브러리
- 공유는 가능하지만 새로고침 시 state정보가 초기화된
  - 그래서 redux-persist, localstorage등을 사용해 새로고침시에도 보관가능하게하는 방법이 존재
