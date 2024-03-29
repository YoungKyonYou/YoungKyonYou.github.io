---
layout: post
title: HTTP Connection
date: 2022-01-15 12:20:00 0000
tags: [HTTP Connection]
categories: [Interview]
description: HTTP Connection
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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> HTTP Connection
</h2>

<br>

<span style="background: rgb(251,243,219)">커넥션 관리</span>는 HTTP의 주요 주제이다. 대규모로 커넥션을 열고 유지하는 것은 웹 사이트 혹은 웹 애플리케이션의 성능에 많은 영향을 준다. <span style="background: rgb(251,243,219)">HTTP/1.x</span>에는 몇 가지 모델이 존재한다.

- **단기 커넥션**
- **영속적인 커넥션**
- **병렬 커넥션**
- **HTTP 파이프라이닝**

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 단기 커넥션
</h4>

<span style="background: rgb(251,243,219)">HTTP 본래의 모델</span>이자 HTTP/1.0의 기본 커넥션은 <span style="background: rgb(251,243,219)">단기 커넥션</span>이다. 각각의 HTTP 요청은 각각의 커넥션 상에서 실행된다. 이는 <span style="background: rgb(251,243,219)">TCP 핸드 셰이크</span>는 각 HTTP 요청 전에 발생하고, 이들이 직렬화됨을 의미한다.

<span style="background: rgb(251,243,219)">TCP 핸드셰이크</span>는 그 자체로 시간을 소모하기는 하지만 TCP 커넥션은 지속적으로 연결되었을 때 <span style="background: rgb(251,243,219)">부하</span>에 맞춰 더욱 예열되어 더욱 효율적으로 작동한다. <span style="background: rgb(251,243,219)">단기 커넥션</span>들은 TCP의 이러한 효율적인 특성을 사용하지 않게 하며 예열되지 않은 새로운 연결을 통해 지속적으로 전송함으로써 성능이 최적 상태보다 저하된다.

이 모델은 <span style="background: rgb(251,243,219)">HTTP/1.0</span>에서 사용된 기본 모델이다. <span style="background: rgb(251,243,219)">HTTP/1.1</span>에서는 이 모델은 Connection 헤더가 close 값으로 설정되어 전송된 경우에만 사용된다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

영속적인 커넥션을 지원하지 않는 매우 낡은 시스템을 다루는 것이 아니라면 이 모델을 사용하려고 애쓸 필요가 없다</div>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 영속적인 커넥션
</h4>

<span style="background: rgb(251,243,219)">단기 커넥션은</span> 두가지 결점을 지니고 있다.

**1)** 새로운 연결을 맺는데 드는 시간이 상당하다<br>
**2)** TCP 기반 커넥션의 성능은 오직 커넥션이 예열된 상태일 때만 나아진다는 것이다.

<br>

이런 문제를 완화시키기 위해 <span style="background: rgb(251,243,219)">HTTP/1.1</span>보다도 앞서 영속적인 커넥션의 컨셉이 만들어졌다. 이는 <span style="background: rgb(251,243,219)">keep-alive 커넥션</span>이라고 불리기도 한다.

<span style="background: rgb(251,243,219)">영속적인 커넥션</span>은 연결을 열어놓고 여러 요청에 재사용함으로써, 새로운 TCP 핸드셰이크를 하는 비용을 아끼고 TCP의 성능 향상 기능을 활용할 수 있다. 커넥션은 영원히 열려있지는 않으며 <span style="background: rgb(251,243,219)">유휴 커넥션</span>들은 얼마 후에 닫힌다.(서버는 **Keep-Alive** 헤더를 사용해서 연결이 최소한 얼마나 열려있어야 할지를 설정할 수 있다.)

물론 영속적인 커넥션도 <span style="background: rgb(251,243,219)">단점</span>을 가지고 있다. **유휴 상태**일때에도 <span style="background: rgb(251,243,219)">서버 리소스를 소비</span>하며 <span style="background: rgb(251,243,219)">과부하</span> 상태에서는 <span style="background: rgb(251,243,219)">DoS attacks</span>을 당할 수 있다. 이런 경우에는 커넥션이 유휴 상태가 되자마자 닫히는 비영속적 커넥션(non-persistent connections)을 사용하는 것이 더 나은 성능을 보일 수 있다.

<span style="background: rgb(251,243,219)">HTTP/1.0 커넥션</span>은 기본적으로 영속적이지 않다. Connection를 close가 아닌 다른 것으로 일반적으로 retry-after로 설정하면 영속적으로 동작하게 될 것이다.

반면 <span style="background: rgb(251,243,219)">HTTP/1.1</span>에서는 기본적으로 영속적이며 헤더도 필요하지 않다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 병렬 커넥션
</h4>

HTTP는 클라이언트가 <span style="background: rgb(251,243,219)">여러 개의 커넥션</span>을 맺음으로써 여러 개의 <span style="background: rgb(251,243,219)">HTTP 트랜잭션</span>을 병렬로 처리할 수 있게 한다.

병렬 커넥션은 페이지를 더 빠르게 내려받는다. 하나의 커넥션으로 객체들을 로드할 때의 대역폭 제한과 대기시간을 줄일 수 있다면 더 빠르게 로드할 수 있다.

