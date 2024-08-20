---
layout: post
title: react-hook
date: 2024-07-30 00:38 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
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
import "./styles.css";
import { useState, useRef, createContext, useContext } from "react";

const ThemeContext = createContext(null);
// 1. 공유정보 보관을 위한 Context생성
<ThemeContext.Provider value={{ val1, val2 }}>
  <ChildComponent />
</ThemeContext.Provider>;
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
  // const [isDark, setIsDark] = useState(false);

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

# 5. useMemo

## 5.1 용도

- Memoization의 약어로 동일한 값을 리턴하는 함수를 반복적으로 호출해야한다면 그 함수 값을 캐시에 저장해 재사용하는 기법
- 함수형 컴포넌트는 함수로서 렌더링 -> 컴포넌트 함수 호출 -> 모든 내부 변수 초기화 과정을 거치는데 useMemo를 사용하면 함수 호출시 값을 저장해 재사용하게 해준다.

## 5.2 선언

```javascript
const value = useMemo(() => {
  return calculate();
}, [item]);
```

- 첫번째 인자인 콜백함수는 메모이제이션 해줄 값을 계산해 리턴(useMemo return 값)
- 두번째 인자인 배열은 배열 요소값이 업데이트 될때만 콜백함수를 호출해 메모이제이션 값을 업데이트 해준다., 빈 배열이면 mount시 최초 계산된 값을 계속 사용

## 5.3 EX

```javascript
import "./styles.css";
import React, {useState, useMemo} from "react";

const hardCalculate = (number) => {
  console.log('hard cal');
  for(let i = 0; i<9999; i++){
    for(let j = 0; j<9999; j++){
    }
  }
  return number + 10000;
}
const easyCalculate = (number) => {
  console.log('easy cal');
  return number + 1;
}

function App() {
  const [hardNumber, setHardNumber] = useState(1);
  const [easyNumber, setEasyNumber] = useState(1);

  // const hardSum = hardCalculate(hardNumber);
  const hardSum = useMemo(() => {
    return hardCalculate(hardNumber);
  },[hardNumber])

  const easySum = easyCalculate(easyNumber);

  return (
    <div>
      <h3>hard calculator</h3>
      <input
        type='number'
        value={hardNumber}
        onChange={(e) => {
          setHardNumber(parseInt(e.target.value));
        }}
      />
      <span> + 10000 = {hardSum} </span>

      <h3>easy calculator</h3>
      <input
        type='number'
        value={easyNumber}
        onChange={(e) => {
          setEasyNumber(parseInt(e.target.value));
        }}
      />
      <span> + 1 = {easySum} </span>
    </div>
  );
}
export default App;

//EX2
import "./styles.css";
import React, {useState, useMemo,useEffect} from "react";

function App() {
  const [number, setNumber] = useState(0);
  const [isKorea, setIsKorea] = useState(true);

  // const location = {
  //   country: isKorea ? '한국' : '외국'
  // }
  const location = useMemo(() => {
    return{
      country: isKorea ? '한국' : '외국'
    }
  },[isKorea])
  useEffect(() => {
    console.log('useeffect');
  },[location]);

  return (
    <div>
     <h2>하루에 몇끼 먹어요?</h2>
     <input
      type='number'
      value={number}
      onChange={(e) => {
        setNumber(e.target.value)
      }}
     />
     <hr />
     <h2>어느 나라에 있어요?</h2>
     <p>나라 : {location.country}</p>
     <button onClick = {() => {
       setIsKorea(!isKorea)
     }}>비행기타자</button>
    </div>
  );
}
export default App;
```

- EX2에서 사용 목적은 자바스크립트 자료형에는 원시타입과 객체타입이 있는데 객체 타입의 경우 실제 값이 아닌 메모리의 주소값이 저장된다, 그래서 unumber 값이 변경되어 재 렌더링될 경우 주소값이 바뀌어 의도하지 않게 useEffect가 실행, 그래서 useMemo로 주소값 재렌더링을 막아줌

# 6. useCallback

## 6.1 용도

