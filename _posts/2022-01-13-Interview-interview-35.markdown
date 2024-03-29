---
layout: post
title: CGI는 무엇인가?
date: 2022-01-13 14:20:00 0000
tags: [httpd]
categories: [Interview]
description: CGI란
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

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> CGI
</h3>

<br>

![](/images/Interview/post16/2022-01-13-16-49-13.png?style=centerme)

<br>

초창기 웹사이트는 웹브라우저와 웹서버만으로도 충분했다. 그 당시 웹서버는 정적인 데이터와 이미지 파일만 처리했기 때문에 <span style="background: rgb(251,243,219)">PHP, Python</span> 등등이 필요 없었다.

하지만 인터넷 서비스가 점점 더 거대해지고 많은 역할들을 수행하기 시작되어 <span style="background: rgb(251,243,219)">정적인 데이터</span>로 서비스를 하는 것만으로는 <span style="background: rgb(251,243,219)">한계</span>를 부딪치게 되었습니다.

요즘 웹사이트를 본다면 HTML 문서로만 되어 있는 서버는 사이트를 운영할 수 없다. HTML 파일 관리, 데이터 고속처리, 사용자가 입력한 데이터 저장 등등 이러한 정적인 HTML 파일을 처리하는 <span style="background: rgb(251,243,219)">웹서버</span>만으로는 불가능하였고 그래서 등장하게 된 것이 <span style="background: rgb(251,243,219)">CGI</span>이다.

<br>

![](/images/Interview/post16/2022-01-13-16-51-03.png?style=centerme)

<br>

이 <span style="background: rgb(251,243,219)">CGI</span>는 사용자가 요청한 정보가 정적인 HTML 파일이 아니라 PHP, Python에서 요청이 오게 되면 웹서버는 자신이 처리할 수 없다는 사실을 알고 <span style="background: rgb(251,243,219)">PHP 인터프리터에게</span> 의뢰를 해서 개발자가 작성한 PHP 스크립터를 읽고 처리하여 그 결과를 웹서버에게 돌려주게 되고 웹서버는 그것을 다시 브라우저에게 돌려주게 된다.

<br>

이러한 웹서버(Nginx, Apache)와 PHP, Python 사이에 존재하여 **규격화된 약속으로 서로 데이터를 전송하여 처리하는 것이 CGI**이며, 웹서버(Nginx, Apache)와 PHP, Python 웹 프로그래밍 언어와 연동이 가능하게 된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> CGI의 한계
</h3>

<br>

이제 점점 더 서비스가 거대해지면서 CGI에도 한계에 봉착하게 된다.

<br>

![](/images/Interview/post16/2022-01-13-16-53-10.png?style=centerme)

<br>

**CGI**는 <span style="background: rgb(251,243,219)">요청할 때마다 프로세스를 생성</span>하고 프로세스가 가동하면서 <span style="background: rgb(251,243,219)">시스템 자원</span>을 소비하게 된다.

또한, 동시에 많은 <span style="background: rgb(251,243,219)">요청이 발생하면 프로세스가 생성되면서 서버에 부하</span>가 발생하게 된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> FastCGI(Fast Common Gateway Interface)
</h3>

<br>

<span style="background: rgb(251,243,219)">CGI 부하의 문제</span>로 서버는 비효율적으로 실행되고 있었다. 이러한 해결책으로 **CGI**를 진화시킨 기술로 <span style="background: rgb(251,243,219)">FastCGI</span>가 나오게 되었다.

<br>

![](/images/Interview/post16/2022-01-13-16-54-47.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">FastCGI</span>는 기존 **CGI**처럼 요청마다 프로세스를 생성하는 것이 아닌 <span style="background: rgb(251,243,219)">1개의</span> 큰 프로세스에 생성해서 여러 요청을 처리하게 된다. <span style="background: rgb(251,243,219)">1개의 프로세스만으로 처리하여 여러 프로세스를 생성해서 실행하는 부하를 해결</span>하게 된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> CGI 장점
</h3>

<br>

- 언어, 플랫폼 독립적이다(스펙만 준수하면 된다).
- 매우 단순하고 다른 server-side 프로그래밍 언어에 비해 advanced task를 훨씬 쉽게 수행할 수 있다.
- 재사용할 수 있는 CGI 코드 라이브러리가 풍부하다.
- CGI가 웹 서버에서 실행될 때 안전하다.
- CGI 코드를 수행하는데 특정 라이브러리가 필요하지 않기 때문에 매우 가볍다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> CGI 단점
</h3>

<br>

- 느리다(요청이 올 때마다 DB connection을 새로 열어야 한다).
- HTTP 요청마다 새로운 프로세스를 만들기 때문에 서버 메모리를 많이 잡아먹는다.(servlet은 요청마다 스레드를 만든다.)
- 페이지 로드 사이에 데이터가 메모리에 캐시될 수 없다.

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

<span style="background: rgb(251,243,219)">CGI</span>는 **인터페이스**인데 <span style="background: rgb(251,243,219)">웹 서버와 외부 프로그램 사이에서 정보를 주고받는 방법이나 규약들을 말한다.</span>
