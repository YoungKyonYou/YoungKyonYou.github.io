---
layout: post
title: 쿠키 vs 세션 vs 캐시
date: 2022-01-02 14:00:00 0000
tags: [Cookie, Session, Cache]
categories: [Interview]
description: 쿠키, 세션 그리고 캐시의 차이
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> 쿠키와 세션
</h2>

<br>

쿠키와 세션을 사용하는 이유가 뭘까?

그것은 바로 **HTTP 프로토콜의 특징이자 약점을 보완**하기 위해서 일 것이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HTTP 프로토콜의 특징
</h3>

<br>

**1. Connectionless 프로토콜 (비연결 지향)**

클라이언트가 서버에 요청(Reqeust)을 했을 때, 그 요청에 맞는 응답(Response)을 보낸 후 <span style="background: rgb(251,243,219)">연결을 끊는 처리방식이다.</span>

- HTTP 1.1 버전에서 커넥션을 계속 유지하고, 요청(Request)에 재활용하는 기능이 추가되었다. (HTTP Header)에 <span style="background: rgb(251,243,219)">keep alive</span> 옵션을 주어 커넥션을 재활용하게 한다. HTTP 1.1 버전에선 디폴트(default) 옵션이다.
- HTTP가 TCP 위에서 구현되었기 때문에(TCP:연결 지향, UDP: 비연결 지향) 연결 지향적이라고 할 수 있다는 얘기가 있어 논란이 있지만, 아직까진 네트워크 관점에서 <span style="background: rgb(251,243,219)">keep-alive</span>는 옵션으로 두고, 서버 측에서 비연결 지향적인 특성으로 커넥션 관리에 대한 비용을 줄이는 것이 명확한 장점으로 보기 때문에 비연결 지향으로 알아두었다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

비연결지향이라는 특성 덕분에 계속해서 통신 연결을 유지하지 않기 때문에 리소스 낭비가 줄어드는 것은 장점이지만 통신할 때마다 새로운 커넥션을 열기 때문에 클라이언트는 내가 누구인지 인증을 계속해야 하는 단점이 생긴다.</div>

<br>

**2. Stateless 프로토콜**

커넥션을 끊는 순간 클라이언트와 서버의 통신이 끝나며 <span style="background: rgb(251,243,219)">상태 정보는 유지하지 않는 특성이</span> 있다.

- 클라이언트와 첫 번째 통신에서 데이터를 주고 받았다 해도, 두 번째 통신에서 이전 데이터를 유지하지 않는다.
- 하지만, 실제로는 데이터 유지가 필요한 경우가 많다.

<br>

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

정보가 유지되지 않으면, 매번 페이지를 이동할 때마다 로그인을 다시 하거나, 상품을 선택했는데 구매 페이지에서 선택한 상품의 정보가 없거나 하는 등의 일이 발생할 수 있다.<br><br>
→ 따라서, Stateful한 경우를 대처하기 위해 쿠키와 세션을 사용한다!
<br>

쿠키와 세션의 차이점은 크게 상태 정보의 저장 위치이다.<br>

쿠키는 '클라이언트(=로컬PC)에 저장하고 세션은 '서버'에 저장한다.

</div>

<br>

서버와 클라이언트가 통신을 할 때 통신이 연속적으로 이어지지 않고 한 번 통신이 되면 끊어진다. 따라서 서버는 클라이언트가 누구인지 계속 <span style="background: rgb(251,243,219)">인증</span>을 해줘야 한다. 하지만 그것은 매우 귀찮고 번거로운 일이다.

그런 번거로움을 해결하는 방법이 바로 <span style="background: rgb(251,243,219)">쿠기와 세션</span>이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 쿠키 Cookie
</h3>

<br>

HTTP의 일종으로 사용자가 어떠한 웹 사이트를 방문할 경우, 그 사이트가 사용하고 있는 서버에서 <span style="background: rgb(251,243,219)">사용자의 컴퓨터에 저장하는 키와 값이 들어있는 작은 데이터 파일</span>이다.

