---
layout: post
title: Spring MVC
date: 2021-12-25 12:00:00 0000
tags: [Spring MVC]
categories: [Interview]
description: Spring MVC의 동작 원리
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

**_크리스마스 때는 뭐니뭐니 해도 공부지~_**

<br>

**~~울지 말고 다시 말해봐..:cry::cry::cry::cry:~~**

<br>

오늘은 기분좋은 크리스마스 날이다. 새로운 지식을 쌓기에 정말 좋은 날인 것 같다.

<br>

그동안 제대로 알지 못하고 사용하고 있었던 Spring MVC에 대해서 알아보자.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Spring MVC
</h3>

<br>

<span style="background: rgb(251,243,219)">Spring MVC</span>는 모델 2방식 구조이다.

모델2 방식이 뭘까?

화면을 담당하는 <span style="background: rgb(251,243,219)">View</span>적인 부분과 데이터를 처리하는 <span style="background: rgb(251,243,219)">비즈니스로직 부분을 분리</span>한 것으로 <span style="background: rgb(251,243,219)">디자이너와 개발자의 작업분리</span>가 되어 있어 작업하기 편리하며 재사용이 가능한 구조이다.

<br>

MVC는 **Model, View, Controller**의 약자라고 할 수 있다.

<br>

<span style="color:#3D9970; font-weight:bold">Model(모델):</span> 데이터를 처리하는 부분

<br>

<span style="color:#3D9970; font-weight:bold">View(뷰):</span> 화면을 담당하는 부분

<br>

<span style="color:#3D9970; font-weight:bold">Controller(컨트롤러): </span> 요청을 처리하는 부분으로 뷰와 모델 사이의 통신 역할을 함

<br>

**모델 2**는 어떤 요청이 들어오면 **Controller**가 요청을 받고 요청에 해당하는 **Model**을 호출하게 된다. 호출된 **Model**은 데이터들을 처리한 후 **Controller**에게 요청에 대한 결과(응답)를 보내고 **Controller**는 **View**에게 전송하는 원리이다.

<br>

(요청->컨트롤러->모델->컨트롤러->뷰)

<br>

이 구조의 장점은 **개발자**와 **디자이너(웹 퍼블리셔)**의 작업공간을 분리시킬 수 있고 **Controller**는 URL을 통해 **View**를 제어하기 때문에 **View(화면)**을 변경하거나 수정할 대 유용하게 사용된다.

<br>

즉 <span style="background: rgb(251,243,219)">유지보수</span>가 좋다!

<br>

좀 더 구체적으로 구조적 설명을 해보자.

<br>

![](/images/Interview/post13/2021-12-26-00-24-51.png?style=centerme)

<br>

**1.** 클라이언트(사용자)의 모든 요청은 <span style="color:#2ECC40; font-weight:bold">DispatcherServlet</span>이 받는다.<br><br>

**2.** <span style="color:#2ECC40; font-weight:bold">DispatcherServlet</span>은 <span style="color:#2ECC40; font-weight:bold">handlerMapping</span>을 통해서 요청에 해당하는 <span style="color:#2ECC40; font-weight:bold">Controller</span>를 실행 시킨다.<br><br>

**3.** <span style="color:#2ECC40; font-weight:bold">Controller</span>는 적절한 서비스 객체를 호출 시킨다.<br><br>

**4.** <span style="color:#2ECC40; font-weight:bold">Service</span>는 <span style="color:#2ECC40; font-weight:bold">DB</span>처리를 위해 <span style="color:#2ECC40; font-weight:bold">DAO</span>를 이용하여 데이터를 요청한다.<br><br>

**5.** <span style="color:#2ECC40; font-weight:bold">DAO</span>는 <span style="color:#2ECC40; font-weight:bold">mybatis</span>를 이용하는 <span style="color:#2ECC40; font-weight:bold">Mapper</span>를 통해 처리를 한다.<br><br>

**6.** 결과(처리한 데이터)가 <span style="color:#2ECC40; font-weight:bold">mapper->DAO->Service->Controller</span>로 전달된다.<br><br>

**7.** <span style="color:#2ECC40; font-weight:bold">Controller</span>는 전달된 결과(처리된 데이터)를 <span style="color:#2ECC40; font-weight:bold">View Resolver</span>를 통해 전달 받을 <span style="color:#2ECC40; font-weight:bold">View</span>가 있는지 검색한다.<br><br>

**8.** 전달 받은 <span style="color:#2ECC40; font-weight:bold">View</span>가 있다면 <span style="color:#2ECC40; font-weight:bold">View</span>에게 전달된 결과(처리된 데이터)를 전달한다.<br><br>

**9.** <span style="color:#2ECC40; font-weight:bold">View</span>는 전달받은 결과(처리된 데이터)를 다시 <span style="color:#2ECC40; font-weight:bold">DispatcherServlet</span>에게 전달한다.<br><br>

**10.** <span style="color:#2ECC40; font-weight:bold">DispatcherServlet</span>은 전달받은 결과(처리된 데이터)를 <span style="color:#2ECC40; font-weight:bold">Client</span>에게 전달한다.

<br><br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">Front Controller</span>: 서버로 들어오는 모든 요청을 받아서 처리(공통 처리 작업을 먼저 수행 한 후 적절한 세부 controller에게 작업을 위힘해주고 예외 발생시 일관된 방식으로 에러를 처리해줌)
  - 위와 같은 일을 하기 때문에 각 controller 사이의 중복된 코드 문제나 협업시 개발자들의 개발 방식이 다른 경우 등을 해결할 수 있음.

<br>

