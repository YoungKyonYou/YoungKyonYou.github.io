---
layout: post
title: NoSQL이란?
date: 2022-01-11 11:20:00 0000
tags: [NoSQL]
categories: [Interview]
description: NoSQL이란?
---

<br><br>

_**오늘의 나보다 성장한 내일의 나를 위해...**_

<br>

<br><br>

<style>
.containercoffee {
  width: 300px;
  height: 280px;
  position: relative;
  top: calc(50% - 140px);
  left: calc(50% - 150px);
}
.coffee-header {
  width: 100%;
  height: 80px;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #ddcfcc;
  border-radius: 10px;
}
.coffee-header__buttons {
  width: 25px;
  height: 25px;
  position: absolute;
  top: 25px;
  background-color: #282323;
  border-radius: 50%;
}
.coffee-header__buttons::after {
  content: "";
  width: 8px;
  height: 8px;
  position: absolute;
  bottom: -8px;
  left: calc(50% - 4px);
  background-color: #615e5e;
}
.coffee-header__button-one {
  left: 15px;
}
.coffee-header__button-two {
  left: 50px;
}
.coffee-header__display {
  width: 50px;
  height: 50px;
  position: absolute;
  top: calc(50% - 25px);
  left: calc(50% - 25px);
  border-radius: 50%;
  background-color: #9acfc5;
  border: 5px solid #43beae;
  box-sizing: border-box;
}
.coffee-header__details {
  width: 8px;
  height: 20px;
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #9b9091;
  box-shadow: -12px 0 0 #9b9091, -24px 0 0 #9b9091;
}
.coffee-medium {
  width: 90%;
  height: 160px;
  position: absolute;
  top: 80px;
  left: calc(50% - 45%);
  background-color: #bcb0af;
}
.coffee-medium:before {
  content: "";
  width: 90%;
  height: 100px;
  background-color: #776f6e;
  position: absolute;
  bottom: 0;
  left: calc(50% - 45%);
  border-radius: 20px 20px 0 0;
}
.coffe-medium__exit {
  width: 60px;
  height: 20px;
  position: absolute;
  top: 0;
  left: calc(50% - 30px);
  background-color: #231f20;
}
.coffe-medium__exit::before {
  content: "";
  width: 50px;
  height: 20px;
  border-radius: 0 0 50% 50%;
  position: absolute;
  bottom: -20px;
  left: calc(50% - 25px);
  background-color: #231f20;
}
.coffe-medium__exit::after {
  content: "";
  width: 10px;
  height: 10px;
  position: absolute;
  bottom: -30px;
  left: calc(50% - 5px);
  background-color: #231f20;
}
.coffee-medium__arm {
  width: 70px;
  height: 20px;
  position: absolute;
  top: 15px;
  right: 25px;
  background-color: #231f20;
}
.coffee-medium__arm::before {
  content: "";
  width: 15px;
  height: 5px;
  position: absolute;
  top: 7px;
  left: -15px;
  background-color: #9e9495;
}
.coffee-medium__cup {
  width: 80px;
  height: 47px;
  position: absolute;
  bottom: 0;
  left: calc(50% - 40px);
  background-color: #FFF;
  border-radius: 0 0 70px 70px / 0 0 110px 110px;
}
.coffee-medium__cup::after {
  content: "";
  width: 20px;
  height: 20px;
  position: absolute;
  top: 6px;
  right: -13px;
  border: 5px solid #FFF;
  border-radius: 50%;
}
@keyframes liquid {
  0% {
    height: 0px;  
    opacity: 1;
  }
  5% {
    height: 0px;  
    opacity: 1;
  }
  20% {
    height: 62px;  
    opacity: 1;
  }
  95% {
    height: 62px;
    opacity: 1;
  }
  100% {
    height: 62px;
    opacity: 0;
  }
}
.coffee-medium__liquid {
  width: 6px;
  height: 63px;
  opacity: 0;
  position: absolute;
  top: 50px;
  left: calc(50% - 3px);
  background-color: #74372b;
  animation: liquid 4s 4s linear infinite;
}
.coffee-medium__smoke {
  width: 8px;
  height: 20px;
  position: absolute;  
  border-radius: 5px;
  background-color: #b3aeae;
}
@keyframes smokeOne {
  0% {
    bottom: 20px;
    opacity: 0;
  }
  40% {
    bottom: 50px;
    opacity: .5;
  }
  80% {
    bottom: 80px;
    opacity: .3;
  }
  100% {
    bottom: 80px;
    opacity: 0;
  }
}
@keyframes smokeTwo {
  0% {
    bottom: 40px;
    opacity: 0;
  }
  40% {
    bottom: 70px;
    opacity: .5;
  }
  80% {
    bottom: 80px;
    opacity: .3;
  }
  100% {
    bottom: 80px;
    opacity: 0;
  }
}
.coffee-medium__smoke-one {
  opacity: 0;
  bottom: 50px;
  left: 102px;
  animation: smokeOne 3s 4s linear infinite;
}
.coffee-medium__smoke-two {
  opacity: 0;
  bottom: 70px;
  left: 118px;
  animation: smokeTwo 3s 5s linear infinite;
}
.coffee-medium__smoke-three {
  opacity: 0;
  bottom: 65px;
  right: 118px;
  animation: smokeTwo 3s 6s linear infinite;
}
.coffee-medium__smoke-for {
  opacity: 0;
  bottom: 50px;
  right: 102px;
  animation: smokeOne 3s 5s linear infinite;
}
.coffee-footer {
  width: 95%;
  height: 15px;
  position: absolute;
  bottom: 25px;
  left: calc(50% - 47.5%);
  background-color: #41bdad;
  border-radius: 10px;
}
.coffee-footer::after {
  content: "";
  width: 106%;
  height: 26px;
  position: absolute;
  bottom: -25px;
  left: -8px;
  background-color: #000;
}
</style>