하지만, 병렬 커넥션이 항상 더 빠르지는 않다. 왜냐하면 클라이언트의 <span style="background: rgb(251,243,219)">네트워크 대역폭</span>이 좁을 때는 대부분 시간을 데이터 전송하는 데만 쓸 것이다. 그리고 다수의 <span style="background: rgb(251,243,219)">커넥션</span>은 메모리를 많이 소모하고 자체적인 성능 문제를 발생시킨다. 브라우저는 실제로 병렬 커넥션을 사용하긴 하지만 적은 수(대부분 4개, 최신 브라우저는 6~8개)의 병렬 커넥션만을 허용한다. 서버는 특정 클라이언트로부터 과도한 수의 커넥션이 맺어졌을 경우 그것을 임의로 끊어버릴 수 있다.

병렬 커넥션이 실제로 페이지를 더 빠르게 내려받는 것은 아니지만 화면에 여러 개의 객체가 동시에 보이면서 내려받고 있는 상황을 볼 수 있기 때문에 사용자는 더 빠르게 내려받고 있는 것 처럼 느낄 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> HTTP 파이프라이닝
</h4>

기본적으로 <span style="background: rgb(251,243,219)">HTTP 요청</span>은 순차적이다. 현재의 요청에 대한 응답을 받고 나서야 다음 요청을 실시한다. 네트워크 지연과 대역폭 제한에 걸려 다음 요청을 보내는 데까지 상당한 <span style="background: rgb(251,243,219)">딜레이</span>가 발생할 수 있다.

<span style="background: rgb(251,243,219)">파이프라이닝</span>이란 같은 <span style="background: rgb(251,243,219)">영속적인 커넥션</span>을 통해서 응답을 기다리지 않고 요청을 연속적으로 보내는 기능이다. 이것은 <span style="background: rgb(251,243,219)">커넥션의 지연</span>을 회피하고자 하는 방법이다. 이론적으로는 두 개의 HTTP 요청을 하나의 TCP 메시지 안에 채워서 성능을 더 향상시킬 수 있다. HTTP 요청의 사이즈는 지속적으로 커져왔지만 일반적인 <span style="background: rgb(251,243,219)">MSS(최대 세그먼트 크기)</span>는 몇 개의 간단한 요청을 포함하기에는 충분히 여유 있다.

모든 종류의 HTTP의 요청이 파이프라인으로 처리될 수 있는 것은 아니다. <span style="background: rgb(251,243,219)">GET, HEAD, PUT</span> 그리고 <span style="background: rgb(251,243,219)">DELETE</span> 메서드 같은 <span style="background: rgb(251,243,219)">idempotent</span> 메서드만 가능하다. 실패가 발생한 경우에는 단순히 파이프라인 컨텐츠를 다시 반복하면 된다. 

오늘 날, 모든 <span style="background: rgb(251,243,219)">HTTP/1.1</span> 호환 프록시와 서버들은 파이프라닝을 지원해야 하지만 실제로는 많은 프록시 서버들은 제한을 가지고 있다. 모던 브라우저가 이 기능을 기본적으로 활성화하지 않은 이유다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HTTP란?
</h3>

<br>

- HTTP란 **HyperText Transport Protocol**의 약자로 웹서버와 클라이언트 간의 문서를 교환하기 위한 통신규약이다.
- World Wide Web(WWW)의 분산되어 있는 **Server와 Client** 간에 **Hypertext**를 이용한 정보교환이 가능하도록 하는 **통신 규약**이다.
- 1989년 Tim Berners Lee가 처음 설계
- HTTP는 웹에서만 사용하는 Protocol로 **TCP/IP** 기반으로 한 지점에서 다른 지점(보통 클라이언트와 서버)으로 **요청과 응답**을 전송한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HTTP의 특징
</h3>

<br>

- HTTP 메시지는 **HTTP Server**와 **HTTP Client**에 의해서 해석
- **TCP/IP 프로토콜**의 **Application 계층**에 위치
- **TCP Protocol**을 이용한다(Default Port 80)
- 현재 Version 1.1 (RFC 2616)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HTTP 1.1
</h3>

<br>

- **HTTP 1.0**의 성능 개선에 중점을 두었다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> HTTP 1.0의 문제점
</h4>

- 단순한 **OPEN, OPERATION, CLOSE**
- 매번 필요할 때마다 연결(비 지속성 연결방식) → 성능의 저하
- 한번에 얻어서 가져올 수 있는 데이터 양이 **제한**
- URL의 크기도 작으며, **캐시 기능이 미흡함(Last-Modified에 의존)**
- **GET/HEAD/POST method**만 허용

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> HTTP 1.1의 개선
</h4>

- **지속적인 연결**을 해 주는 **persistent connection** 지원
- **multiple request 처리** 가능
- **reqeust/response**가 **pipeline** 방식으로 진행
- **proxy server**와 **캐시 기능** 향상(Cache-Control)
- **GET, HEAD, POST, OPTIONS, DELETE, TRACE, CONNECT** 메소드 허용

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 파이프라이닝(Pipe Lining) 이란?
</h3>

<br>

- 응답 메시지가 도착하지 않은 상태에서 **연속적인 요구 메시지**를 서버에 전달
- 이때 서버는 요구 메시지를 **수신한 순서대로 응답 메시지를 클라이언트에 전달**
- **연결과 종료횟수**를 줄임으로서 네트워크 자원의 절약
- 발생하는 **패킷의 숫자**를 감소, **네트워크 트래픽** 감소

<br>

![](/images/Interview/post16/2022-01-15-13-13-57.png?style=centerme)

<br>
