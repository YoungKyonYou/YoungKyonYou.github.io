---
layout: post
title: 웹의 동작 원리
date: 2021-12-23 18:00:00 0000
tags: [Web]
categories: [Interview]
description: Web이 어떤 식으로 동작하는 가
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

웹의 동작 원리는 면접을 하면서 한 2~3번은 나온 것 같다. 하지만 질문 받을 때마다 확신있게 대답을 못한 것 같아서 이번 기회에 제대로 정리하고 다음에는 확실하게 말해보려 한다.

<br>

## Q: 브라우저에 naver.com 이라는 url를 치고 엔터를 누르면 내부적으로 어떻게 동작하는지 설명해주세요.

<br>

![](/images/Interview/post12/2021-12-23-21-36-38.png?style=centerme)

<br>

1. **사용자**가 웹 브라우저의 검색창에 **특정 사이트의 주소를 입력**한다.
   <br><br>
   &emsp;&emsp;&emsp;1-1. **웹 브라우저**가 **DNS**에게 특정 사이트의 (도메인)주소를 **요청**한다.
   <br><br>
2. **DNS**가 웹 브라우저에게 사이트의 **IP 주소**를 응답한다.
   <br><br>
3. **웹 브라우저**가 웹 서버에게 IP 주소를 이용하여 **html 문서를 요청**한다.
   <br><br>
4. **웹 서버**는 바로 웹 페이지를 공급하지 못하고, **웹 애플리케이션 서버와 데이터 베이스**에서 웹 페이지 작업을 처리한다.
   <br><br>
5. **작업 처리 결과**를 **웹 서버**로 보낸다.
   <br><br>
6. **웹 서버**는 웹 브라우저에게 **html 문서 결과를 응답**한다. 그리고 **웹 브라우저**는 화면에 웹 페이지를 **출력**한다.

---

### 웹 클라이언트

<br>

- 웹 클라이언트는 웹 서버에 자료를 요청하기 위해 http를 사용하는 클라이언트 프로그램

<br>

**ex: Internet Explorer, FireFox, Chrome, Safari 등**

<br>

---

### 웹 서버

<br>

- 소프트웨어와 하드웨어로 구분된다.

- <span style="color:#3D9970; font-weight:bold">하드웨어</span>
  - Web 서버가 설치되어 있는 컴퓨터