HTTP에서 클라이언트의 상태 정보를 클라이언트의 PC에 저장하였다가 <span style="background: rgb(251,243,219)">필요시 정보를 참조하거나 재사용할 수 있다.</span>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 쿠키의 특징
</h4>

- <span style="background: rgb(251,243,219)">이름, 값, 만료일(저장기간), 경로 정보로 구성</span>되어 있다.
  - 유효 시간이 부여되면 브라우저가 종료되어도 인증정보가 유효하다.
- <span style="background: rgb(251,243,219)">클라이언트에 총 300개의 쿠키를 저장</span>할 수 있다.
- 하나의 <span style="background: rgb(251,243,219)">도메인 당 20개</span>의 쿠키를 가질 수 있다.
- <span style="background: rgb(251,243,219)">하나의 쿠키는 4KB(=4096byte)까지 저장</span> 가능하다.
- 쿠키는 사용자가 요청하지 않아도 브라우저가 Request 시에 Request Header에 넣어서 자동으로 전송한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 쿠키의 동작 순서
</h4>

- 클라이언트가 <span style="background: rgb(251,243,219)">페이지를 요청</span>한다. (사용자가 웹사이트에 접근)
- 웹 서버는 클라이언트가 보낸 Request-Header에 <span style="background: rgb(251,243,219)">쿠키가 없음을</span> 판별하고 통신 상태(UserId, Password, 조작상태, 방문횟수 등)을 저장한 쿠키를 response한다.
  - 생성된 쿠키를 <span style="background: rgb(251,243,219)">헤더에 포함</span>시켜 응답한다.
- 넘겨받은 쿠키는 <span style="background: rgb(251,243,219)">클라이언트가(웹 브라우저) 가지고 있다가</span>(로컬 PC에 저장)다시 서버에 요청할 때 요청과 함께 HTTP 헤더에 쿠키를 넣어서 전송한다.
- 서버에서는 쿠키 정보를 읽어 이전 상태 정보를 확인할 후 응답한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 사용 예시
</h4>

- 방문 사이트에서 로그인 시, "아이디와 비밀번호를 저장하시겠습니까?"
- 팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크
- 쇼핑몰 장바구니
- 자동 로그인

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 세션 Session
</h3>

<br>

**일정 시간 동안** 같은 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술이다. 여기서 일정 시간은 방문자가 웹 브라우저를 통해 웹 서버에 접속한 시점부터 웹 브라우저를 종료하여 연결을 끝내는 시점을 말한다.

즉, **방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라고 한다.**

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 세션 특징
</h4>

- 웹 서버에 <span style="background: rgb(251,243,219)">웹 컨테이너의 상태를 유지하기 위한 정보를 저장한다.</span>
- 쿠키를 기반으로 두고 있지만, 쿠키와 달리 사용자 정보 저장을 서버 측에서 관리
- 브라우저를 닫거나, 서버에서 세션을 삭제했을 때만 삭제가 되므로, <span style="background: rgb(251,243,219)">쿠키보다 비교적 보안이 좋다.</span>
- 각 클라이언트에 <span style="background: rgb(251,243,219)">고유 Session ID를 부여한다.</span> Session ID로 클라이언트를 구분해 각 요구에 맞는 서비스를 제공

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 세션의 동작 순서
</h4>

- 클라이언트가 서버에 접속시, <span style="background: rgb(251,243,219)">세션 ID를 발급</span>한다.
  - 서버가 응답할 때 HTTP 헤더(**Set-Cookie**)에 **Session ID**를 포함해서 전송
  - 쿠키에 Session ID를 JSESSIONID라는 이름으로 저장 (Set-Cookie: JSESSIONID=xslei13f)
- 클라이언트는(웹 브라우저) 다시 페이지에 접속할때, <span style="background: rgb(251,243,219)">다음 요청 때 부여된 Session ID가 담겨 있는 쿠키를 HTTP 헤더</span>에 넣어서 전송(Cookie: JSEESIONID=xslei13f)
- 서버는 Request Header에 <span style="background: rgb(251,243,219)">쿠키정보(세션ID)로 클라이언트를 판별</span>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 사용 예시
</h4>

