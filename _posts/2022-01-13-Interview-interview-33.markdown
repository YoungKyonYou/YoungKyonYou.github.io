---
layout: post
title: Web Server와 WAS의 차이점
date: 2022-01-13 09:20:00 0000
tags: [Web Server, WAS]
categories: [Interview]
description: Web Server와 WAS의 차이
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Static Pages와 Dynamic Pages
</h3>

<br>

![](/images/Interview/post16/2022-01-13-11-50-46.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Static Pages
</h4>

- Web Server는 파일 경로 이름을 받아 경로와 일치하는 **file contents**를 반환한다.
- 항상 **동일한 페이지**를 반환한다.
- 서버에 **미리 저장된 파일**이 그대로 전달되는 웹 페이지
- Ex) **image, html, css, javascript 파일**과 같이 컴퓨터에 저장되어 있는 파일들

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Dynamic Pages
</h4>

- 인자의 내용에 맞게 **동적인 contents를 반환**한다.
- 요청에 대해서 **각각 다른 내용**을 보여준다.
- 개발자는 **Servlet에 doGet()**을 구현한다.
- 연결된 데이터베이스의 정보에 액세스하여 **사용자의 요구에 응답**하고 관련 정보를 제공한다.
- Ex) **Servlet, JSP, ASP, PHP** 등

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Web Server
</h3>

<br>

![](/images/Interview/post16/2022-01-13-11-50-59.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Web Server의 개념
</h4>

<span style="background: rgb(251,243,219)">소프트웨어</span>와 <span style="background: rgb(251,243,219)">하드웨어</span>로 구분한다.

- **1) 하드웨어**
  - Web 서버가 설치되어 있는 컴퓨터
- **2) 소프트웨어**
  - 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 **정적인 컨텐츠(.html .jpeg .css 등)**를 제공하는 컴퓨터 프로그램

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Web Server의 기능
</h3>

<br>

- **HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능**을 담당한다.
- 요청에 따라 아래의 **두 가지 기능** 중 적절하게 선택하여 수행한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 기능 1)
</h4>

- **정적인 컨텐츠** 제공
- WAS를 거치지 않고 **바로 자원을 제공**한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 기능 2)
</h4>

- **동적인 컨텐츠 제공**을 위한 **요청 전달**
- 클라이언트의 요청(Request)을 WAS에 보내고, **WAS가 처리한 결과**를 클라이언트에게 전달(응답, Response)한다.
  - 클라이언트는 일반적으로 **웹 브라우저**를 의미한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Web Server의 예
</h4>

- Ex) **Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등**

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Web Server 사용 이유
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> WAS가 해야 할 일의 부담을 줄이기 위해서
</h4>

WAS 앞에 웹 서버를 둬서 웹 서버에서는 **정적인 문서**만 처리하도록 하고, WAS는 **애플리케이션의 로직**만 수행하도록 기능을 분배하여 <span style="background: rgb(251,243,219)">서버의 부담</span>을 줄이기 위한 것이다.

<br>

![](/images/Interview/post16/2022-01-13-14-42-09.png?style=centerme)

<br>

위의 그림처럼 <span style="background: rgb(251,243,219)">WAS 앞에 웹 서버를 둠</span>으로써 서버의 부담을 줄일 수 있다. 웹 서버에서는 플러그인 형태로 WAS를 연결하면 <span style="background: rgb(251,243,219)">일 처리를 나눌 수 있다</span>.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> WAS의 환경설정 파일을 외부에 노출시키지 않도록 하기 위해서
</h4>

<span style="background: rgb(251,243,219)">클라이언트와 연결하는 포트</span>가 직접 WAS에 연결이 되어 있다면 <span style="background: rgb(251,243,219)">중요한 설정 파일들이 노출</span>될 수 있기 때문에 <span style="background: rgb(251,243,219)">WAS 설정 파일</span>을 외부에 노출시키지 않도록 하기 위해서 웹 서버를 앞단에 배치시킨다. 웹 서버와 WAS에 접근하는 <span style="background: rgb(251,243,219)">포트</span>가 다르기 때문에, WAS에 들어오는 포트에는 <span style="background: rgb(251,243,219)">방화벽을 쳐서 보안을 강화</span>할 수도 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 아파치(Apache)와 CGI, 그리고 톰캣(Tomcat)
</h4>