- <span style="color:#3D9970; font-weight:bold">소프트웨어</span>
  - 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 \*\*정적인 컨텐츠(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램

<br>

- <span style="color:#3D9970; font-weight:bold">Web Server의 기능</span>
  - HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당한
  - 웹 서버의 가장 중요한 기능은 클라이언트가 요청하는 HTML 문서나 각종 리소스를 전달하는 것
  - 정적인 컨텐츠 제공
  - WAS를 거치지 않고 바로 자원을 제공함
  - 동적인 컨텐츠 제공을 위한 요청 전달
  - 클라이언트의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.
  - 클라이언트는 일반적으로 웹 브라우저를 의미한다.

<br>

**ex: Apache, Nginx, Microsoft, Google 웹서버**이다.

---

<br>

### 웹 애플리케이션 서버(WAS)

<br>

- 브라우저 DBMS(데이터 베이스 관리 시스템) 사이에서 동작하는 미들웨어이다.
- DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
- “웹 컨테이너(Web Container)” 혹은 “서블릿 컨테이너(Servlet Container)”라고도 불린다

<br>

여기서 미들웨어란, 클라이언트와 DBMS 사이에서 **중개 역할을 하는 미들웨어**이다.

<br>

클라이언트는 단순히 미들웨어에게 요청을 보내고, 미들웨어에서는 대부분의 로직을 수행한다.

<br>

데이터를 조작할 일이 있으면 미들웨어가 DBMS에 접속하기도 한다.

- <span style="color:#3D9970; font-weight:bold">WAS의 기능</span>
  - 프로그램 실행 환경과 DB 접속 기능 제공
  - 여러 개의 트랜젝션(논리적인 작업 단위) 관리 기능
  - 업무를 처리하는 비즈니스 로직 수행

<br><br>

#### WAS의 기능

<br>

- WAS가 가지는 중요한 3가지 기능
  - 프로그램 실행 환경과 데이터 베이스 접속 기능을 제공
  - 여러 개의 트랜젝션을 관리
  - 업무를 처리하는 비즈니스 로직을 수행

<br>

이외에 웹 서버를 제공하는 기능도 한다.

---

<br>

### Static Pages와 Dynamic Pages

<br>

![](/images/Interview/post12/2021-12-23-22-13-58.png?style=centerme)

<br>

#### <span style="color:#3D9970; font-weight:bold">Static Pages</span>

<br>

- Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.
- 항상 동일한 페이지를 반환한다.
- ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 파일들

<br>

#### <span style="color:#3D9970; font-weight:bold">Dynamic Pages</span>

<br>

- 인자의 내용에 맞게 동적인 contents를 반환한다.
- 즉, 웹 서버에 의해서 실행되는 프로그램을 통해서 만들어진 결과물 -> **Servlet**: WAS 위에서 돌아가는 Java Program
- 개발자는 Servlet에 doGet()을 구현한다.

<br>

---

<br>

### Web Server와 WAS를 구분하는 이유

<br>

![](/images/Interview/post12/2021-12-23-22-23-54.png?style=centerme)

<br>

- <span style="color:#3D9970; font-weight:bold">Web Server가 필요한 이유</span>
  - 클라이언트(웹 브라우저)에 이미지 파일(정적 컨텐츠)을 보내는 과정을 생각해보자
    - 이미지 파일과 같은 정적인 파일들은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.
    - 클라이언트는 HTML 문서를 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아온다.
    - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.
  - 따라서 Web Server에서는 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있다.

<br>

- <span style="color:#3D9970; font-weight:bold">WAS가 필요한 이유</span>
  - 웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재한다.
    - 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 한다.
    - 이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 해야 한다.
    - 하지만 이렇게 수행하기에는 자원이 절대적으로 부족하다.
  - 따라서 WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있다.

<br>

- <span style="color:#3D9970; font-weight:bold">그렇다면 WAS가 Web Server의 기능도 모두 수행하면 되지 않을까?</span>

  - 기능을 분리하여 서버 부하 방지
    - WAS는 DB 조회나 다양한 로직을 처리하느라 바쁘기 때문에 단순한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에 제공하는 것이 좋다.
    - WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버이다.
    - 만약 정적 컨텐츠 요청까지 WAS가 처리한다면 정적 데이터 처리로 인해 부하가 커지게 되고, 동적 컨텐츠의 처리가 지연됨에 따라 수행 속도가 느려진다.
    - 즉, 이로 인해 페이지 노출 시간이 늘어나게 될 것이다.

  <br>

  - 물리적으로 분리하여 보안 강화
    - SSL에 대한 암호화 및 복호화 처리에 Web Server를 사용

  <br>

  - 여러 대의 WAS를 연결 가능
    - Load Balancing을 위해서 Web Server를 사용
    - fail over(장애 극복), fail back 처리에 유리
    - 특히 대용량 웹 애플리케이션의 경우 (여러 개의 서버 사용) Web Server와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있음
    - 예를 들어, 앞 단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작함으로써 사용자는 오류를 느끼지 못하고 이용할 수 있음

  <br>

  - 여러 웹 애플리케이션 서비스 가능
    - 예를 들어, 하나의 서버에서 PHP Application과 Java Application을 함께 사용하는 경우

  <br>

  - 기타
    - 접근 허용 IP 관리, 2대 이상의 서버에서의 세션 관리 등도 Web Server에서 처리하면 효율적

<br>

자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 Web Server와 WAS를 분리한다.

<br>

Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능하다.

<br>
