---
layout: post
title: react-hook
date: 2024-07-30 00:38 +0900
---

# REACT Hook

> 훅에대해서 따로 공부가 필요할것 같아 정리

# 1. useState

## 1.1 State

- 컴포넌트의 상태

## 1.2 선언

```javascript
const [state, setState] = useState("초기값");
```

- state에 상태저장, setState로 state값을 변경
- setState로 변경할 때마다 화면이 재렌더링 된다
- 재렌더링 시 컴포넌트 내부가 초기화

## 1.3 EX

```javascript
import "./styles.css";
import { useState } from "react";

function App() {
  const [time, setTime] = useState(1);

  return (
    <div className="App">
      <span>현재 시각 {time}시</span>
      <button
        onClick={() => {
          setTime(time + 1);
        }}
      >
        Update
      </button>
    </div>
  );
}

export default App;
```

# 2. useEffect

## 2.1 용도

- 리액트 라이프사이클에서 컴포넌트가 Mount 된 후, Update 된 후,Unmount 되기 전 useEffect는 실행되며, 특정 작업을 처리할 코드를 실행 시킬 때 사용

## 2.2 선언

```javascript
useEffect(() => {
  //작업
});

useEffect(() => {
  //작업
}, [value]);
```

- 인자가 없을땐 렌더링 될 때 마다 실행
- 인자가 있을 때는 화면의 첫 렌더링 될때만 실행 , value 값이 바뀔 때 실행
  - 특이사항으로 value값이 빈 배열 일 경우엔 화면에 첫 렌더링 될 때만 실행

## 2.3 EX & clean up

```javascript
import "./styles.css";
import React, { useEffect, useState } from "react";

function App() {
  const [showTimer, setShowTimer] = useState(false);
  return (
    <div>
      {showTimer && <Timer />}
      <button
        onClick={() => {
          setShowTimer(!showTimer);
        }}
      >
        Toggle Timer
      </button>
    </div>
  );
}

function Timer(props) {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log("timer ing....");
    }, 1000);

    return () => {
      clearInterval(timer);
      console.log("timer fin");
    };
  }, []);

  return (
    <div>
      <span>Timer Start</span>
    </div>
  );
}

export default App;
```

- CleanUP 이란 개념은 useEffect() 에서 parameter 로 넣은 함수(위에선 timer)의 return 함수이다.
- 컴포넌트를 update 직후 , unmount 직전 특정 작업을 원한다면 반환해 주어야 한다.

# 3. useRef

# 3.1 용도

- 함수 컴포넌트에서 사용하면 오브젝트를 반환해준다.
- 컴포넌트 전 라이프사이클에 존재, Unmount 되기 전까지 유지된다.
- state와 비슷하게 저장공간으로 사용되지만, 값의 변화가 생겨도 렌더링이 발생하지 않고 그러므로 내부 변수가 변경되지 않는다.
- state의 변화가 일어나 렌더링이 발생해도 ref값은 유지
- DOM 요소에 접근하여

# 3.2 선언

```javascript
const ref = useRef(0);
```

-

# 3.3 Ex

```javascript
import "./styles.css";
import { useState, useRef } from "react";

function App() {
  const countRef = useRef(0);
  const [render, setRender] = useState(0);
  let countVar = 0;

  const doRendering = () => {
    setRender(render + 1);
  };

  const increaseRef = () => {
    countRef.current = countRef.current + 1;
    console.log("ref:" + countRef.current);
  };

  const increaseVar = () => {
    countVar = countVar + 1;
    console.log("var:" + countVar);
  };

  const printResults = () => {
    console.log(
      "ref:" + countRef.current + ", var:" + countVar + ", state:" + render
    );
  };

  return (
    <div className="App">
      <p>Var : {countVar}</p>
      <p>Ref: {countRef.current}</p>
      <p>State : {render}</p>
      <button onClick={increaseVar}>Var Up</button>
      <button onClick={increaseRef}>Ref Up</button>
      <button onClick={doRendering}>Redering</button>
      <button onClick={printResults}>print Result</button>
    </div>
  );
}

export default App;
///

function App() {
  const inputRef = useRef();

  useEffect(() => {
    console.log(inputRef);
    inputRef.current.focus();
  }, []);

  const login = () => {
    alert("come come!" + inputRef.current.value);
    inputRef.current.focus();
  };

  return (
    <div className="App">
      <input ref={inputRef} type="text" placeholder="username"></input>
      <button onClick={login}>Login</button>
    </div>
  );
}
```