- useMemo처럼 메모이제이션을 이용해 컴포넌트 최적화가 목적이지만 약간의 차이를 지니고 있다.
  - useMemo는 메모이제이션된 값을 반환하나 useCallback은 함수를 반환
  - useMemo는 계산 비용이 큰 연산을 최적화하는데 자주사용(큰 데이터 가공 및 복잡한 연산),useCallback은 불필요한 함수 재생성을 방지하는데 자주 사용(자식 컴포넌트에 전달되는 함수를 최적화)

## 6.2 선언

```javascript
const value = useCallback(() => {
  return calculate();
}, [item]);
```

- 첫번째 인자인 콜백함수는 메모이제이션 해줄 함수를 리턴
- 두번째 인자인 배열은 배열값이 변경 될 때 함수를 다시 메모이제이션하게 해준다.

## 6.3 EX

```javascript
import "./styles.css";
import React, {useState, useCallback,useEffect} from "react";

function App() {
  const [number, setNumber] = useState(0);
  const [toggle, setToggle] = useState(true);

  const someFunction = useCallback(() =>{
    console.log('someFunc:number:' +number);
    return;
  },[number]);

  useEffect(() => {
    console.log('change someFunc');
  },[someFunction])

  return (
    <div>
      <input
        type='number'
        value={number}
        onChange={(e) => {
          setNumber(e.target.value);
        }}
      />
      <br/>
      <button onClick={() => {
        setToggle(!toggle);
      }}>{toggle.toString()}</button>
      <button onClick={someFunction}>Call someFunc</button>
    </div>
  );
}
export default App;

//EX2
import "./styles.css";
import React, {useState, useCallback,useEffect} from "react";

function App() {
  const [size, setSize] = useState(100);
  const [isDark,setIsDark] = useState(false);

  const createBoxStyle = useCallback(() => {
    return {
      backgroundColor: 'pink',
      width : size+'px',
      height : size+'px'
    }
  },[size])

  return (
    <div style={{
      background : isDark ? 'black' : 'white',
    }}>
      <input
        type='number'
        value={size}
        onChange={(e) => {
          setSize(e.target.value);
        }}
      />
      <button onClick={() => setIsDark(!isDark)}>change theme</button>
      <Box createBoxStyle={createBoxStyle}/>
    </div>
  );
}

function Box({createBoxStyle}) {
  const [style, setStyle] = useState({});

  useEffect(() => {
    console.log('change box');
    setStyle(createBoxStyle);
  }, [createBoxStyle])
  return (
    <div style = {style}></div>
  );
}

export default App;
```

# 7. useReducer

## 7.1 용도

- 컴포넌트의 state를 생성 및 관리를 위해 useState를 사용해왔지만 state관리를 위한 다른 hook
- state를 생성하고 관리할 수 있게 해주는건 동일하지만 여러 하위값을 포함하는 복잡한 state를 다뤄야 할때 사용, 다음 3가지로 구성
  - Reducer : state를 update해주는 역할
  - Dispatch : state변경을 위해 Reducer에게 요청하는 것
  - Action : 요청하는 행위의 내용

## 7.2 선언

```javascript
const reducer = ([state, dispatch] = useReducer(reducer, initVal));

const reducer = (state, action) => {};
```

- 첫번째 인자로 state, 두번째로 reducer가 만들어준 dispatch를 받는다
- useReducer의 첫번째 인자는 reducer를 두번째 인자는 초기값을 받는다.
- 선언한 reducer에서 state와 action을 전달받아 분기하여 처리

## 7.3EX

