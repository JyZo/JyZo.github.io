---
layout: post
title: react-sidebar
date: 2023-12-08 03:29 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---

# 1. 사이드바 만들기
사이드바 만들어보기 제안을 받아서 컴포넌트들의 개념 및 사용법을 익히기에도 좋다고 판단되고 우선 사이드바를 만들어보면서 react를 사용해보기로 했다.

## 1. React-router-dom 설치
리액트는 기본적으로 SPA(Single Page Application)을 지향하고 페이지의 최초 로드 후 동적으로 페이지를 변경하기 위해서는 라우팅이 필수이다. 

구현하려는 사이드바는 메뉴에 따라서 바뀌므로 사용해보기 딱 좋은 기회이다.

우선 react-router-dom 외에 next.js를 사용할 수도 있다고 하나 아직은 초보스럽게 기본적인 방법을 사용해보려한다. 우선 라이브러리를 npm으로 설치해 주었다.

> npm install react-router-dom

설치가 무사히 완료되었다.

## 2. 컴포넌트 구상
