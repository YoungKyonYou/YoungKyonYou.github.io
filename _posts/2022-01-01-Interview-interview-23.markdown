---
layout: post
title: 트랜잭션 격리 수준(Isolation Level)
date: 2022-01-01 16:00:00 0000
tags: [Isolation Level]
categories: [Interview]
description: 트랜잭션 격리 수준에 대하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Transaction Isolation Level
</h2>

<br>

트랜잭션 격리 수준에 대해 알기 위해서는 일단 **트랜잭션**이 무엇인지부터 알아야 한다.

<br>

**트랜잭션**: 데이터베이스의 <span style="background: rgb(251,243,219)">상태를 변화</span>시키기 위해서 수행하는 <span style="background: rgb(251,243,219)">작업의 단위를</span> 뜻한다.

<br>

데이터베이스의 <span style="background: rgb(251,243,219)">상태를 변화</span> 시킨다는 것은 아래의 질의어(SQL)를 이용하여 <span style="background: rgb(251,243,219)">데이터베이스를 접근</span>하는 것을 의미한다.

<br>

- SELECT
- INSERT
- DELETE
- UPDATE

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 트랜잭션의 특징(ACID)
</h4>

<br>

- 원자성(Atomicity)
- 일관성(Consistency)
- 독립성(Isolation)
- 지속성(Durability)

<br>

<span style="background: rgb(251,243,219)">원자성(Atomicity)</span>

1. 트랜잭션의 연산은 데이터베이스에 **모두 반영되든지** 아니면 **전혀 반영되지** 않아야 한다.
2. 트랜잭션 내의 모든 명령은 반드시 **완벽히 수행**되어야 하며, 모두가 **완벽히 수행**되지 않고 어느 하나라도 오류가 발생하면 **트랜잭션 전부가 취소**되어야 한다.

<br>

<span style="background: rgb(251,243,219)">일관성(Consistency)</span>

1. 트랜잭션이 그 **실행**을 성공적으로 **완료**하면 언제나 **일관성** 있는 **데이터베이스 상태로** 변환한다.
2. 시스템이 가지고 있는 **고정요소**는 **트랜잭션 수행 전과 트랜잭션 수행 완료 후**의 **상태**가 **같아야** 한다.

<br>

<span style="background: rgb(251,243,219)">독립성, 격리성(Isolation)</span>

1. 둘 이상의 트랜잭션이 **동시에 병행** 실행되는 경우 어느 하나의 트랜잭션 실행 중에 다른 트랜잭션의 **연산이 끼어**들 수 없다.
2. 수행중인 트랜잭션은 **완전히 완료될 때까지** 다른 트랜잭션에서 **수행 결과를 참조**할 수 없다.

<br>

<span style="background: rgb(251,243,219)">영속성, 지속성(Durability)</span>

1. **성공적으로 완료**된 트랜잭션의 **결과**는 **시스템이 고장**나더라도 **영구적으로 반영**되어야 한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Commit 연산과 Rollback 연산
</h4>

<br>

<span style="background: rgb(251,243,219)">Commit 연산</span>

1. Commit 연산은 **한 개의 논리적 단위**(트랜잭션)에 대한 **작업이 성공적**으로 끝났고 데이터베이스가 다시 일관된 상태에 있을 때, 이 **트랜잭션이 행한 갱신 연산**이 **완료**된 것을 **트랜잭션 관리자에게 알려주는 연산**이다.

<br>

<span style="background: rgb(251,243,219)">Rollback 연산</span>

1. Rollback 연산은 **하나**의 **트랜잭션 처리가 비정상적으로 종료**되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 **트랜잭션의 원자성**을 구현하기 위해 이 **트랜잭션**이 행한 **모든 연산을 취소(Undo)**하는 연산이다.
2. Rollback시에는 해당 **트랜잭션**을 **재시작**하거나 **폐기**한다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 트랜잭션 격리 수준
</h3>

<br>

본론으로 돌아와서 이제 트랜잭션 <span style="background: rgb(251,243,219)">격리 수준</span>에 대해서 살펴보자.

<br>

트랜잭션 격리 수준은 <span style="color:#2ECC40; font-weight:bold">고립도</span>와 <span style="color:#2ECC40; font-weight:bold">성능</span>의 **Trade-off**를 조절한다.

<br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">READ UNCOMMITED:</span> 다른 트랜잭션 중 커밋되지 않은 데이터를 다른 트랜잭션이 참조할 수 있다.
- <span style="color: rgba(131, 24, 67); font-weight:bold">READ COMMITED:</span> 커밋이 완료된 데이터만 다른 트랜잭션에서 참조할 수 있다.
- <span style="color: rgba(131, 24, 67); font-weight:bold">REPEATABLE READ:</span> 트랜잭션 시작 전 COMMIT 된 데이터에만 접근할 수 있다.
- <span style="color: rgba(131, 24, 67); font-weight:bold">SERIALIZABLE:</span> 트랜잭션에 진입하면 락을 걸어 다른 트랜잭션이 접근하지 못하게 한다. (성능이 매우 떨어짐)

