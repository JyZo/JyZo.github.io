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