자바 웹 애플리케이션을 개발할 때 주로 사용하는 조합이 <span style="background: rgb(251,243,219)">아파치와 톰캣</span>일 것이다. 그러면 다른 언어들은 <span style="background: rgb(251,243,219)">톰캣 같은 WAS</span>가 없을까?

<br>

![](/images/Interview/post16/2022-01-13-14-44-43.png?style=centerme)

<br>

아파치에는 <span style="background: rgb(251,243,219)">CGI(Common Gateway Interface)</span>라는 것을 제공한다.

<span style="background: rgb(251,243,219)">CGI</span>는 이름 그대로 <span style="background: rgb(251,243,219)">인터페이스</span>로서, <span style="background: rgb(251,243,219)">웹 서버 상에서 프로그램을 동작</span>시키기 위한 방법을 정의한 <span style="background: rgb(251,243,219)">프로그램(또는 스크립트)</span>이다.

즉 <span style="background: rgb(251,243,219)">PHP, Perl, Python</span> 등의 언어들은 <span style="background: rgb(251,243,219)">CGI</span>를 구현해 놓았기 때문에 <span style="background: rgb(251,243,219)">아파치에서 다양한 언어</span>로 짜여진 각 프로그램을 실행할 수 있다. 예를 들어 아파치에 PHP 모듈을 설치했을 경우, 요청이 왔을 때 아파치는 <span style="background: rgb(251,243,219)">HTTP 헤더를 분석</span>하고 <span style="background: rgb(251,243,219)">파싱</span>하여 PHP로 파라미터를 넘겨준다. 그러면 PHP에서는 파라미터를 받아 <span style="background: rgb(251,243,219)">응답 할 HTML 문서를 만들어서 아파치에 전달</span>한다. HTML 문서를 전달 받은 아파치는 <span style="background: rgb(251,243,219)">CSS, JS, img 등 정적인 자원</span>들과 함께 브라우저로 반환한다.

그런데 자바는 CGI로 구현되어 있지 않다. 자바 자체가 무겁고, <span style="background: rgb(251,243,219)">Common 라이브러리</span>와 <span style="background: rgb(251,243,219)">JEE라는 플랫폼</span>이 존재하기 때문에 아파치에서 굳이 CGI를 제공하지 않는 것 같다. 그렇기 때문에 톰캣은 Default Servlet을 통해 정적인 파일을 제공해주기 때문에 웹 서버의 역할을 할 수 있는 것이다.

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> WAS(Web Application Server)
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> WAS의 개념
</h4>

- **DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공**하기 위해 만들어진 **Application Server**
- **HTTP**를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 **미들웨어(소프트웨어 엔진)**이다.
- **"웹 컨테이너(Web Container)"** 혹은 **"서블릿 컨테이너(Servlet Container)"**라고도 불린다.
  - **Container**란 **JSP, Servlet**을 실행시킬 수 있는 소프트웨어를 말한다.
  - 즉, **WAS는 JSP, Servlet 구동 환경**을 제공한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> WAS의 역할
</h4>

- **WAS = Web Server + Web Container**
- Web Server 기능들을 구조적으로 분리하여 처리하고자 하는 목적으로 제시되었다.
  - **분산 트랜잭션, 보안, 메시징, 쓰레드 처리** 등의 기능을 처리하는 분산 환경에서 사용된다.
  - 주로 **DB 서버**와 같이 수행된다.
- 현재는 WAS가 가지고 있는 **Web Server**도 정적인 컨텐츠를 처리하는 데 있어서 **성능상 큰 차이가 없다**

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> WAS의 주요 기능
</h3>

<br>

**1)** <span style="background: rgb(251,243,219)">프로그램 실행 환경</span>과 <span style="background: rgb(251,243,219)">DB 접속</span> 기능 제공<br>
**2)** 여러 개의 <span style="background: rgb(251,243,219)">트랜잭션(논리적인 작업 단위) 관리</span> 기능<br>
**3)** 업무를 처리하는 <span style="background: rgb(251,243,219)">비즈니스 로직 수행</span>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> WAS의 예
</h3>

<br>

- Ex) **Tomcat, JBoss, Jeus, Web Sphere 등**

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Web Server와 WAS를 구분하는 이유
</h3>

<br>

