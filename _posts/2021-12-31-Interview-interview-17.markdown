---
layout: post
title: AOP, Filter, Interceptor의 차이
date: 2021-12-31 11:00:00 0000
tags: [AOP, Filter, Interceptor]
categories: [Interview]
description: AOP, Filter, Interceptor의 차이에 관하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Filter & Interceptor & AOP
</h2>

<br>

자바 웹 개발을 하다보면 **공통적으로 처리**해야 할 업무들이 많다.

<br>

**Example**

- 로그인 관련(세션체크)처리
- 권한 체크
- XSS(Cross site script)방어
- pc와 모바일 웹의 분기처리
- 로그 처리
- 페이지 인코딩 변환
- (...)

<br>

공통업무에 관련된 코드를 모든 페이지 마다 작성 해야한다면 <span style="background: rgb(251,243,219)">중복된 코드</span>가 많아지게 되고 프로젝트 단위가 커질수록 <span style="background: rgb(251,243,219)">서버에 부하</span>를 줄 수도 있으며, 소스 관리도 되지 않는다.

<br>

<span style="color:#85144b; font-weight:bold">즉, 공통 부분은 빼서 따로 관리하는 게 좋다!</span>

<br>

위와 같은 공통처리를 위해 활용할 수 있는 것이 3가지가 있다.

<br>

1. **Filter**
2. **Interceptor**
3. **AOP**

<br>

> 스프링에서 사용되는 **Filter, Interceptor, AOP** 세 가지 기능은 모두 무슨 행동을 하기전에 **먼저 실행**하거나, 실행한 후에 **추가적인 행동**을 할 때 사용되는 기능들이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Filter, Interceptor, AOP의 흐름
</h3>

<br>