```javascript
import "./styles.css";
import React, {useState, useReducer} from "react";

const ACTION_TYPES = {
  deposit: 'deposit',
  withdraw: 'withdraw'
}
const reducer = (state, action) => {
  console.log('reducer start',state,action);
  switch(action.type){
    case ACTION_TYPES.deposit:
      return state+action.payload;
    case ACTION_TYPES.withdraw:
      return state-action.payload;
    default:
      return state;
  }
}

function App() {
  const [number, setNumber] = useState(0);
  const [money,dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>useReducer 은행에 오신걸 환영합니다.</h2>
      <p>잔고 : {money}원</p>
      <input
        type='number'
        value={number}
        onChange={(e) => {
          setNumber(parseInt(e.target.value));
        }}
        step='1000'
      />
      <button onClick={() => {
        dispatch({type:ACTION_TYPES.deposit, payload: number});
      }}>예금</button>
      <button onClick={() => {
        dispatch({type:ACTION_TYPES.withdraw, payload: number});
      }}>출금</button>
    </div>
  );
}

export default App;

//EX
import "./styles.css";
import React, {useState, useReducer} from "react";

const reducer = (state, action) => {
  console.log('reducer start',state,action);
  switch(action.type){
    case 'add-student':
      const name = action.payload.name;
      const newStudent ={
        id: Date.now(),
        name: name,
        isHere: false,
      }
      return {
        count: state.count+1,
        students: [...state.students, newStudent],
      }
    case 'delete-student':
      console.log(action.payload.id);
      return{
        count: state.count - 1,
        students: state.students.filter(
          (student) => student.id !== action.payload.id
        ),
      }
    case 'mark-student':
      return{
        count: state.count,
        students: state.students.map(student => {
          if(student.id === action.payload.id){
            return {...student, isHere: !student.isHere};
          }
          return student;
        })
      }
    default :
      return state;
    }
};


const initialState = {
  count: 0,
  students: [],
};

function App() {
  const [name, setName] = useState('');
  const [studentsInfo,dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h1>출석부</h1>
      <p>총 학생 수 : {studentsInfo.count}</p>
      <input
        type='text'
        placeholder='이름을입력해주세요'
        value={name}
        onChange={(e) => {
          setName(e.target.value);
        }}
      />
      <button onClick={() => {
        dispatch({type:'add-student', payload: {name}});
      }}>추가</button>
      {studentsInfo.students.map((student) => {
        return <Student key={student.id} name={student.name} dispatch={dispatch} id={student.id} isHere={student.isHere}/>
      })}
    </div>
  );
}

function Student({name,dispatch,id,isHere}){
  console.log(name);
  return(
    <div>
      <span style={{
        textDecoration: isHere ? 'line-through' : 'none',
        color: isHere ? 'gray' : 'black',
      }}
      onClick={() => {
        dispatch({type: 'mark-student', payload:{id}})
      }}>{name}</span>
      <button onClick={() =>{
        dispatch({type:'delete-student',payload: {id}})
      }
      }>삭제</button>
    </div>
  )
}

export default App;
```

# 8. React.memo

## 8.1 용도

- 반복이 필요없는 불필요한 렌더링이 일어나는 컴포넌트를 최적화
- 리액트에서 제공하는 고차 컴포넌트(HOC),어떤 컴포넌트를 인자로 받아서 새로운 최적화된 컴포넌트를 반환해주는 컴포넌트
- 자신이 받는 props의 변화가 있을때 만 렌더링 하는 방식
- 컴포넌트가 같은 Props로 자주 렌더링 될 때, 컴포넌트가 렌더링이 될 때마다 복잡한 로직을 처리해야 할 때 최적화를 위해 사용

## 8.2 선언

```javascript
//표현식
const Child = memo(({ name }) => {});
//선언식
function Child(props) {}
export default memo(Child);
```

- React.memo는 props의 변화에만 반응하며 표현식 선언식 사용방법이 약간의 차이가 있다.

## 8.3 EX

```javascript
import "./styles.css";
import React, { useState, memo, useMemo, useCallback } from "react";

function App() {
  const [parentAge, setParentAge] = useState(0);
  // const [childAge, setChildAge] = useState(0);

  const incrementParentAge = () => {
    setParentAge(parentAge + 1);
  };

  // const incrementChildAge = () => {
  //   setChildAge(childAge + 1);
  // };

  console.log("parent redering");
  const name = useMemo(() => {
    return {
      lastName: "홍",
      firstName: "길동",
    };
  }, []);

  return (
    <div
      style={{
        border: "2px solid navy",
        padding: "10px",
      }}
    >
      <h1>부모</h1>
      <p>age: {parentAge}</p>
      <button onClick={incrementParentAge}>부모 나이 증가</button>
      {/* <button onClick={incrementChildAge}>자녀 나이 증가</button> */}
      <Child /*name={'홍길동'} age={childAge}*/ name={name} />
    </div>
  );
}
const Child = memo(({ name }) => {
  console.log("child redering");
  return (
    <div
      style={{
        border: "2px solid powderblue",
        padding: "10px",
      }}
    >
      <h3>자녀</h3>
      <p>성: {name.lastName}</p>
      <p>이름: {name.firstName}</p>
      {/* <p>name: {name}</p> */}
      {/* <p>age: {age}</p> */}
    </div>
  );
});

export default App;
```

