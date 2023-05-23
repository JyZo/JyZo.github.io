---
layout: post
title: duplication
date: 2023-05-23 23:42 +0900
categories: [Tip, Knowledge]
tags: [Tip, knowledge]
---


# 이중화(duplication)


- ### 서버 인프라 운영시 서비스가 중단되는 다운타임(downtime)을 최소화 하기 위해 운영 
- ### 이중화는 시스템에 장애가 발생할 것을 대비해서 동일한 기능을 수행하는 예비 시스템을 동시에 운용하는 행위
- ### 다운타임이 거의 없이 서비스를 지속할 수 있으나 초기 구성이 복잡하고, 운영 비용이 높음

<br/>
<br/>

# 이중화의 방식

## 1. Active - Standby

![HA1_AS](/assets/img/post_img/HA1_AS.JPG "HA1_AS")

- 동일한 두 벌의 시스템을 만들어 두되, 하나의 시스템(Active)으로만 운영하며, 운영 시스템에 장애가 발생할 경우 다른 시스템(Standby)으로 즉시 전환하는 방식
- 클러스터로 연결된 모든 서버는 hearbeat로 상태를 주고받음
- Active에서 장애 발생 시 클러스터가 Standby점수가 더 높은 서버로 서비스 이관
- 한 벌의 시스템이 대기 상태로 있어 자원의 비효율성 발생

<br/>

## 2. Active - Active

![HA1_AA](/assets/img/post_img/HA1_AA.JPG "HA1_AA")

- 동일한 두 벌의 시스템을 같이 운영하는 형태이며, 하나의 시스템에 장애가 생기면 장애가 발생하지 않은 나머지 하나의 시스템으로만 가동하는 방식
- Active - Standby 보다 더 높은 처리량을 가질 수 있지만 장애발생 시 나머지 장비에 부하가 커져 장애 확대 우려
- Active - Standby 보다 더 높은 처리량을 갖는 서버나 더 많은 대수로 구성하는것이 안전
- 장애 대응 뿐만 아니라 시스템의 부하를 줄이거나 개발·테스트의 편의를 위해서도 사용

<br/>
<br/>

## 3. 비교표

![AAVSAS](/assets/img/post_img/AAVSAS.PNG "AAVSAS")





<br/>


#

출처 - [[https://tech.gluesys.com/blog/2020/08/22/HA_1_intro.html](https://www.youtube.com/@dongbinna)]  

출처 - [[https://haeunyah.tistory.com/122](https://haeunyah.tistory.com/122)]  

출처 - [[http://wiki.hash.kr/index.php/%EC%95%A1%ED%8B%B0%EB%B8%8C-%EC%8A%A4%ED%83%A0%EB%B0%94%EC%9D%B4](http://wiki.hash.kr/index.php/%EC%95%A1%ED%8B%B0%EB%B8%8C-%EC%8A%A4%ED%83%A0%EB%B0%94%EC%9D%B4)]  




