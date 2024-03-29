---
layout: post
title: 스택(Stack)과 큐(Queue)의 개념 및 활용
date: 2021-12-30 10:00:00 0000
tags: [Stack, Queue]
categories: [Interview]
description: 스택과 큐의 비교 및 활용 예시
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

## **스택 Stack**

<br>

![](/images/Interview/post16/2021-12-30-10-29-20.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">스택(stack)</span>이란 **쌓아 올린다는 것**을 의미한다.

따라서 스택 자료구조라는 것은 책을 쌓는 것처럼 **차곡차곡 쌓아 올린 형태의 자료구조**를 말한다.

<br>

### <span style="color:#3D9970; font-weight:bold">스택의 특징</span>

<br>

스택은 위 사진처럼 **같은 구조와 크기의 자료**를 **정해진 방향으로만** 쌓을 수 있고 **top으로 정한 곳을 통해서만 접근**할 수 있다.

<br>

top에는 가장 위에 있는 자료를 가리키고 있으며 삽입되는 새 자료는 top이 가리키는 자료의 위에 쌓이게 된다.

<br>

스택에서 자료를 삭제할 때도 top을 통해서만 가능하다.

<br>

스택은 시간 순서에 따라 자료가 쌓여서 **가장 마지막에 삽입된 자료가 가장 먼저 삭제된다는** 구조적 특징을 가지게 된다.

<br>

이러한 스택의 구조를 **후입선출(LFO, Last-In-First-Out)** 구조라고 한다.

<br>

비어있는 스택에서 원소를 추출하려고 하면 **stack underflow**라고 하며 스택이 넘치는 경우 **stack overflow**라고 한다.

<br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">스택 오버플로우(stack overflow): </span> 스택이 꽉 차서 더 이상 자료를 <span style="background: rgb(251,243,219)">push</span> 할 수 없는 경우인데도 push를 하는 경우
- <span style="color: rgba(131, 24, 67); font-weight:bold">스택 언더플로우(stack underflow): </span>스택이 텅 비어있는 경우에 다시 <span style="background: rgb(251,243,219)">pop</span>을 하여 스택의 값을 빼낼 것을 요구하는 경우

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 스택 활용 예시
</h3>

<br>

- **웹 브라우저 방문기록** (뒤로 가기): 가장 나중에 열린 페이지부터 다시 보여준다.
- **역순 문자열 만들기**: 가장 나중에 입력된 문자부터 취소한다.
- **실행 취소 (undo)**: 가장 나중에 실해된 것부터 취소한다.
- **후위 표기법 계산**
- **수식의 괄호 검사** (연산자 우선순위 표현을 위한 괄호 검사)

<br>

---

<br>

## 큐 Queue

<br>

![](/images/Interview/post16/2021-12-30-11-03-44.png?style=centerme)

<br>

큐는 **줄, 혹은 줄을 서서 기다리는 것**을 의미한다.

일상생활에서 놀이동산에서 줄을 서서 기다리는 것, 은행에서 먼저 온 사람의 업무를 창구에서 처리하는 것과 같이 **선입선출(FIFO, First in First out) 방식**의 자료구조를 말한다.

<br>

### <span style="color:#3D9970; font-weight:bold">큐의 특징</span>

<br>

정해진 한 곳(top)을 통해서 삽입, 삭제가 이루어지는 스택과 달리 큐는 한쪽 끝에서 삽입 작업이, 다른 쪽 끝에서 살제 작업이 양쪽으로 이루어진다.

이때 **삭제 연산만 수행되는 곳을 프론트(front)**, **삽입 연산만 이루어지는 곳을 리어(rear)**로 정하여 각각의 연산 작업만 수행된다.

이때 큐의 리어에서 이루어지는 삽입연산을 **인큐(enqueue)** 프론트에서 이루어지는 삭제연산을 **디큐(dequeue)**라고 부른다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 큐 활용 예시
</h3>

<br>

- 우선순위가 같은 **작업 예약** (프린터의 인쇄 대기열)
- **은행 업무**
- 콜센터 **고객 대기시간**
- **프로세스 관리**
- **너비 우선 탐색(BFS) 구현**
- **캐시(Cache) 구현**