- state와 ref 그래고 일반적인 변수의 렌더링시의 상호작용이 각각 다르다
- ref는 변화는 감지해야하지만 렌더링을 발생시키지 않으며 상태를 유지하고 싶을 때 사용
- DOM 요소에 접근하여 응용도 가능

# 4. useContext + Context API

## 4.1 용도

- 여러 컴포넌트로 만들어진 리액트앱은 props를 통해 부모에서 자식으로 데이터가 전달되는데 이 경우 컴포넌트들이 많아질 경우 공통 설정인 언어, 테마 등의 props도 계속 수송하면 너무 비효율적이다
- 이럴 때 전역 데이터를 여러 컴포넌트들끼리 공유를 쉽게 해준다.
- 사실 기본 useCotnext보다는 redux등의 외부 라이브러리를 더 많이 사용하는걸로 알고있다.
- 단 Context를 사용하면 컴포넌트를 재사용 하기 어려워 질수 있다.
- 공식문서상에선 Prop drilling을 피하기위해서라는 단순한 이유라면 컴포넌트 합성이 더 좋다라고 기재

## 4.2 선언

```javascript
export const ThemeContext = createContext(null);
// 1. 공유정보 보관을 위한 Context생성

<ThemeContext.Provider value={{val1,val2}}>
  <ChildComponent>
<ThemeContext.Provider>

// 2. App.js에서 Provider를 통하여 공유 할 원하는 컴포넌트 감싸기
// 3. value를 통해 공유할 데이터 props 설정

const data = useContext(ThemeContext);
// 4. 사용할 컴포넌트에서 useContext를 사용해 필요한 Context 호출

```

## 4.3 EX

```javascript
import "./styles.css";
import { useState, useRef, createContext, useContext } from "react";

const ThemeContext = createContext(null);
//선언시 null위치에 기본값설정이 가능한데 Provider로 전달값이 없을경우 기본값이 세팅된다 왠만하면 전달값을 줄것이므로 쓸일적음
function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    <ThemeContext.Provider value={{ isDark, setIsDark }}>
      <Page /** isDark = {isDark} setIsDark={setIsDark} */ />
    </ThemeContext.Provider>
  );
}

function Page({ isDark, setIsDark }) {
  const data = useContext(ThemeContext);
  console.log(data);
  return (
    <div className="page">
      <Header /**isDark={isDark} */ />
      <Content /**isDark={isDark} */ />
      <Footer /**isDark={isDark} setIsDark={setIsDark} */ />
    </div>
  );
}

function Header(/**{isDark} */) {
  const { isDark } = useContext(ThemeContext);
  return (
    <header
      className="header"
      style={{
        backgroundColor: isDark ? "black" : "lightgray",
        color: isDark ? "white" : "black",
      }}
    >
      <h1>Whelcome 홍길동!</h1>
    </header>
  );
}

function Content(/**{isDark} */) {
  const { isDark } = useContext(ThemeContext);
  return (
    <div
      className="content"
      style={{
        backgroundColor: isDark ? "black" : "lightgray",
        color: isDark ? "white" : "black",
      }}
    >
      <p>홍길동님, 좋은하루 되세요</p>
    </div>
  );
}

function Footer(/**{isDark,setIsDark} */) {
  const { isDark, setIsDark } = useContext(ThemeContext);

  const toggleTheme = () => {
    setIsDark(!isDark);
  };
  return (
    <footer
      className="footer"
      style={{
        backgroundColor: isDark ? "black" : "lightgray",
      }}
    >
      <p>홍길동님, 좋은하루 되세요</p>
      <button className="button" onClick={toggleTheme}>
        Dark Mode
      </button>
    </footer>
  );
}
export default App;
```