<br>

![](/images/Interview/post16/2022-01-01-22-54-26.png?style=centerme)

<br>

트랜잭션 격리 수준이란 **트랜잭션들끼리 얼마나 고립되어있는지(잠금수준)를 나타내는 것이다.**

특정 트랜잭션이 다른 트랜잭션에 의해 변경된 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것이다.

<br>

격리 수준은 위에 명시된 순서로 내려갈수록 **고립도가 높아지나 성능이 떨어지는 게 일반적**이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 트랜잭션 격리 수준이 필요한 이유
</h3>

<br>

트랜잭션 수준 읽기 일관성 (Transaction-Level Read Consistency)을 지키기 위해서이다.(다시 말해 **동시성 제어 문제** 해결을 위해서이다.)

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

트랜잭션 수준 읽기 일관성이란<br><br>
트랜잭션이 시작된 시점으로부터 일관성 있게 데이터를 읽어 들이는 것을 말한다. 하나의 트랜잭션이 진행되는 동안 다른 트랜잭션에 의해 변경사항이 발생하더라도 이를 무시하고 계속 일관성 있는 데이터를 보여준다. (물론 트랜잭션 자신이 발생한 변경사항은 읽을 수 있다.)</div>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> READ UNCOMMITTED (트랜잭션 레벨 0)
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-02-12.png?style=centerme)

<br>

이 단계에서는 트랜잭션에서 처리 중인, 아직 <span style="background: rgb(251,243,219)">커밋되지 않은 데이터</span>를 다른 트랜잭션이 <span style="background: rgb(251,243,219)">읽는 것을</span> 허용한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

- Dirty Read, Non-Repeatable Read, Phantom Read 현상이 발생한다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

PHANTOM READ<br><br>

- 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상<br> - 이를 방지하기 위해서는 쓰기 잠금을 걸어야 한다.
</div>

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

DIRTY READ<br><br>

아직 커밋되지 않은 다른 트랜잭션의 데이터를 읽는 것을 의미한다.</div>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 문제점
</h4>

데이터 정합성에 문제가 많다. 그렇기에 RDBMS 표준에서는 격리수준으로 인정하지 않는다.

<br>

**예시**

- <span style="background: rgb(251,243,219)">트랜잭션 A</span>는 테이블의 데이터를 수정중인 상태이고 아직 <span style="background: rgb(251,243,219)">COMMIT</span> 전이다.
- <span style="background: rgb(251,243,219)">트랜잭션 B</span>는 트랜잭션 A가 수정중인 데이터를 조회한다. (이를 <span style="background: rgb(251,243,219)">Dirty Read라고 한다.</span>)
- 하지만 <span style="background: rgb(251,243,219)">트랜잭션 B</span>는 COMMIT 되지 않은 데이터를 가지고 로직을 수행한다. (문제 발생)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> READ COMMITTED (트랜잭션 레벨 1)
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-06-40.png?style=centerme)

<br>

RDB에서 대부분 기본적으로 사용되고 있는 격리 수준으로 **실제 테이블 값**을 가져오는 것이 아니라 **Undo** 영역에 <span style="background: rgb(251,243,219)">백업된 레코드에서</span> 값을 가져온다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

- <span style="background: rgb(251,243,219)">Dirty Read</span>가 발생하지 않지만(트랜잭션이 COMMIT되어 확정된 데이터만 읽는 것을 허용한다.) <span style="background: rgb(251,243,219)">Non-Repeatable Read, Phantom Read</span> 현상은 여전히 발생한다.
- 온라인 서비스에서 <span style="background: rgb(251,243,219)">가장 많이 선택</span>되는 격리수준이다.
  - DB2, SQL Server, Sybase의 경우 <span style="background: rgb(251,243,219)">읽기, 공유 Lock</span>을 이용하여 구현한다.
  - Oracle은 Lock을 사용하지 않고 쿼리시작 시점의 <span style="background: rgb(251,243,219)">Undo 데이터</span>를 제공한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 문제점
</h4>

**NON-REPEATBLE READ** <span style="background: rgb(251,243,219)">부정합 문제</span>가 발생할 수 있다.

READ COMMITED 격리 수준에서 실행되는 SQL 문장의 <span style="background: rgb(251,243,219)">결과가 무엇인지 정확히 예측</span>하고 있어야 한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REPEATABLE READ (트랜잭션 레벨 2)
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-10-59.png?style=centerme)