![](/images/Interview/post16/2022-01-01-15-48-41.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">Interceptor</span>와 <span style="background: rgb(251,243,219)">Filter</span>는 <span style="background: rgb(251,243,219)">Servlet 단위</span>에서 실행된다. 반면 <span style="background: rgb(251,243,219)">AOP</span>는 메소드 앞에 <span style="background: rgb(251,243,219)">Proxy 패턴</span>의 형태로 실행된다.

실행 순서를 보면 <span style="background: rgb(251,243,219)">Filter</span>가 가장 <span style="background: rgb(251,243,219)">바깥 쪽</span>에 있고, 그 안에 <span style="background: rgb(251,243,219)">Interceptor</span>와 <span style="background: rgb(251,243,219)">AOP</span>가 있는 형태다.

요청이 들어오면 <span style="background: rgb(251,243,219)">Filter → Interceptor → AOP → Interceptor → Filter</span> 순으로 거치게 된다.

<br>

하나 하나 살펴보자.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30">필터(Filter) 
</h3>

<br>

필터는 <span style="background: rgb(251,243,219)">Dispathcer Servlet</span>에 <span style="background: rgb(251,243,219)">요청</span>이 전달되기 <span style="background: rgb(251,243,219)">전/후</span>에 url 패턴에 맞는 모든 요청에 대해 <span style="background: rgb(251,243,219)">부가작업을 처리</span>할 수 있는 기능을 제공한다.

<br>

> **요청**과 **응답**을 거른 뒤 **정제**하는 역할을 한다. **서블릿 필터**는 **DispatcherServlet** 이전에 실행이 되는데 **필터**가 동작하도록 지정된 자원의 앞단에서 **요청내용을 변경**하거나, 여러가지 **체크**를 수행할 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 필터의 업무
</h4>

- <span style="background: rgb(251,243,219)">보안</span> 관련 공통 작업
- 모든 요청에 대한 <span style="background: rgb(251,243,219)">로깅</span> 또는 <span style="background: rgb(251,243,219)">감사</span>
- 이미지/데이터 <span style="background: rgb(251,243,219)">압축</span> 및 문자열 <span style="background: rgb(251,243,219)">인코딩</span>

<br>

<span style="background: rgb(251,243,219)">필터</span>에서는 <span style="background: rgb(251,243,219)">스프링과 무관</span>하게 <span style="background: rgb(251,243,219)">전역적</span>으로 처리해야 하는 <span style="background: rgb(251,243,219)">작업</span>들을 처리할 수 있다.

대표적인 예시로 <span style="background: rgb(251,243,219)">보안</span>과 관련된 <span style="background: rgb(251,243,219)">공통 작업</span>이 있다. <span style="background: rgb(251,243,219)">필터</span>는 <span style="background: rgb(251,243,219)">인터셉터</span>보다 <span style="background: rgb(251,243,219)">앞단</span>에서 동작하기 때문에 <span style="background: rgb(251,243,219)">전역적</span>으로 해야하는 보안 검사(XSS 방어 등)를 하여 올바른 요청이 아닐 경우 차단을 할 수 있다. 그러면 스프링 컨테이너까지 요청이 전달되지 못하고 차단되므로 <span style="background: rgb(251,243,219)">안정성</span>을 더욱 높일 수 있다.

또한 <span style="background: rgb(251,243,219)">필터</span>는 이미지나 데이터의 압축이나 문자열 인코딩과 같이 웹 애플리케이션에 전반적으로 사용되는 기능을 구현하기에 적당하다. <span style="background: rgb(251,243,219)">Filter</span>는 다음 체인으로 넘기는 <span style="background: rgb(251,243,219)">ServletRequest/ServletResponse 객체</span>를 조작할 수 있다는 점에서 <span style="background: rgb(251,243,219)">Interceptor</span>보다 훨씬 강력한 기술이다.

<br>

즉, <span style="background: rgb(251,243,219)">스프링 컨테이너</span>가 아닌 <span style="background: rgb(251,243,219)">톰캣</span>과 같은 <span style="background: rgb(251,243,219)">웹 컨테이너</span>에 의해 관리되므로 <span style="background: rgb(251,243,219)">DispatcherServlet</span>으로 가기 전에 <span style="background: rgb(251,243,219)">요청을 처리</span>하는 것이다.

<br>

![](/images/Interview/post16/2022-01-01-15-53-10.png?style=centerme)

<br>

필터를 추가하기 위해서는 javax.servlet의 <span style="background: rgb(251,243,219)">Filter 인터페이스를 구현</span>(implement)해야 하며 이는 다음의 3가지 메소드를 가지고 있다.

<br>

- init 메서드
- doFilter 메서드
- destroy 메서드

<br>

**init 메소드**

<span style="background: rgb(251,243,219)">init</span> 메소드는 <span style="background: rgb(251,243,219)">필터 객체</span>를 <span style="background: rgb(251,243,219)">초기화</span>하고 <span style="background: rgb(251,243,219)">서비스에 추가</span>하기 위한 메소드이다. 웹 컨테이너가 1회 init 메소드를 호출하여 필터 객체를 초기화하면 이후의 요청들은 <span style="background: rgb(251,243,219)">doFilter를</span> 통해 <span style="background: rgb(251,243,219)">전/후</span>에 처리된다.

<br>

**doFilter 메소드**

<span style="background: rgb(251,243,219)">doFilter</span> 메소드는 <span style="background: rgb(251,243,219)">url-pattern</span>에 맞는 <span style="background: rgb(251,243,219)">모든 HTTP 요청</span>이 <span style="background: rgb(251,243,219)">Dispatcher Servlet</span>으로 전달되기 <span style="background: rgb(251,243,219)">전/후</span>에 웹 컨테이너에 의해 실행되는 메소드이다. <span style="background: rgb(251,243,219)">doFilter</span>의 파라미터로는 <span style="background: rgb(251,243,219)">FilterChain</span>이 있는데, <span style="background: rgb(251,243,219)">FilterChain</span>의 <span style="background: rgb(251,243,219)">doFilter</span>를 통해 다음 대상으로 <span style="background: rgb(251,243,219)">요청을 전달</span>하게 된다.

<br>

**destroy 메소드**

<span style="background: rgb(251,243,219)">destroy</span> 메소드는 <span style="background: rgb(251,243,219)">필터 객체</span>를 서비스에서 제거하고 <span style="background: rgb(251,243,219)">사용하는 자원을 반환</span>하기 위한 메소드이다. 이는 웹 컨테이너에 의해 1번 호출되며 이후에는 이제 <span style="background: rgb(251,243,219)">doFilter</span>에 의해 처리되지 않는다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 인터셉터(Interceptor)
</h3>

<br>

<span style="background: rgb(251,243,219)">요청</span>에 대한 <span style="background: rgb(251,243,219)">작업 전/후</span>로 가로챈다고 보면 된다.

<span style="background: rgb(251,243,219)">필터</span>는 <span style="background: rgb(251,243,219)">스프링 컨텍스트 외부</span>에 존재하여 스프링과 무관한 자원에 대해 동작한다.

하지만 <span style="background: rgb(251,243,219)">인터셉터</span>는 스프링의 <span style="background: rgb(251,243,219)">DispatcherServlet</span>이 <span style="background: rgb(251,243,219)">컨트롤러</span>를 호출하기 <span style="background: rgb(251,243,219)">전, 후</span>로 끼어들기 때문에 <span style="background: rgb(251,243,219)">스프링 컨텍스트 내부</span>에서 <span style="background: rgb(251,243,219)">Controller</span>에 관한 요청과 응답에 대해 처리한다.

스프링의 <span style="background: rgb(251,243,219)">모든 빈 객체</span>에 <span style="background: rgb(251,243,219)">접근</span>할 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 인터셉터의 업무
</h4>

- 인증/인가 등과 같은 <span style="background: rgb(251,243,219)">공통 작업</span>
- <span style="background: rgb(251,243,219)">API 호출</span>에 대한 로깅 또는 감사
- Controller로 <span style="background: rgb(251,243,219)">넘겨주는 정보(데이터)</span>의 가공

<br>

<span style="background: rgb(251,243,219)">인터셉터</span>에서는 <span style="background: rgb(251,243,219)">클라이언트의 요청</span>과 관련되어 <span style="background: rgb(251,243,219)">전역적</span>으로 처리해야 하는 <span style="background: rgb(251,243,219)">작업</span>들을 처리할 수 있다.

대표적으로 <span style="background: rgb(251,243,219)">인증이나 인가</span>와 같이 <span style="background: rgb(251,243,219)">클라이언트 요청</span>과 관련된 작업 등이 있다. 이러한 작업들은 <span style="background: rgb(251,243,219)">컨트롤러로 넘어가기 전</span> 에 검사해야 하므로 <span style="background: rgb(251,243,219)">인터셉터</span>가 처리하기에 적합하다.

또한 <span style="background: rgb(251,243,219)">인터셉터</span>는 <span style="background: rgb(251,243,219)">필터</span>와 다르게 <span style="background: rgb(251,243,219)">HttpServletRequest</span>나 <span style="background: rgb(251,243,219)">HttpServletResponse</span> 등과 같은 객체를 제공받으므로 객체 자체를 조작할 수는 없다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Filter의 doFilter 메서드는 매개변수로 ServletRequest와 ServletResponse를 받고 Interceptor의 preHandle이나 postHandle은 HttpServletRequest를 받는다.<br><br>
ServletRequest는 기본적인 클라이언트 요청에 관한 모든 정보를 가지고 있다. 그리고 이 인터페이스는 다시 HttpServletRequest로 확장하여 HTTP 프로토콜 상에서 할 수 있는 일들이 포함되어져 있다.<br>
이 HttpServletReqeust는 서블릿의 service의 매개변수의 하나로 서블릿 프로그래머가 클라이언트의 요청에 관한 작업들을 핸들할 수 있도록하는 중요한 역할을 담당하고 있다.

</div>

<br>

**[HttpServletReqeust와 ServletRequest의 차이에 관한 링크](https://allinfo.tistory.com/494)**

<br>

대신 해당 객체가 <span style="background: rgb(251,243,219)">내부적으로 갖는 값</span>은 조작할 수 있으므로 컨트롤러로 넘겨주기 위한 <span style="background: rgb(251,243,219)">정보를 가공</span> 하기에 용이하다. 예를 들어 <span style="background: rgb(251,243,219)">JWT 토큰 정보를 파싱</span>해서 컨트롤러에게 사용자의 정보를 제공하도록 가공할 수 있는 것이다.

그 외에도 우리는 다양한 목적으로 <span style="background: rgb(251,243,219)">API 호출</span>에 대한 <span style="background: rgb(251,243,219)">정보들을 기록</span>해야 할 수 있다. 이러한 경우에 HttpServletRequest나 HttpServletResponse를 제공해주는 <span style="background: rgb(251,243,219)">인터셉터</span>는 <span style="background: rgb(251,243,219)">클라이언트의 IP</span>나 요청 정보들을 포함해 <span style="background: rgb(251,243,219)">기록</span>하기에 용이하다.

<br>

**preHandler()**

컨트롤러 메서드가 실행되기 전

<br>

**postHandler()**

컨트롤러 메서드 실행직 후 view페이지 렌더링 되기 전

<br>

**afterCompletion()**

view 페이지가 렌더링 되고 난 후

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 필터 vs 인터셉터 차이 및 용도
</h4>

<br>

![](/images/Interview/post16/2022-01-01-16-28-45.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> AOP
</h3>

<br>

<span style="background: rgb(251,243,219)">AOP</span>는 객체 지향의 프로그래밍을 했을 때, <span style="background: rgb(251,243,219)">AOP</span>을 줄일 수 없는 부분을 줄이기 위해 종단면(관점)에서 바라보고 처리한다.

주로 <span style="background: rgb(251,243,219)">로깅, 트랜잭션, 에러 처리</span> 등 비즈니스단의 메서드에서 조금 더 세밀하게 조정하고 싶을 때 사용한다.

Interceptor와 Filter와 달리 <span style="background: rgb(251,243,219)">메소드 전 후의 지점</span>에 자유롭게 설정이 가능하며 <span style="background: rgb(251,243,219)">주소, 파라미터, 어노테이션</span> 등 다양한 방법으로 대상을 지정할 수 있다.

<br>

**@Before**

대상 메서드의 수행 전

<br>

**@After**

대상 메서드의 수행 후

<br>

**@After-returning**

대상 메서드의 정상적인 수행 후

<br>

**@After-throwing**

예외 발생 후

<br>

**@Around**

대상 메서드의 수행 전/후
