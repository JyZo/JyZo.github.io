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

## 1.2 선언 특징

```javascript
const [state, setState] = useState("초기값");
```

- state에 상태저장, setState로 state값을 변경
- setState로 변경할 때마다 화면이 재렌더링 된다

## 1.3 EX

```javascript
import "./styles.css";
import { useState } from "react";

export default function App() {
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
```