<br>

트랜잭션이 시작되기 전에 <span style="background: rgb(251,243,219)">COMMIT된 내용에 대해서만 조회</span>할 수 있는 격리수준이다.

- MySQL에서는 트랜잭션마다 <span style="background: rgb(251,243,219)">트랜잭션 ID</span>를 부여하여 **트랜잭션 ID 보다 작은 트랜잭션 번호에서 변경한 것만 읽게 된다.**
- 변경되기 전 레코드는 <span style="background: rgb(251,243,219)">Undo 공간</span>에 백업해 두고 <span style="background: rgb(251,243,219)">실제 레코드 값</span>을 변경한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

- Dirty Read와 같은 현상은 발생하지 않지만 **Phantom Read** 현상은 여전히 발생한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 문제점
</h4>

하나의 트랜잭션 실행시간이 길어질수록 **Undo에 백업된 레코드가 많아져서 멀티 버전을 관리해야 하는 단점이** 있다.
(하지만 영향을 미칠정도로 트랜잭션이 오래 지속되는 경우가 없어서 READ COMMITTED와 REPEATABLE READ의 성능 차이는 거의 없다고 한다.)

또한, <span style="background: rgb(251,243,219)">UPDATE 부정합</span>와 <span style="background: rgb(251,243,219)">Phantom Read</span>가 발생할 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 
SERIALIZABLE (트랜잭션 레벨 3)</h3>

<br>

선형 트랜잭션이 특정 테이블을 읽는 경우(SELECT) <span style="background: rgb(251,243,219)">공유 잠금(shared lock)</span>을 걸어, 다른 트랜잭션에서 해당 테이블의 데이터를 <span style="background: rgb(251,243,219)">UPDATE, DELETE, INSERT</span> 작업을 못하도록 막는다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

가장 단순한 격리 수준이지만 가장 <span style="background: rgb(251,243,219)">엄격한 격리 수준</span>으로 <span style="background: rgb(251,243,219)">Phantom Read</span>가 발생하지 않는다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 문제점
</h4>

<span style="background: rgb(251,243,219)">동시 처리 능력</span> 이 다른 격리수준보다 떨어지고 <span style="background: rgb(251,243,219)">성능저하</span>가 발생하여 데이터베이스에서 거의 사용되지 않는다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 낮은 단계의 트랜잭션 고립화 수준을 사용할 때 발생하는 세 가지 현상
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-24-12.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Dirty Read (Uncommitted Dependency)
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-24-46.png?style=centerme)

<br>

- 변경 후 아직 <span style="background: rgb(251,243,219)">Commit 되지 않은 값 읽고</span>, Rollback 후의 값을 다시 읽어 <span style="background: rgb(251,243,219)">최종 결과 값이 상이한</span> 현상이다.
- Oracle은 <span style="background: rgb(251,243,219)">다중 버전 읽기 일관성 모델</span>을 채택하여 <span style="background: rgb(251,243,219)">lock</span>을 사용하지 않고 <span style="background: rgb(251,243,219)">Dirty Read</span>를 피해 일관성 있는 데이터 읽기가 가능하게 하였다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Non-Repeatble Read (Inconsistent Analysis)
</h3>

<br>

![](/images/Interview/post16/2022-01-01-23-26-36.png?style=centerme)

<br>

한 트랜잭션 내에서 <span style="background: rgb(251,243,219)">같은 쿼리를 두번 수행</span>할 때, 그 사이에 다른 트랜잭션이 <span style="background: rgb(251,243,219)">값을 수정</span> 또는 <span style="background: rgb(251,243,219)">삭제</span>함으로써 두 쿼리가 <span style="background: rgb(251,243,219)">상이하게 나타나는</span> <span style="background: rgb(251,243,219)">비 일관성이</span> 발생하는 것을 말한다.

(다시말해 하나의 트랜잭션 내에서 동일한 SELECT를 수행했을 경우 <span style="background: rgb(251,243,219)">항상 같은 결과</span>를 반환해야하는 REPEATABLE READ <span style="background: rgb(251,243,219)">정합성</span>에 어긋나는 것이다.)

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

금전적 처리와 연결된 서비스에서 문제가 발생할 수 있다.<br><br>

- 트랜잭션B에서 1번 상품의 총 투자액을 조회 => 100만원이 조회됨<br>
- 트랜잭션A에서 1번 상품의 총 투자액을 120만원으로 바꾸고 COMMIT<br>
- 트랜잭션B에서 1번 상품의 총 투자액을 다시 조회 => 120만원이 조회됨 (NON-REPEATABLE READ)</div>

<br>
