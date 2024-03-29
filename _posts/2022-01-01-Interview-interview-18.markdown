---
layout: post
title: Framework와 Library의 차이
date: 2022-01-01 10:00:00 0000
tags: [Framework, Library]
categories: [Interview]
description: Framework와 Library의 대하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Framework vs Library
</h2>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Framework란?
</h3>

<br>

**"프레임워크란, 소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스들을 제공하는 것"** <span style="color:#107896; font-weight:bold">-by GOF</span>

<br>

쉽게 말해서 프레임워크는 <span style="color:#3D9970; font-weight:bold">차, 비행기, 배 같은 탈것과 같은 <span style="background: rgb(251,243,219)">운송수단</span>이다.</span>

사람이 탑승하여 시동을 걸고, 기어를 넣고, 핸들을 작동하고, 운전을 해야 한다.

<span style="background: rgb(251,243,219)">정해진 규칙</span>에 따라 시동을 걸고, 기어를 넣고, 핸들을 돌리면 되는 것이다. 즉, 이미 <span style="background: rgb(251,243,219)">프로그래밍할 규칙</span>이 정해져 있는 것이다.

<br>

![](/images/Interview/post16/2022-01-01-13-23-26.png?style=centerme)

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> 프레임워크 종류
</h3>

<br>

![](/images/Interview/post16/2022-01-01-13-27-15.png?style=centerme)

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> Framework의 장점
</h3>

<br>

- **효율적**
  - 아무것도 그려지지 않은 제로에서 <span style="background: rgb(251,243,219)">코드를 일일</span>이 짜는 것보다 **시간과 비용**이 훨씬 **절약**되며 생산성이 좋아진다.
- **Quality 향상**
  - <span style="background: rgb(251,243,219)">버그 발생 가능성</span>을 처리해줌으로써 개발자가 반복 작업에서 실수하기 쉬운 부분을 커버해준다. 다수의 개발자가 사용하며 수정하다 보니 <span style="background: rgb(251,243,219)">이미 검증된 코드</span>라고 볼 수 있다.
- **유지 보수가 좋다**
  - 프레임워크를 쓰지 않고 일일이 코드를 짜 놓은 경우, 회사 입장에서 개발 담당자가 바뀌어버리면 곤란해진다. 그러나 <span style="background: rgb(251,243,219)">Framework를</span> 사용하면 코드가 보다 **체계적**이어서 담당자가 바뀌더라도 <span style="background: rgb(251,243,219)">위험부담</span>을 줄일 수 있으며 **유지 보수**에 **안정적**이다.
- **코드의 중복을 줄일 수 있음**
  - 그로인한 <span style="background: rgb(251,243,219)">가독성</span>과 <span style="background: rgb(251,243,219)">유지보수</span> 향상
- **프로그래밍 시간을 줄일 수 있음**
  - 그로인한 <span style="background: rgb(251,243,219)">생산성</span> 향상

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23">Framework의 단점
</h3>

<br>

- **오랜 학습시간**
  - 코드를 본인이 짜 놓은 것이 아니기 때문에 프레임워크에 있는 코드를 **습득하고 이해하는 데 오랜 시간**이 걸림
- **제작자의 의도된 제약 사항**
  - 제작자가 <span style="background: rgb(251,243,219)">설계한 구조</span>를 어느 정도 유지한 채 코드에 살을 붙여나가야 함. 따라서 개발자는 **자유롭고 유연하게 개발하는 데 한계**가 있음

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Library란
</h3>

<br>

<span style="color:#3D9970; font-weight:bold">쉽게 비유 하자면 톱, 망치, 삽 같은 연장(도구)이다.</span> 사람들이 흔히 <span style="background: rgb(251,243,219)">도구</span>를 사용하여 썰고, 박고, 땅 파는 역할과 같다.

<span style="background: rgb(251,243,219)">도구</span>를 사용하다 보면 급할 때는 톱으로 못을 박을 수도 있다.

IT 프로젝트 시에 개발자는 도구를 선택하는 입장이기 때문에, 어떤 도구를 사용하든 사용자가 원하는 것을 만들어 줄 수만 있으면 된다.

<br>

![](/images/Interview/post16/2022-01-01-13-25-15.png?style=centerme)

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> 정리
</h3>

<br>

<span style="color:#093145; font-weight:bold">라이브러리란 자주 사용되는 로직을 재사용하기 편리하도록 잘 정리한 일련의 코드들의 집합을 의미한다.</span>

<br>

- 라이브러리는 <span style="background: rgb(251,243,219)">재사용</span>이 필요한 기능으로 <span style="background: rgb(251,243,219)">반복적인 코드 작성</span>을 없애기 위해 언제든지 필요한 곳에서 <span style="background: rgb(251,243,219)">호출</span>하여 사용할 수 있도록 **Class나 Function**으로 만들어진다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> API란
</h3>

<br>

<span style="color:#093145; font-weight:bold">API란 응용 프로그램에서 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스이다.</span>

위에서 말했던 것과 같이 **라이브러리는 도구 자체이고** API는 **"도구 주세요!"**라고 요청하는 것이라 볼 수 있을 것 같다.

<br>

필요한 부분을 요청하여 응답을 받는 <span style="background: rgb(251,243,219)">서비스간</span>의 **다리**와 같은 역할을 한다.

- 구현과 독립적으로 **사양만 정의** 되어있음
- **접근권한**을 부여받아야함
- 말 그대로 **인터페이스**, 안에는 무엇이 들어있는지 알 수 없음.

<br>

---

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> 결론
</h2>

<br>

![](/images/Interview/post16/2022-01-01-13-36-31.png?style=centerme)

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> Framework
</h3>

<br>

> **응용 프로그램**이나 **소프트웨어의 솔루션 개발**을 수월하게 하기 위해 제공된 **소프트웨어 환경**

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> Library
</h3>

<br>

> **응용 프로그램 개발**을 위해 필요한 기능을 모아 놓은 소프트웨어

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> API
</h3>

<br>

**Exmaple:** jQuery

<br>

> **응용 프로그램**에서 **운영체제**나 **프로그래밍 언어**가 제공하는 기능을 제어할 수 있게 만든 인터페이스

<br>

**Example:** 구글 지도 api/ 카카오 api