- 로그인
- 화면을 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> SESSION ID 보안의 취약점
</h4>

**세션 해킹**: 홈페이지 관리자의 세션 아이디를 탈취 => 쿠키값을 관리자의 세션 아이디로 변경한다. => 관리자 권한으로 이용

**예방법**: 세션에 로그인 했을 때의 IP를 저장 => 페이지 이동 시마다, 현재 IP와 세션의 IP/브라우저 정보(UserAgent)가 같은지 검사

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 쿠키와 세션의 차이
</h3>

- 쿠키와 세션은 비슷한 역할을 하며, 동작 원리도 비슷하다. 그 이유는 세션도 결국 쿠키를 사용하기 때문이다.
- 큰 차이점은 **사용자의 정보가 저장되는 위치**이다. <span style="background: rgb(251,243,219)">쿠키는 서버의 자원을 전혀 사용하지 않으며,</span> **세션은 서버의 자원을 사용**한다.
- 보안 면에서 세션이 더 우수하다.
- 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 request에서 **스니핑** 당할 우려가 있어서 **보안에 취약**하지만 세션은 쿠키를 이용해서 session-id만 저장하고 그것으로 구분하여 서버에서 처리하기 때문에 비교적 **보안성이 높다**
- **라이프 사이클**은 쿠키도 만료기간이 있지만 <span style="background: rgb(251,243,219)">파일로 저장되기 때문에 브라우저를 종료해도 정보가 유지</span>될 수 있다. 또한 만료기간을 따로 지정해 **쿠키를 삭제할 때까지 유지할 수도** 있다.
- 반면에 세션도 만료기간을 정할 수 있지만, **브라우저가 종료되면 만료기간에 상관없이 삭제**된다.
- **속도 면에서 쿠키가 더 우수**하며 쿠키는 쿠키에 정보가 있기 때문에 서버에 요청 시 속도가 빠르고 세션은 정보가 서버에 있기 때문에 처리가 요구되어 비교적 느린 속도를 낸다

<br>

![](/images/Interview/post16/2022-01-02-14-33-51.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 세션을 사용하면 좋은데 왜 쿠키를 사용할까?
</h3>

**A:** 세션이 쿠키에 비해 보안이 높은 편이나 쿠키를 사용하는 이유는 세션은 서버에 저장되고, 서버의 자원을 사용하기에 서버 자원에 한계가 있다.

이로 인해 속도가 느려질 수 있고 자원관리 차원에서 쿠키와 세션을 적절한 요소 및 기능에 병행 사용하여 서버 자원의 낭비를 방지하며 웹 사이트의 속도를 높일 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 캐시 Cache
</h3>

**캐시**는 웹 페이지 요소를 저장하기 위한 임시 저장소이다.

쿠키/세션은 정보를 저장하기 위해 사용된다.

캐시는 웹 페이지를 빠르게 렌더링할 수 있도록 도와주고 쿠키/세션은 사용자의 인증을 도와준다.

<br>

- 캐시는 이미지, 비디오, 오디오, css, js파일 등 데이터나 값을 미리 복사해 놓는 리소스 파일들의 임시 저장소이다.
- 저장 공간이 작고 비용이 비싼 대신 빠른 성능을 제공한다.
- 같은 웹 페이지에 접속할 때 사용자의 PC에서 로드하므로 서버를 거치지 않아도 된다.
- 이전에 사용된 데이터가 다시 사용될 가능성이 많으면 캐시 서버에 있는 데이터를 사용한다.
- 그래서 다시 사용될 확률이 있는 데이터들이 빠르게 접근할 수 있어진다. (페이지 로딩 속도 ↑)
- 캐시 히트(hit): 캐시를 사용할 수 있는 경우 (ex: 이전에 왔던 요청이랑 같은 게 왔을 때)
- 캐시 미스(miss): 캐시를 사용할 수 없는 경우 (ex: 웹서버로 처음 요청했을 때)
