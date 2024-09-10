---
layout: post
title: react-query
date: 2024-09-03 21:13 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---

> 휴가를 갔다오며 머리도 식히고 생각도 정리하였다. 애플코딩 리액트 관련 강의도 완강하였고 추가로 어떤 방향성으로 추가적으로 공부할지를 생각했다. 우선 강의는 추가적으로나 여러 목차들을 알아봤으나 목차부터 대부분 비슷했고 강의는 대부분 시간이 좀 지난 과거가 많았다.
> 실제 회사 프로젝트에서 사용한 리액트쿼리가 너무 간단히 설명되어 한번 더 상세히 써보고 싶었고 개념들을 채우고 앞부분의 까먹거나 약한 부분들을 채우며 뭔가를 보이는대로 만들어보며 익숙해 질 계획이다 결국은 익숙해져야 하는 기술이니까

# 1. React-query

- 리액트 어플리케이션에서 서버 데이터와의 동기화를 지원해주는 라이브러리
- useState, useEffect등 대부분의 상태 관리 라이브러리는 서버가 아닌 클라이언트 상태관리에 유용하며 비동기 또는 서버 상태관리에는 좋지 않기에 react-query를 사용한다.

- 「if(kakao)2021 - 카카오페이 프론트엔드 개발자들이 React Query를 선택한 이유」 세줄요약 🤟

1. React Query는 React Application에서 서버 상태를 불러오고, 캐싱하며, 지속적으로 동기화하고 업데이트하는 작업을 도와주는 라이브러리입니다.

2. 복잡하고 장황한 코드가 필요한 다른 데이터 불러오기 방식과 달리 React Component 내부에서 간단하고 직관적으로 API를 사용할 수 있습니다.

3. 더 나아가 React Query에서 제공하는 캐싱, Window Focus Refetching 등 다양한 기능을 활용하여 API 요청과 관련된 번잡한 작업 없이 “핵심 로직”에 집중할 수 있습니다.

# 1.1 server state vs client state

- client

  - 앱의 메모리에 존재하며 동기방식으로 접근 및 업데이트 한다.

- server
  - 원거에서 비동기 API방식으로 가져오거나 업데이트 한다.
  - 데이터를 다른이와 공유하며 누군가가 수정할 수 있다.
  - UI 데이터와 원격데이터가 맞지 않을수 있다.
  - 동일 데이터에 대한 중복 요청에 대해 캐싱 처리 및 성능 최적화가 어렵다.

# 1.2 리액트 쿼리의 선언 및 간결함

```javascript
//기존 server state 방식
import { useState, useEffect } from "react";
import axios from "axios";

export const SuperHeroesPage = () => {
  const [isLoading, setIsLoading] = useState(true);
  const [data, setData] = useState([]);
  const [error, setError] = useState("");

  useEffect(() => {
    axios
      .get("http://localhost:4000/superheroes")
      .then((res) => {
        setData(res.data);
        setIsLoading(false);
      })
      .catch((error) => {
        setError(error.message);
        setIsLoading(false);
      });
  }, []);

  if (isLoading) {
    return <h2>Loading...</h2>;
  }

  if (error) {
    return <h2>{error}</h2>;
  }

  return (
    <>
      <h2>Super Heroes Page</h2>
      {data.map((hero) => {
        return <div key={hero.name}>{hero.name}</div>;
      })}
    </>
  );
};
```

```javascript
//react-query를 사용한 client state 방식
import {
  useQuery,
  useMutation,
  useQueryClient,
  QueryClient,
  QueryClientProvider,
} from "@tanstack/react-query";
import axios from "axios";

const fetchSuperHeroes = () => {
  return axios.get("http://localhost:4000/superheroes");
};
export const RQSuperHeroesPage = () => {
  const { isLoading, isError, data, error } = useQuery({
    queryKey: ["super-heroes"],
    queryFn: fetchSuperHeroes,
  });

  if (isLoading) {
    return <h2>Loading....</h2>;
  }

  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  return (
    <>
      <h2>RQ Super Heroes Page</h2>
      {data?.data.map((hero) => {
        return <div key={hero.name}>{hero.name}</div>;
      })}
    </>
  );
};
```

- useState,useEffect를 사용할 때에 비해 선언해야하는 변수의 개수부터 눈에 띄게 줄었고 데이터 관리 로직,에러처리등이 눈에띄게 간편해 졌다.

## 1.3 Query Cache

- react-query의 기본 기능으로서 데이터를 캐싱하여 재로드 속도를 높인다
- 최초 useQuery를 사용하면 isLoading이 false에서 true가 되면 useQuery의 key를 이용해 쿼리객체를 만들고 쿼리객체안에 캐시정보가 저장된다.
- 그후 다른 페이지를 갔다가 다시 재요청이 들어올 때 쿼리객체 생성시 사용된 key를 사용해 재요청시 데이터가 캐시에 존재하는지 확인후 존재할 시 isLoading을 true로 만들고 즉시 반환한다. 데이터 가져오기가 완료되면 false로 변경된다.
- react-query는 캐시에서 가져온 데이터가 서버데이터가 업데이트되어 최신이 아닐수 있기에 캐시에 있는 데이터로 렌더링을 우선 적용하고 백그라운드에서 최신 데이터를 가져와 동기화한다. isFetching으로 확인가능
- useQuery의 3번째 인자로 캐시 유지시간 설정 가능
- 아래 두 인자로 네트워크 요청을 효율적으로 관리 가능
  - gcTime: 10, : 화면이 바뀌어도 캐시를 일정시간 가지고 있을 시간
  - staleTime: 5 \* 1000, 데이터의 변화가 많지않아 다시 가져올 필요가 없어 데이터 상태를 fresh로 지니고 있을 시간
- refetch 관련 설정값들로 새로고침 없이 실시간 데이터 반영 가능