![](/images/Interview/post16/2022-01-13-11-57-13.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Web Server가 필요한 이유?
</h4>

- 클라이언트(웹 브라우저)에 **이미지 파일(정적 컨텐츠)을 보내는 과정**을 생각해보자.
  - 이미지 파일과 같은 **정적인 파일들**은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.
  - **클라이언트는 HTML 문서를 먼저 받고** 그에 맞게 필요한 이미지 파일들을 **다시 서버로 요청**하면 그때서야 이미지 파일을 받아온다.
  - **Web Server**를 통해 정적인 파일들을 **Application Server**까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.
- 따라서 Web Server에서는 **정적 컨텐츠만** 처리하도록 기능을 분배하여 **서버의 부담**을 줄일 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> WAS가 필요한 이유?
</h3>

<br>

- 웹 페이지는 **정적 컨텐츠와 동적 컨텐츠**가 모두 존재한다.
  - 사용자의 요청에 맞게 적절한 **동적 컨텐츠**를 만들어서 제공해야 한다.
  - 이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 **결과값을 모두 미리 만들어 놓고 서비스**를 해야 한다.
  - 하지만 이렇게 수행하기에는 **자원**이 절대적으로 **부족**하다.
- 따라서 WAS를 통해 **요청에 맞는 데이터를 DB**에서 가져와서 **비즈니스 로직에 맞게 그때그때 결과를 만들어서 제공**함으로써 자원을 효율적으로 사용할 수 있다.
- **Php,jsp, asp**와 같은 언어들을 사용해 **동적 페이지를 생성**할 수 있게 해준다.

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> WAS와 Web Server를 따로 두는 이유
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 기능을 분리하여 서버 부하 방지
</h4>

<span style="background: rgb(251,243,219)">WAS</span>는 DB 조회나 다양한 로직을 처리하느라 바쁘기 때문에 <span style="background: rgb(251,243,219)">단순한 정적 컨텐츠</span>는 <span style="background: rgb(251,243,219)">Web Server</span>에서 빠르게 <span style="background: rgb(251,243,219)">클라이언트에 제공</span>하는 것이 좋다. <span style="background: rgb(251,243,219)">WAS</span>는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버이다. 만약 정적 컨텐츠 요청까지 WAS가 처리한다면 정적 데이터 처리로 인해 부하가 커지게 되고, 동적 컨텐츠의 처리가 지연됨에 따라 수행 속도가 느려진다. 즉, 이로 인해 <span style="background: rgb(251,243,219)">페이지 노출 시간</span>이 늘어나게 될 것이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 물리적으로 분리하여 보안 강화
</h4>
 
<span style="background: rgb(251,243,219)">SSL에 대한 암복호화 처리</span>에 Web Server를 사용

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 여러 대의 WAS를 연결 가능
</h4>

<span style="background: rgb(251,243,219)">Load Balancing</span>을 위해서 Web Server를 사용할 수 있다. 그리고 <span style="background: rgb(251,243,219)">fail over(장애 극복), fail back처리</span>에 유리하다. 특히 <span style="background: rgb(251,243,219)">대용량 웹 애플리케이션</span>의 경우(여러 개의 서버 사용) <span style="background: rgb(251,243,219)">Web Server와 WAS를 분리</span>하여 무중단 운영을 위한 <span style="background: rgb(251,243,219)">장애 극복</span>에 쉽게 대응할 수 있다. 예를 들어, 앞 단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작함으로써 사용자는 오류를 느끼지 못하고 이용할 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 여러 웹 애플리케이션 서비스 가능
</h4>

예를 들어, 하나의 서버에서 <span style="background: rgb(251,243,219)">PHP Application</span>과 <span style="background: rgb(251,243,219)">Java Application</span>을 함께 사용하는 경우가 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 기타
</h4>

<span style="background: rgb(251,243,219)">접근 허용 IP관리</span> 및 2대 이상의 서버에서의 <span style="background: rgb(251,243,219)">세션 관리</span> 등도 Web Server에서 처리하면 효율적이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 정리
</h4>

즉, <span style="background: rgb(251,243,219)">자원 이용의 효율성</span> 및 <span style="background: rgb(251,243,219)">장애 극복, 배포</span> 및 <span style="background: rgb(251,243,219)">유지보수의 편의성</span>을 위해 Web Server와 WAS를 분리한다.

Web Server를 WAS 앞에 두고 필요한 WAS들을 <span style="background: rgb(251,243,219)">Web Server에 플러그인 형태</span>로 설정하면 더욱 <span style="background: rgb(251,243,219)">효율적인 분산 처리</span>가 가능하다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Web Service Architecture
</h3>

<br>

**1)** **_Client -> Web Server -> DB_**<br>
**2)** **_Client -> WAS -> DB_**<br>
**3)** **_Client -> Web Server -> WAS -> DB_**

