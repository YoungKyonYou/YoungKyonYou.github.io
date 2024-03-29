---
layout: post
title: Servlet
date: 2021-12-25 13:00:00 0000
tags: [Servlet]
categories: [Interview]
description: Servlet에 대하여
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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Servlet
</h2>

<br>

서블릿을 한 줄로 정의하자면 아래와 같다.

<br>

<span style="color:#093145; font-weight:bold">Servlet:</span> 클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술

<br>

**클라이언트가 어떠한 요청을 하면 그에 대한 결과를 다시 전송**해주어야 하는데, 이러한 역할을 하는 자바 프로그램이 **서블릿**이다.

예를 들어 어떠한 사용자가 로그인 버튼을 누른다.

그때 서버는 클라이언트의 아이디와 비밀번호를 확인하고, 다음 페이지를 띄워주어야 하는데, 이러한 역할을 하는 것이 바로 **서블릿(Servlet)**이다.

<span style="background: rgb(251,243,219)">서블릿</span>은 **웹 요청과 응답의 흐름을 간단한 메서드 호출만으로 체계적으로 다룰 수 있게 해주는 기술**이라고도 할 수 있다.

<br>

![](/images/Interview/post16/2022-01-01-00-56-58.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서블릿의 특징
</h3>

<br>

- 웹 통신에서 **요청과 응답**을 **처리**하고 결과를 반한
- **요청 당 쓰레드가 생성**되거나, 풀에서 가져와서 사용됨
- 주요 클래스로 **HttpServlet**이 있음
- 서블릿 등장이전에는 **CGI (Common Gateway Interface)** 기술이 있었는데 이는 요청 당 프로세스를 생성함
  - **서블릿**은 CGI에 비해서 작동이 빠르고, 플랫폼에 독립적이며, 보안이 좋고, 이식성이 강함
- **클라이언트 요청**에 대해 **동적**으로 작동하는 **웹 애플리케이션 컴포넌트**
- **html**을 사용하여 **요청에 응답**
- MVC 패턴에서 **Controller**로 이용
- 서블릿 객체는 **싱글톤**으로 관리<br>
  - 고객의 요청이 올 때마다 생성하는 것은 비효율적이기 때문<br>
  - 공유 변수 사용에 주의해야 함<br>
  - 서블릿 컨테이너가 종료되면 서블릿도 종료
    <br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서블릿 컨테이너(Servlet Container)
</h3>

![](/images/Interview/post14/2021-12-26-00-50-11.png?style=centerme)

<br>

**서블릿 컨테이너란 말 그대로 서블릿을 담고 관리해주는 컨테이너이다.**

<span style="background: rgb(251,243,219)">서블릿 컨테이너</span>는 구현되어 있는 servlet 클래스의 규칙에 맞게 서블릿을 관리해주며 클라이언트에서 요청을 하면 컨테이너는 <span style="color:#093145; font-weight:bold">HttpServletRequest, HttpServletResponse</span> 두 객체를 생성하며 post, get여부에 따라 <span style="background: rgb(251,243,219)">동적인 페이지를 생성</span>하여 응답을 보낸다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#3D9970; font-weight:bold">HttpServletRequest</span><br>
http 프로토콜의 request 정보를 서블릿에게 전달하기 위한 목적으로 사용하며 헤더 정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메서드와 Body의 Stream을 읽어 들이는 메서드를 가지고 있다.<br>

<span style="color:#3D9970; font-weight:bold">HttpServletResponse</span><br>
WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServletResponse 객체를 생성하여 서블릿에게 전달하고 이 객체를 활용하여 content type, 응답 코드, 응답 메시지 등을 전송한다.</div>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서블릿 컨테이너의 특징
</h3>

<br>

- **서블릿을 관리**하기 위한 모든 작업을 수행 (생성 / 호출 / 관리)
- java thread를 사용해서 **서블릿을 호출**
- **톰캣**처럼 서블릿을 지원하는 WAS를 **서블릿 컨테이너**라고 함
- 동시 요청을 위한 **멀티 쓰레드(Multi Thread) 처리**를 지원

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서블릿 컨테이너의 주요 기능
</h3>

<br>

<span style="color:#2ECC40; font-weight:bold">1. 생명주기 관리</span>

<span style="background: rgb(251,243,219)">서블릿의 생명주기</span>를 관리한다. 서블릿 컨테이너가 기동 되는 순간 서블릿 클래스를 로딩해서 인스턴스화하고, 초기화 메서드를 호출하고, 요청이 들어오면 적절한 서블릿 메서드를 찾아서 동작한다. 그리고 서블릿의 생명이 다하는 순간 <span style="background: rgb(251,243,219)">가비지 컬렉션</span>을 통해 메모리에서 제거한다.

<br>

<span style="color:#2ECC40; font-weight:bold">2. 통신 지원</span>

<span style="background: rgb(251,243,219)">클라이언트의 Request</span>를 받아주고 <span style="background: rgb(251,243,219)">Response</span>를 보낼 수 있게 웹 서버와 소켓을 만들어서 통신을 해준다. 우리가 통신을 한다고 생각할 때 소켓을 만들고, 특정 포트를 리스닝하고, 연결 요청이 들어오면 스트림을 생성해서 요청을 받는다고 알고 있는데 이 과정을 <span style="background: rgb(251,243,219)">서블릿 컨테이너</span>가 대신 해주고 있는 것이다. 서블릿 컨테이너는 이렇게 소켓을 만들고 listen, accept 등의 기능을 API로 제공하여 복잡한 과정을 생략할 수 있게 해주고 개발자로서 <span style="background: rgb(251,243,219)">비즈니스 로직에 더욱 집중</span>할 수 있게 만들어준다.

<br>

<span style="color:#2ECC40; font-weight:bold">3. 멀티스레딩 관리</span>

서블릿 컨테이너는 해당 서블릿의 요청이 들어오면 스레드를 생성해서 작업을 수행한다. 그렇기에 동시에 여러 요청이 들어와도 <span style="background: rgb(251,243,219)">멀티스레딩 환경</span>으로 동시다발적인 작업을 관리할 수 있다. 또한, 이렇게 한번 메모리에 올라간 스레드는 다시 생성할 필요가 없기에 <span style="background: rgb(251,243,219)">메모리 관리에 효율적</span>이다.

<br>

<span style="color:#2ECC40; font-weight:bold">4. 선언적인 보안관리</span>

<span style="background: rgb(251,243,219)">서블릿 컨테이너</span>는 보안 관련된 기능을 지원한다. 그렇기에 서블릿 또는 자바 클래스 안에 보안 관련된 메서드를 구현하지 않아도 된다. 대체적으로 보안관리는 XML 배포 서술자에 기록하기 때문에 보안 이슈로 소스를 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서블릿 엔진 (=서블릿 컨테이너) ex: 톰캣
</h3>

<br>

- Tomcat, Jetty, Undertow 같은 WAS(Web Application Server)가 **서블릿 엔진**
  - **서블릿**을 실행시킬 수 있음
  - 세션 관리, 네트워크 서비스, 서블릿 생명주기 관리, MIME 기반 메시지 인코딩, 디코딩 등의 기능을 제공

<br>

#### 참고 할 만한 좋은 링크

**[서블릿과 JSP의 차이 및 MVC가 나타나게 된 배경](https://steady-coding.tistory.com/463)**
