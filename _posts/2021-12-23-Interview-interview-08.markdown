---
layout: post
title: I/O 모델 - 동기, 비동기, Blocking, Non-Blocking
date: 2021-12-23 16:00:00 0000
tags: [IO Model]
categories: [Interview]
description: I/O 관점에서의 동기, 비동기, Blocking, Non-Blocking
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

이전 포스트에서 동기, 비동기, 블로킹, 논블로킹에 대해서 충분히 다뤘는데도 불구하고 또 다루는 이유는 이렇다. 전의 포스트에서는 일반적인 개념에 대해서 다뤘다면 이번에는 I/O 관점에서 다루고 싶었다.

<br>

많은 면접을 거친 결과 이런 질문들이 있다.

<br>

### Q: 동기와 비동기에 대해서 설명해 주세요

혹인

### Q: 동기 비동기 I/O에 대해서 설명해 주세요

혹은

### Q: 블로킹과 논블로킹에 대해서 설명해 주세요

혹은

### Q: 블로킹 I/O와 논블로킹 I/O에 대해서 설명해 주세요

<br>

물론 <span style="background: rgb(251,243,219)">I/O</span> 하나 붙었다고 해서 큰 개념에 차이가 있는 것은 아니다. 일반적인 의미는 이전 포스트에서 다룬 내용과 같다. 다만 이번에는 <span style="background: rgb(251,243,219)">운영체제 관점</span>에서 들여다 본다는 차이가 있다.

<br>

하나씩 살펴보도록 하자.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 동기식 입출력 (Synchronous I/O)
</h3>

<br>

- 프로그램 <span style="background: rgb(251,243,219)">I/O 요청</span>을 했을 때 해당 <span style="background: rgb(251,243,219)">I/O 작업</span>이 완료되어야 다음 작업을 할 수 있는 방식이다.
  - <span style="background: rgb(251,243,219)">I/O</span>가 진행되는 동안 다음 명령을 수행하지 않고 기다린다.
  - <span style="background: rgb(251,243,219)">I/O</span> 상태의 프로세스는 <span style="background: rgb(251,243,219)">blocked state</span>로 전환된다.
  - <span style="background: rgb(251,243,219)">I/O</span>가 완료되면 인터럽트를 통해 완료를 알린다. 이후 CPU의 제어권이 기존 프로그램에게 넘어간다.
  - <span style="background: rgb(251,243,219)">blocked state</span>의 프로세스는 <span style="background: rgb(251,243,219)">wait</span> 상태로 돌아간다.

<br>

- 명령 수행 속도는 빠르지만 <span style="background: rgb(251,243,219)">입출력 연산</span>은 상대적으로 느리다. 기다리는 과정에서 <span style="background: rgb(251,243,219)">자원 낭비</span>를 초래한다.

<br>

- 보통 I/O가 진행되면 CPU는 다른 프로그램의 작업을 수행하게 된다.

<br>

- 입출력 요청의 동기화
  - 여러 프로세스가 <span style="background: rgb(251,243,219)">동시에 I/O 요청</span>을 할 경우 각 요청을 큐에 넣어 순서대로 처리한다.

---

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 비동기식 입출력(Non-Synchronous I/O)
</h3>

<br>

- CPU의 <span style="background: rgb(251,243,219)">제어권</span>을 입출력 연산을 호출한 프로그램에게 곧바로 다시 부여한다.

<br>

- <span style="background: rgb(251,243,219)"> I/O 결과와 관련 없는 연산</span>이 있을 경우 주로 사용된다.

<br>

- CPU는 <span style="background: rgb(251,243,219)">I/O 결과</span>와 상관 없이 처리 가능한 작업부터 처리한다.

<br>

- I/O 연산이 완료되면 <span style="background: rgb(251,243,219)">인터럽트</span>를 통해 알린다.

<br>

---

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Blocking I/O
</h3>

<br>

- 직접 제어할 수 없는 대상의 <span style="background: rgb(251,243,219)">작업(I/O)</span>이 완료될 때까지 기다린다.
  - <span style="background: rgb(251,243,219)">I/O가 완료</span>되어야 제어권이 프로세스로 넘어간다.

<br>

- 동기와 마찬가지로 자원이 낭비된다.

---

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Non-Blocking I/O
</h3>

<br>

입출력 처리는 시작만 해둔 채 완료되지 않은 상태에서 다른 처리 작업을 계속 진행할 수 있도록 <span style="background: rgb(251,243,219)">멈추지 않고 입출력 처리를 기다리는 방법</span>을 말한다.

I/O 처리를 하는 <span style="background: rgb(251,243,219)">전통적인 방법은 I/O 작업을 시작하면 완료될 때까지 기다리는 방법</span>이다. 기존에는 synchronous I/O 혹은 blocking I/O를 통해 I/O 작업을 진행하는 동안 <span style="background: rgb(251,243,219)">프로그램이 아무 일도 하지 않고 시간을 소비하게</span> 만든다.

반면, <span style="background: rgb(251,243,219)">Non-blocking I/O 방식</span>을 사용하면 <span style="background: rgb(251,243,219)">외부에 I/O 작업을 하도록 요청한 후, 즉시 다음 작업을 처리</span>함으로써 시스템 자원을 더 효율적으로 사용할 수 있게된다.

그러나 I/O 작업이 완료된 이후에 처리해야 하는 후속 작업이 있다면, I/O 작업이 완료될 때까지 기다려야 한다. 따라서 이 후속 작업이 프로세스를 멈추지 않도록 만들기 위해 I/O 작업이 완료된 이후 <span style="background: rgb(251,243,219)">후속 작업이 이어서 진행할 수 있도록 별도의 약속(Polling, Callback function 등)</span>을 한다.

<br>

- I/O 작업이 진행되는 동안에는 <span style="background: rgb(251,243,219)">유저 프로세스의 작업</span>을 중단시키지 않는다.
  - 제어권을 바로 반납한다.

<br>

- I/O 완료와 상관없이 <span style="background: rgb(251,243,219)">작업 결과가 반환</span>된다.
  - 이를 입력 데이터가 있을 때까지 반복하고, 입력 데이터가 있으면 결과가 전달된다.

<br>

- 대기하지 않아도 되지만 I/O 완료를 확인해야 하기 때문에 <span style="background: rgb(251,243,219)">시스템 호출이 반복</span>된다.

<br>

- 동기, 비동기는 개선된 I/O 이벤트 통지 모델이다.

---

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

![](/images/Interview/post11/2021-12-23-17-53-39.png?style=centerme)

<br>

- <span style="background: rgb(251,243,219)">동기/비동기</span>는 <span style="background: rgb(251,243,219)">인터럽트 발생</span>으로 인한 <span style="background: rgb(251,243,219)">제어권 반한 시점</span>에 중점을 두고 Blocking/Non-Blocking은 <span style="background: rgb(251,243,219)">제어권 자체</span>에 중점을 둔다는 점에서 차이가 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 읽어보면 좋은 링크
</h3>

**[링크](https://carnival.tistory.com/51)**

**[링크](https://owlyr.tistory.com/26)**
