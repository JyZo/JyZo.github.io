---
layout: post
title: React setting
date: 2023-12-05 23:58 +0900
author: JyZo
categories: [Front, React]
tags: [Front, React]
math: true
---


>말로만 듣던 React를 한번 누군가 가이드 해줄 기회가 생겨 디테일한 부분은 
추후에 더 자세히 보고 복습 및 놓치거나 모르는 부분들을 빠르게 훓고 간단한 토이 프로젝트를 해보며 과정을 기록해 보려고 한다. 


# 1. Node.js 설치

우선 공식 홈페이지에 들어가면

>사용자 인터페이스를 만들기 위한 JavaScript 라이브러리

이렇게 소개를 하고 있고 웹에서 하는 방법과 로컬에서 하는 두가지 방법을 제안하고 있는데 로컬에서 할 경우 Node.js 설치를 우선적으로 요구하고 있었다.

---

## 1. Node.js
그래서 설치하게 된 Node.js 역시 간단하게 검색할 경우 공식 페이지에서 한마디로 간단히 설명을 해주고 있다.

>Node.js®는 오픈 소스, 크로스 플랫폼 JavaScript 런타임 환경입니다.

그래서 우선 리액트 환경을 구성하기 위해 Node.js 홈페이지에 들어가 가장 최신의 LTS 를 다운받아 설치하였다.

Node.js[[https://nodejs.org/en]

설치는 그냥 next만 눌러 기본값으로 빠르게 설치하였다

<br/>

## 2. NPM(Node Package Manager)
Node.js를 설치하게 되면 기본적으로 설치되는 패키지 매니저라고 하며 라이브러리인 React앱을 만들때 노드 패키지를 설치하고 프로젝트를 관리할 수 있도록 도움을 준다.


<br/>

![node&npm-v.PNG](/assets/img/post_img/node&npm-v.PNG "node&npm-v")

다음과 같이 정상적으로 설치된 것을 확인할 수 있었다.


## 3. Project 생성
처음 여러 블로그들이나 검색을 하던 중 프로젝트 생성을 당연히 무난하게 명령어를 입력했다.

프로젝트를 생성하는 방법은 두가지가 있는데  

1)패키지 전역으로 설치
>npm -g create-react-app react-project

2)패키지 설치 없이 진행
>npx create-react-app react-project

대부분 두번째 방법을 선호하기에 나도 두번째 방법으로 했는데 에러가 발생

원인은 node.js와 npm npx등은 설치되어있었으나 프로젝트를 생성하기 위한 create-react-app이 설치되어 있지 않아서였고 꽤나 허무했다.

> npm install -g create-react-app

으로 앱을 설치하고 나니 정상적으로 프로젝트가 생성되었다.