# 9. Custom Hooks

## 9.1 용도

- 내가 원하는 인터페이스와 기능을 담은 Custom Hooks를 만들수있음
- 중복된 코드를 제거하는 용도로 사용할 때 유용
- Custom hook 안에 다른 리액트 훅들을 자유롭게 사용할 수 있으며 사용하는 컴포넌트마다 state,effect는 독립적이다.

## 9.2 선언

## 9.3 EX

```javascript
//분리된 커스텀 훅 js
import {useState} from 'react';

export function useInput(initialValue,submitAction){
    const [inputValue, setInputValue] = useState(initialValue);

    const handleChange = (e) =>{
        setInputValue(e.target.value);
    };

    const handleSubmit = () =>{
         setInputValue('');
        submitAction(inputValue);
    };

    return [inputValue, handleChange,handleSubmit];
}


import "./styles.css";
import React, { useState, memo, useMemo, useCallback } from "react";
import {useInput} from './useInput';

function displayMessage(message){
    alert(message)
}
function App() {
    const [inputValue, handleChange,handleSubmit] = useInput('',displayMessage );
  return (
    <div>
      <h1>useInput</h1>
    <input value={inputValue} onChange={handleChange} />
        <button onClick={handleSubmit}>확인</button>
    </div>
  );
}

export default App;

//EX2
//분리된 커스텀 훅 js
import {useState,useEffect} from 'react';
export function useFetch(baseUrl, initialType) {
    const [data,setData] = useState(null);

    const fetchUrl = (type) => {
        fetch(baseUrl + '/' + type)
      .then((res) => res.json())
      .then((res) =>setData(res));
    }

  useEffect(() => {
    fetchUrl(initialType)
  }, [])
    return {
        data,
        fetchUrl,
    };
}

import "./styles.css";
import React, { useState, memo, useMemo, useCallback,useEffect } from "react";
import {useFetch} from './useFetch';

const baseUrl = 'https://jsonplaceholder.typicode.com';

function App() {
    const {data: userData} = useFetch(baseUrl,'users');
    const {data: postData} = useFetch(baseUrl,'posts');

  return (
    <div>
      <h1>User</h1>
        {userData && <pre>{JSON.stringify(userData[0],null,2)}</pre>}
      <h1>Post</h1>
        {postData && <pre>{JSON.stringify(postData[0],null,2)}</pre>}
    </div>
  );
}

export default App;
```

# 10. useId

## 10.1 용도

- 고유한 ID를 만들 때 사용하는 hook

## 10.2 선언

```javascript
const id = useId();
```

- 일반적인 hook사용법 처럼 import하고 사용하면 끝
- 아무런 인자도 전달받지 않음

## 10.3 EX

```javascript
import "./styles.css";
import React, {
  useState,
  memo,
  useMemo,
  useCallback,
  useEffect,
  useId,
} from "react";

function App() {
  return (
    <div>
      <MyInput />
    </div>
  );
}

function MyInput() {
  const id = useId();
  return (
    <div>
      <label htmlFor={id + "name"}>이름</label>
      <input id={id + "name"} />
      <br />
      <label htmlFor={id + "age"}>이름</label>
      <input id={id + "age"} />
    </div>
  );
}

export default App;
```

- useID로 만들 경우 다음과 같은 장점이 있다
  - 항상 id값에 :을 표현하고 있는데 이 :이 포함되면 쿼리셀렉터 등이 잘 작동하지 않는데 외부 API없이 리액트로 더 나은 코드 작성 도움
  - 컴포넌트가 렌더링 될 때마다 초기화가 되지 않아 안정감이 있다.
  - 서버사이드 렌더링 시 서버사이드와 클라이언트사이드에서 동일한 안정적인 ID를 생성

# 11. useLayoutEffect

## 11.1 용도

- useEffect와 목적도 용도도 비슷하다
- 차이점이 있다면 Effect가 실행되는 시점
  - useEffect : 화면 업데이트 -> effect 실행, 컴포넌트가 화면에 그려진 이후 실행, 비동기적으로 실행
  - useLayoutEffect : effect 실행 -> 화면 업데이트, 컴포넌트가 화면에 그려지기 이전에 실행, 동기적으로 실행