<div class="containercoffee">
    <div class="coffee-header">
      <div class="coffee-header__buttons coffee-header__button-one"></div>
      <div class="coffee-header__buttons coffee-header__button-two"></div>
      <div class="coffee-header__display"></div>
      <div class="coffee-header__details"></div>
    </div>
    <div class="coffee-medium">
      <div class="coffe-medium__exit"></div>
      <div class="coffee-medium__arm"></div>
      <div class="coffee-medium__liquid"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-one"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-two"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-three"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-for"></div>
      <div class="coffee-medium__cup"></div>
    </div>
    <div class="coffee-footer"></div>
</div>

<br><br><br><br><br><br><br><br>

<br>

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> NoSQL</h2>
<br>

<span style="background: rgb(251,243,219)">NoSQL</span>은 <span style="background: rgb(251,243,219)">RDBMS</span>의 형태가 아닌 <span style="background: rgb(251,243,219)">일관성 모델(비관계형 모델)</span>을 이용하는 데이터 저장을 말하는 것이다.
<span style="background: rgb(251,243,219)">NoSQL</span> 데이터베이스는 기존의 관계형 데이터베이스보다 더 융통성 있는 데이터 모델을 사용하고 데이터의 저장 및 검색을 위한 특화된 메커니즘을 제공한다.

이를 통해 <span style="background: rgb(251,243,219)">NoSQL</span> 데이터베이스는 단순 검색 및 추가작어베 있어서 매우 최적화된 키 값 저장 기법을 사용하여 <span style="background: rgb(251,243,219)">응답속도나 처리효율</span> 등에 있어서 매우 뛰어난 성능을 나타낸다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> NoSQL의 특징
</h3>

<br>

**1)** <span style="background: rgb(251,243,219)">관계형 모델</span>을 사용하지 않으며 테이블 간 연결해서 조회할 수 있는 <span style="background: rgb(251,243,219)">조인 기능이</span> 없다.

**2)** <span style="background: rgb(251,243,219)">데이터 조회</span>를 위해 직접 프로그래밍하는 등의 <span style="background: rgb(251,243,219)">비SQL 인터페이스</span>를 통한 데이터 접근

**3)** 대부분 <span style="background: rgb(251,243,219)">여러 데이터베이스 서버를 묶어서(클러스터링)</span> 하나의 데이터베이스를 구성

**4)** <span style="background: rgb(251,243,219)">관계형 데이터베이스</span>에서는 지원하는 <span style="background: rgb(251,243,219)">데이터 처리 완결성(Trascation, ACID 지원)</span>이 보장되지 않음

**5)** 데이터의 스키마와 속성들을 다양하게 수용하고 동적으로 정의(Schemaless)

**6)** 데이터베이스의 중단없는 서비스와 자동 복구 기능 지원

**7)** 대다수의 제품이 <span style="background: rgb(251,243,219)">Open Source</span>로 제공

**8)** 대다수의 제품이 <span style="background: rgb(251,243,219)">고확장성, 고가용성, 고성능</span> 특징을 가진다.

**9)** 관계형 데이터베이스보다 훨씬 다양한 방식으로 <span style="background: rgb(251,243,219)">빠르게 바뀌는 대량의 비정형 데이터</span>를 처리할 수 있음

<br>

정리하면 <span style="background: rgb(251,243,219)">NoSQL</span>은 <span style="background: rgb(251,243,219)">초고용량 데이터 처리</span>등 <span style="background: rgb(251,243,219)">성능에 특화</span>된 목적을 위해 비 관계형 데이터 저장소에 비 구조적인 데이터를 저장하기 위한 분산저장 시스템이라고 볼 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 대표적인 NoSQL
</h3>

<br>

- **key-value Database**
  - Riak, Redis, Voldmort
- **Document Database**
  - MongoDB, CouchDB
- **BigTable Database**
  - Hbase, Casandra
- **Graph Database**
  - Sones, AllegroGraph

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> NoSQL의 장점
</h3>

<br>

- RDBNS에 비해 저렴한 비용으로 **분산 처리와 병렬 처리**가 가능
- **비정형 데이터 구조 설계**로 설계 비용이 감소
- 관계형 데이터베이스의 **relation과 join** 구조를 **linking과 embedded**로 구현하여 성능이 빠름
- **Big Data** 처리에 효과적
  - 많은 서버로 확장이 가능(데이터 중복이 생기더라도 테이블을 정규화 시키지 않아도 큰 테이블에 담아 저장)