<br>

![](/images/Interview/post16/2022-01-13-14-30-23.png?style=centerme)

<br>

**3번 구조의 동작과정**

1. <span style="background: rgb(251,243,219)">Web Server</span>는 웹 브라우저 클라이언트로부터 <span style="background: rgb(251,243,219)">HTTP 요청</span>을 받는다.
2. Web Server는 <span style="background: rgb(251,243,219)">클라이언트의 요청(Request)</span>을 WAS에 보낸다.
3. WAS는 관련된 <span style="background: rgb(251,243,219)">Servlet</span>을 <span style="background: rgb(251,243,219)">메모리에 올린다</span>.
4. WAS는 <span style="background: rgb(251,243,219)">web.xml을 참조</span>하여 해당 Servlet에 대한 <span style="background: rgb(251,243,219)">Thread를 생성</span>한다. (Thread Pool 이용)
5. <span style="background: rgb(251,243,219)">HttpServletRequest</span>와 <span style="background: rgb(251,243,219)">HttpServletResponse</span> 객체를 생성하여 <span style="background: rgb(251,243,219)">Servlet에 전달</span>한다.

- 5-1. <span style="background: rgb(251,243,219)">Thread</span>는 Servlet의 <span style="background: rgb(251,243,219)">service() 메서드</span>를 호출한다.
- 5-2. service() 메서드는 요청에 맞게 <span style="background: rgb(251,243,219)">doGet() 또는 doPost() 메서드를 호출</span>한다.(4에서 생성된 Thread가)

6. doGet() 또는 doPost() 메서드는 <span style="background: rgb(251,243,219)">인자에 맞게 생성된 적절한 동적 페이지</span>를 <span style="background: rgb(251,243,219)">Response 객체에 담아 WAS에 전달</span>한다.
7. WAS는 <span style="background: rgb(251,243,219)">Response 객체를 HttpResponse 형태</span>로 바꾸어 <span style="background: rgb(251,243,219)">Web Server에 전달</span>한다.
8. 생성된 <span style="background: rgb(251,243,219)">Thread</span>를 종료하고, <span style="background: rgb(251,243,219)">HttpServletRequest와 HttpServletResponse 객체를 제거</span>한다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 추가
</h3>

<br>

이제는 <span style="background: rgb(251,243,219)">WAS, Web Server</span>를 따로 두고 쓰는 이유가 성능 때문이라고 하는 건 잘못되었다.

<span style="background: rgb(251,243,219)">톰캣 5.5 이상</span>부터는 httpd의 native 모듈을 사용해서 정적 파일을 처리하는 기능을 제공하는데 이것이 순수 아파치 Httpd만 사용하는 것과 비교해서 성능이 전혀 떨어지지 않기 때문이다.

그럼에도 톰캣 앞에 아파치를 두는 이유는 하나의 서버에서 php 애플리케이션과 java 애플리케이션을 함께 사용하거나, httpd 서버를 <span style="background: rgb(251,243,219)">간단한 로드밸런싱</span>을 위해서 사용해야 할 때 필요하기 때문이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 왜 Tomcat이 아닌 Apache Tomcat이라고 부를까?
</h4>

앞에서 언급한대로 <span style="background: rgb(251,243,219)">정적 컨텐츠</span>를 처리하는 웹 서버에는 <span style="background: rgb(251,243,219)">Apache</span>가 있고, <span style="background: rgb(251,243,219)">동적 컨텐츠</span>를 처리하는 WAS 서버는 <span style="background: rgb(251,243,219)">Tomcat</span>이 있는데 Tomcat은 <span style="background: rgb(251,243,219)">Apache Tomcat</span>이라는 이름으로 많이 사용되어 혼란스러울 것이다. 붙여서 쓰는 이유는 2008년에 릴리즈 된 <span style="background: rgb(251,243,219)">Tomcat 5.5 버전</span>부터 <span style="background: rgb(251,243,219)">정적 컨텐츠를 처리하는 기능</span>이 추가되었는데, 이 기능이 순수 Apache를 사용하는 것에 비해 성능적 차이가 전혀 없으며 <span style="background: rgb(251,243,219)">Tomcat이 Apache의 기능을 포함</span>하고 있기 때문에 <span style="background: rgb(251,243,219)">Apache Tomecat</span>이라고 부르고 있다.