- 사용자에게 보여주는 UI변화를 더 정교하게 다룰 수 있다.
- 컴포넌트를 화면에 배치하기 전에 레이아웃 같은 UI적 계산을 해야 할 때 사용

## 11.2 선언

```javascript
useLayoutEffect(() => {
  //작업
});

useLayoutEffect(() => {
  //작업
}, [value]);
```

- 첫번째 인자로 콜백, 두번째 인자로 의존성 배열 useEffect와 동일
-

## 11.3 EX

```javascript
import "./styles.css";
import React, {useState,memo,useMemo,useCallback,useEffect,useId,useLayoutEffect} from "react";

function App() {
  const [count, setCount] = useState(0);

  const handleCountUpdate =() => {
    setCount(count+1);
  }

  useLayoutEffect(() => {
    console.log('useLayoutEffect',count);
  },[count])

  useEffect(() => {
    console.log('useEffect',count);
  },[count])


  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleCountUpdate}>Update</button>
    </div>
  );
}

export default App;

//EX
import "./styles.css";
import React, {useState,memo,useMemo,useCallback,useEffect,useId,useLayoutEffect,useRef} from "react";

function getNumbers() {
  return [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15];
}
function App() {
  const [numbers,setNumbers] = useState([]);
  const ref = useRef(null);

  useLayoutEffect(() => {
    const nums = getNumbers();
    console.log(nums);
    setNumbers(nums);
  }, []);

  useLayoutEffect(() => {
    if(numbers.length === 0){
      return;
    }

    for(let i=0;i<3000000; i++){}

    ref.current.scrollTop = ref.current.scrollHeight;
  }, [numbers]);

  return (
    <div
      ref={ref}
      style={{
        height: '300px',
        border: '2px solid blue',
        overflow: 'scroll'
      }}
      >
      {numbers.map((number,idx) => (
        <p key={idx}>{number}</p>
      ))}
    </div>
  );
}

export default App;

```

- EX2처럼 미리 계산을 다 끝내고 렌더링을 하기 때문에 UI를 사용자에게 바로 보여줄수 있어 딜레이가 개선된다.

# 11. Debounce

## 11.1 용도

- 함수가 너무 자주 호출되는걸 방지하고, 이벤트가 발생할 때 호출횟수에 제한을 두는것
- 이벤트가 연속적으로 발생할 때, 제일 마지막 이벤트가 발생한 후 일정시간이 지난 후에 함수를 호출

## 11.2 EX

```javascript
//Debounce 커스텀 훅 분리
import { useState, useEffect } from "react";
export function useDebounce(value, delay) {
  const [debouncedValue, setdebouncedValue] = useState(value);

  useEffect(() => {
    const timerID = setTimeout(() => {
      console.log("callback");
      setdebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(timerID);
    };
  }, [value, delay]);
  return debouncedValue;
}

import "./styles.css";
import React, {
  useState,
  memo,
  useMemo,
  useCallback,
  useEffect,
  useId,
  useLayoutEffect,
  useRef,
} from "react";
import { useDebounce } from "./debounce";

function fetchDataFromServer(value) {
  if (!value) {
    return [];
  }
  console.log("getdata");
  const users = [
    { name: "김철수", age: "16" },
    { name: "이영희", age: "26" },
    { name: "김민수", age: "15" },
    { name: "홍길동", age: "20" },
    { name: "홍민영", age: "45" },
    { name: "김민영", age: "32" },
  ];
  return users.filter((user) => user.name.startsWith(value));
}

function App() {
  const [input, setInput] = useState("");
  const debouncedInput = useDebounce(input, 1000);
  const [result, setResult] = useState([]);

  useEffect(() => {
    const users = fetchDataFromServer(debouncedInput);
    setResult(users);
    console.log(users);
  }, [debouncedInput]);

  return (
    <div class="container">
      <div class="search-container">
        <input
          placeholder="여기다 검색하세요"
          value={input}
          onChange={(e) => {
            setInput(e.target.value);
          }}
        />
        <ul>
          {result.map((user) => (
            <li key={user.name}>
              <span>{user.name}</span>
              <span>{user.age} 세</span>
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```