- **가변적인 구조**로 데이터 저장이 가능
- **Scale out** 구조를 채댁하여 서버 확장에 용이하며 더 많은 데이터를 저장
- **Document based(Schema-less)** 구조로 데이터 모델의 유연한 변화가 가능
- **json 구조**로 RDBMS 테이블 구조에 비해 데이터를 직관적으로 파악
- **Auto Sharding**을 지원

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

sharding이란<br>

단일의 논리적 데이터셋을 다수의 데이터베이스에 쪼개고 나누는 방법이다. 이런 방법으로 데이터베이스 시스템의 클러스터에서 큰 데이터셋을 저장하고 추가적인 요청을 처리할 수 있다. 샤딩은 데이터셋이 단일 데이터베이스에서 저장하기에 너무 클 때 필수적으로 사용된다. </div>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> NoSQL의 단점
</h3>

<br>

- **데이터 업데이트** 중 장애가 발생하면 **데이터 손실 발생** 가능
- **많은 인덱스**를 사용하려면 충분한 메모리가 필요. **인덱스 구조**가 메모리에 저장
- 복잡한 **join**은 어려움(다양하고 복잡한 데이터 쿼리), **document based**이기 때문
- **NoSQL**은 **sharding** 방식을 사용해서 큰 테이블을 여러 서버에 나누어 저장한다. fault tolerancy를 위해 데이터는 두개 이상의 서버에 저장된다. 어떤 데이터가 update 되었을 때, NoSQL은 중복 저장된 서버들에 해당 **update**가 적용되기까지는 시간이 걸린다.
- **RDBMS**는 모든 서버를 update 되기전까지는 해당 데이터 또는 테이블에 lock을 걸어 읽기 금지를 한다. 따라서 데이터에 대한 일관성이 보장된다. 하지만 NoSQL에서는 lock을 하게 될 경우 느려지므로 RDBMS와 같은 lock을 하지 않는다.
- **데이터 일관성**이 항상 보장되지 않는다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> NoSQL의 종류
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Key-Value Database
</h4>

![](/images/Interview/post16/2022-01-11-14-21-21.png?style=centerme)

<br>

기본적인 패턴으로 <span style="background: rgb(251,243,219)">KEY-VALUE</span> 하나의 묶음(Unique)으로 저장되는 구조로 단순한 구조이기에 속도가 빠르며 분산 저장시 용이하다.
Key 안에 (COLUMN, VALUE) 형태로 된 여러 개의 필드, 즉 **COLUMN FAMILIES**을 갖는다.

주로 <span style="background: rgb(251,243,219)">SERVER CONFIG, SESSION CLUSTERING</span>등에 사용되고 엑세스 속도는 빠르지만, <span style="background: rgb(251,243,219)">SCAN</span>에는 용이하지 않다.

**Ex)** Redis, Oracle NoSQL Database, VoldeMort

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Wide-Column Database
</h4>

![](/images/Interview/post16/2022-01-11-14-23-41.png?style=centerme)

<br>

행마다 키와 해당 값을 저장할 때마다 각각 다른 값의 다른 수의 스키마를 가질 수 있다.

위 그림을 참고하면 <span style="background: rgb(251,243,219)">사용자의 이름(key)</span>에 해당하는 값에 스키마들이 각각 다름을 볼 수 있다.

이러한 구조를 갖는 <span style="background: rgb(251,243,219)">WIDE COlUMN DATABASE</span>는 대량의 데이터 압축, 분산처리, 집계 쿼리(SUM, COUNT, AVG)및 쿼리 동작 속도 그리고 확장성이 뛰어난 것이 대표적 특징이라 할 수 있다. 

**Ex)** Hbase, GoogleBigTable, Vertica

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Document Database
</h4>

![](/images/Interview/post16/2022-01-11-14-25-25.png?style=centerme)

<br>

테이블의 스키마가 유동적, 즉 레코드마다 각각 다른 스키마를 가질 수 있다. 보통 <span style="background: rgb(251,243,219)">XML, JSON과 같은 DOCUMENT</span>를 이용해 레코드를 저장한다.

<span style="background: rgb(251,243,219)">트리형 구조</span>로 레코드를 저장하거나 검색하는 데 효율적이다.

**Ex)** MongoDB, CouchDB, Azure Cosmos DB

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Graph Database
</h4>

![](/images/Interview/post16/2022-01-11-14-28-13.png?style=centerme)

<br>

데이터를 노드로(그림에서 파란, 녹색 원) 표현하며 노드 사이의 관계를 엣지(그림에서 화살표)로 표현한다.

일반적으로 RDBMS보다 <span style="background: rgb(251,243,219)">성능이 좋고 유연하며 유지보수에 용이</span>한 것이 특징이다.

Social networks, Network diagrams 등에 사용할 수 있다.

**Ex)** Neo4j, BlazeGraph, OrientDB