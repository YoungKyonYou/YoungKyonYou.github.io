---
layout: post
title: REST API와 HTTP Methods
date: 2022-01-02 10:00:00 0000
tags: [REST API, GET, POST, PUT, DELETE]
categories: [Interview]
description: REST API와 HTTP Methods에 관하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> REST API와 HTTP METHOD
</h2>

<br>

REST API는 웹에서 데이터를 <span style="background: rgb(251,243,219)">전송 및 처리</span>하는 방법을 정의한 인터페이스를 말한다.

<br>

HTTP METHOD를 통해 해당 자원에 대한 CRUD Operation을 적용하여 아래와 같이 사용한다.

<br>

- Create: 데이터 생성 (POST)
- Read: 데이터 조회 (GET)
- Update: 데이터 수정 (PUT)
- Delete: 데이터 삭제 (DELETE)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REST 구성
</h3>

<br>

쉽게 말해 REST API는 다음의 구성으로 이루어져 있다.

<br>

- **자원(RESOURCE) - URI**
- **행위(Verb) - HTTP METHOD**
- **표현(Representations)**

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 자원(RESOURCE)
</h4>

<br>

- 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
- 자원을 구별하는 ID는 `/orders/order_id/1`와 같은 HTTP URI이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 행위(Verb)
</h4>

<br>

- HTTP 프로토콜의 Method를 사용한다.
- HTTP 프로토콜은 <span style="background: rgb(251,243,219)">GET, POST, PUT, DELETE</span>와 같은 메서드를 제공한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 표현 (Representation of Resource)
</h4>

<br>

- Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
- REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타낼 수 있다.
- 현재는 JSON으로 주고 받는 것이 대부분이다.

<br>

![](/images/Interview/post16/2022-01-02-12-14-32.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REST의 특징
</h3>

<br>

**1)** <span style="color:#093145; font-weight:bold">Uniform (유니폼 인터페이스)</span>

Uniform Interface는 URI로 지정한 <span style="background: rgb(251,243,219)">리소스에 대한 조작</span>을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말한다.

<br>

**2)** <span style="color:#093145; font-weight:bold">Stateless (무상태성)</span>

REST는 무상태성 성격을 갖는다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다. <span style="background: rgb(251,243,219)">세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기</span> 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 <span style="background: rgb(251,243,219)">구현이 단순</span>해진다.

<br>

**3)** <span style="color:#093145; font-weight:bold">Cacheable (캐시 가능)</span>

REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 <span style="background: rgb(251,243,219)">기존 인프라를 그대로 활용</span>이 가능하다. 따라서 HTTP가 가진 <span style="background: rgb(251,243,219)">캐싱 기능이 적용</span> 가능합니다. HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.

<br>

**4)** <span style="color:#093145; font-weight:bold">Self-Descriptiveness (자체 표현 구조)</span>

REST의 또 다른 특징 중 하나는 REST API 메시지만 보고도 이를 <span style="background: rgb(251,243,219)">쉽게 이해 할 수 있는 자체 표현 구조</span>로 되어 있는 것이다.

<br>

**5)** <span style="color:#093145; font-weight:bold">Client-Server 구조</span>

REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 <span style="background: rgb(251,243,219)">각각의 역할이 확실히 구분되기</span> 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 <span style="background: rgb(251,243,219)">서로간 의존성이 줄어들게 된다.</span>

<br>

**6)** <span style="color:#093145; font-weight:bold">계층형 구조</span>

REST 서버는 다중 계층으로 구성될 수 있으며 <span style="background: rgb(251,243,219)">보안, 로드 밸런싱, 암호화 계층을 추가해</span> 구조상의 <span style="background: rgb(251,243,219)">유연성을</span> 둘 수 있고 <span style="background: rgb(251,243,219)">PROXY, 게이트웨이</span> 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REST API 디자인 가이드
</h3>

<br>

REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있다.

**첫 번째,** URI는 정보의 <span style="background: rgb(251,243,219)">자원</span>을 표현해야 한다.

**두 번째,** 자원에 대한 <span style="background: rgb(251,243,219)">행위</span>는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

> 꼭 기억하기!!

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> REST API 중심 규칙
</h4>

<br>

**1)** URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용)

```url
GET /members/delete/1
```

<br>

위와 같은 방식은 <span style="background: rgb(251,243,219)">REST를 제대로 적용하지 않은</span> URI이다. URI는 <span style="background: rgb(251,243,219)">자원</span>을 표현하는데 중점을 두어야 한다. <span style="background: rgb(251,243,219)">delete</span>와 같은 행위에 대한 표현이 들어가서는 안된다.

<br>

**2)** 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

위의 잘못 된 URI를 HTTP Method를 통해 수정해 보자.

```uri
DELETE /members/1
```

<br>

으로 수정할 수 있다. 회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현한다.

<br>

<span style="color:#85144b; font-weight:bold">회원정보를 가져오는 URI</span>

```uri
GET /members/show/1    (x)
GET /members/1         (o)
```

<br>

<span style="color:#85144b; font-weight:bold">회원을 추가할 때</span>

```uri
GET /members/insert/2    (x)   - GET 메서드는 리소스 생성에 맞지 않는다.
POST /members/2          (o)
```

<br>

**3)** 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

```uri
   http://restapi.example.com/houses/apartments
   http://restapi.example.com/animals/mammals/whales
```

<br>

**4)** URI 마지막 문자로 슬래시(/)를 포함하지 않는다.

URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

```uri
    http://restapi.example.com/houses/apartments/ (X)
    http://restapi.example.com/houses/apartments  (0)
```

<br>

**5)** 하이픈(-)은 URI 가독성을 높이는데 사용

URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI 경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있다.

<br>

**6)** 밑줄(\_)은 URI에 사용하지 않는다.

글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋다.(가독성)

<br>

**7)** URI 경로에는 소문자가 적합하다.

URI 경로에 대문자 사용은 피하도록 해야 합니다. 대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이지요.

<br>

**8)** 파일 확장자는 URI에 포함시키지 않는다.

```uri
    http://restapi.example.com/members/soccer/345/photo.jpg (X)
```

<br>

**8)** 리소스 간의 관계 표현 방법

REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현방법으로 사용한다.

```uri
/리소스명/리소스 ID/관계가 있는 다른 리소스명

ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

<br>

만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있다. 예를 들어 사용자가 '좋아하는' 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용될 수 있다.

```uri
GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REST의 장점
</h3>

<br>

- HTTP 프로토콜의 인프라를 그대로 사용하므로 <span style="background: rgb(251,243,219)">REST API 사용을 위한 별도의 인프라</span>를 구축할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 <span style="background: rgb(251,243,219)">모든 플랫폼에서 사용이</span> 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 <span style="background: rgb(251,243,219)">범용성을</span> 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 <span style="background: rgb(251,243,219)">의도하는 바를 쉽게 파악</span>할 수 있다.
- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- <span style="background: rgb(251,243,219)">서버와 클라이언트의 역할을</span> 명확하게 <span style="background: rgb(251,243,219)">분리</span>한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> REST의 단점
</h3>

<br>

- 표준이 존재하지 않아 <span style="background: rgb(251,243,219)">정의가 필요하다</span>
- 사용할 수 있는 <span style="background: rgb(251,243,219)">메소드가 4가지</span> 밖에 없다.
- HTTP Method 형태가 <span style="background: rgb(251,243,219)">제한적</span>이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 정보의 값을 처리해야 하므로 <span style="background: rgb(251,243,219)">전문성이 요구</span>된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 왜 RESTful APIs를 만드는 것일까?
</h3>

<br>

- RESTful API를 개발하는 가장 큰 이유는 <span style="background: rgb(251,243,219)">Client Side를 정형화된 플래폼이 아닌 모바일, PC, 애플리케이션 등 플랫폼에 제약을 두지 않는 것을 목표로 했기 때문이다.</span> -즉, 2010년 이전만 해도 Server Side에서 데이터를 전달해주는 Client 프로그램의 대상은 PC 브라우저로 그 대상이 명확했다. 그렇다 보니 그냥 JSP ASP PHP 등을 이용한 웹페이지를 구성하고 작업을 진행하면 됐다.
- 하지만 스마트 기기들이 등장하면서 TV, 스마트 폰, 테블릿 등 Client 프로그램이 다양화되고 그에 맞춰 Server를 일일이 만든다는 것은 꽤 비효율적인 일이 되어 버렸다.
- 이런 과정에서 개발자들은 Client Side를 전혀 고려하지 않고 메시지 기반, XML, JSON과 같은 <span style="background: rgb(251,243,219)">Client에서 바로 객체로 치환 가능한 형태의 데이터 통신을 지향하게 되면서 Server와 Client의 역할을 분리하게 되었다.</span>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HTTP Methods
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> GET
</h4>

<br>

GET 메소드는 주로 <span style="background: rgb(251,243,219)">데이터를 읽거나(Read) 검색(Retrieve)할</span> 때에 사용되는 메서드이다.

만약에 GET요청이 성공적으로 이루어진다면 XML이나 JSON과 함께 200(Ok) HTTP 응답 코드를 리턴한다. 에러가 발생하면 주로 404 (Not found) 에러나 400 (Bad Request) 에러가 발생한다.

<br>

- HTTP 명세에 의하면 GET 요청은 오로지 <span style="background: rgb(251,243,219)">데이터를 읽을 때만</span> 사용되고 <span style="background: rgb(251,243,219)">수정할</span> 때는 사용하지 않는다.
- GET 요청은 <span style="background: rgb(251,243,219)">idempotent</span> 하다.
- 같은 요청을 여러 번 하더라도 변함없이 <span style="background: rgb(251,243,219)">항상 같은 응답을</span> 받을 수 있다.
- 데이터를 <span style="background: rgb(251,243,219)">변경하는 연산에</span> 사용하면 안된다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

멱등성(Idempotence)이란?<br><br>
멱등성이란 여러번 수행해도 결과가 같음을 의미한다. 즉, 호출로 인하여 데이터가 변형이 되지 않는다는 것을 의미한다.</div>

<br>

**Example**

```url
GET /user/1
```

<br>

데이터를 조회하는 것이기 때문에 요청시에 <span style="background: rgb(251,243,219)">Body</span> 값과 <span style="background: rgb(251,243,219)">Content-Type가</span> 비워져있다. 조회할 데이터에 대한 정보는 URL을 통해서 파라미터를 받고 있는 모습을 볼 수 있다.

데이터 조회에 성공한다면 <span style="background: rgb(251,243,219)">Body</span> 값에 데이터 값을 저장하여 <span style="background: rgb(251,243,219)">성공 응답을</span> 보낸다.

GET은 <span style="background: rgb(251,243,219)">캐싱이</span> 가능하여 같은 데이터를 한번 더 조회할 경우에 <span style="background: rgb(251,243,219)">저장한 값을 사용하여</span> 조회 속도가 빨라진다.(이미지 같은 정적 컨텐츠는 데이터 양이 크고, 변경된 일이 적기 때문에 동일한 요청이 ㅂ라생했을 경우 서버로 요청을 보내지 않고 캐시된 데이터를 사용)

<br>

또한, **GET** 방식으로 <span style="background: rgb(251,243,219)">데이터를 보내는</span> 것이 가능하다. **GET** 요청시 필요한 **데이터**를 <span style="background: rgb(251,243,219)">쿼리스트링</span> 형식으로 **header**에 담는다.(이 정보는 HTTP 패킷의 헤더에 포함되어 서버에 요청됨)

**쿼리스트링**은 URL의 끝에 **?**와 함께 **키, 값** 쌍으로 파라미터를 붙여준 문자열이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> POST
</h4>

<br>

POST 메소드는 주로 새로운 리소스를 생성(creat)할 때 사용된다. 조금 더 구체적으로 POST는 하위 리소스(부모 리소스의 하위 리소스)들을 생성하는데 사용된다. 성공적으로 creation을 완료하면 201 (Created) HTTP 응답을 반환한다.

<br>

POST 방식은 GET 방식과 달리 **데이터 전송**을 기반으로 한 요청 메서드이다. GET 방식은 **URL**에 데이터를 붙여서 보내는 반면 **POST** 방식은 **URL**에 붙여서 보내지 않고 <span style="background: rgb(251,243,219)">BODY에다가 데이터를 넣어서 보낸다.</span>

따라서, 헤더필드 중 <span style="background: rgb(251,243,219)">BODY의 데이터를 설명하는 Content-Type</span>이라는 헤더 필드가 들어가고 어떤 데이터 타입인지 명시한다.

<br>

- POST 요청은 idempotent 하지 않다.
- 같은 POST 요청을 반복해서 했을 때 항상 같은 결과물이 나오는 것을 보장하지 않는다.
- 두 개의 같은 POST 요청을 보내면 같은 정보를 담은 두 개의 다른 resource를 반환할 가능성이 높다.

<br>

**Example**

```url
POST /user
body : {date : "example"}
Content-Type : "application/json"
```

<br>

데이터를 생성하는 것이기 때문에 요청시에 <span style="background: rgb(251,243,219)">Body 값과 Content-Type 값</span>을 작성해야 한다. 해당 예시는 JSON을 통해서 작성된 예시다.

URL을 통해서 데이터를 받지 않고, Body 값을 통해서 받는다.

데이터 조회에 성공한다면 Body 값에 저장한 데이터 값을 저장하여 성공 응답을 보낸다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> PUT
</h4>

<br>

PUT은 리소스를 생성 / 업데이트하기 위해 서버로 데이터를 보내는 데 사용된다.
**POST**와 **PUT**의 차이는 <span style="background: rgb(251,243,219)">멱등성 idempotent</span>에 있다.

<br>

- PUT 요청은 <span style="background: rgb(251,243,219)">idempotent</span> 하다.
- 동일한 PUT 요청을 여러 번 호출하면 <span style="background: rgb(251,243,219)">항상 동일한 결과가</span> 생성된다.

<br>

```url
PUT /user/1
body : {date : "update example"}
Content-Type : "application/json"
```

<br>

데이터를 수정하는 것이기 때문에 요청시에 <span style="background: rgb(251,243,219)">Body 값과 Content-Type 값</span>을 작성해야 한다. 해당 예시는 JSON을 통해서 작성된 예시다.

URL을 통해서 어떠한 데이터를 수정할지 파라미터를 받는다. 그리고 수정할 데이터 값을 Body 값을 통해서 받는다.

데이터 조회에 성공한다면 <span style="background: rgb(251,243,219)">Body 값에 저장한 데이터 값을 저장</span>하여 성공 응답을 보낸다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> DELETE
</h4>

<br>

DELETE 메서드는 지정된 리소스를 삭제한다.

<br>

**Example**

```url
DELETE /user/1
```

<br>

데이터를 삭제하는 것이기 때문에 요청시에 <span style="background: rgb(251,243,219)">Body 값과 Content-Type 값이 비워져있다.</span>

URL을 통해서 어떠한 데이터를 삭제할지 파라미터를 받는다.

데이터 삭제에 성공한다면 <span style="background: rgb(251,243,219)">Body 값 없이 성공 응답만</span> 보내게 된다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 자주하는 질문
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> POST 방식이 GET 방식보다 보안 측면에서 더 좋다?
</h4>

<br>

- GET과 비교하여 <span style="background: rgb(251,243,219)">URL에 데이터의 정보가 들어 있지 않으므로</span> 조금 더 안전하다고 볼 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> GET 방식이 POST 방식보다 속도가 빠르다?
</h4>

<br>

- GET 방식은 <span style="background: rgb(251,243,219)">캐싱을</span> 하기 때문에 여러번 요청시 저장된 데이터를 활용하므로 조금 더 빠를 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> POST vs PUT
</h4>

<br>

- POST와 PUT은 구분해서 사용해야 한다. POST는 <span style="background: rgb(251,243,219)">새로운 데이터를 계속 생성</span>하기 때문에 요청시마다 데이터를 생성하지만, PUT은 사용자가 데이터를 지정하고 수정하는 것이기 때문에 같은 요청을 하더라도 데이터가 계속 생성되지는 않는다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> POST와 PUT의 차이점 예시
</h3>

<br>

아래와 같은 URI가 있고, 해당 URI에 대해 POST와 PUT이 작동하는 예를 보자

```url
/student
```

<br>

POST 메소드로 뽀로로라는 이름을 가진 학생을 생성하기 위해 아래와 같이 요청하면 고유 구분값인 **id**를 **1**로 설정되어 뽀로로라는 학생이 생성된다.

```url
HttpRequest
POST /student
{
  “name”: “뽀로로”,
  “grade”: 1
}

-----------------------

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “뽀로로”,
  “grade”: 1
}
```

<br>

그러면 이제 **PUT**을 통해 뽀로로의 grade를 2로 변경해부자. PUT은 리소스에 대한 수정이므로 특정 리소스를 구분하는 **id**값을 넣어줘야 한다.

```url
HttpRequest
PUT /student/1
{
  “grade”: 2
}

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “뽀로로”,
  “grade”: 2
}
```

<br>

이는 POST와 PUT의 가장 기본적인 사용 예제이고, 두 메서드의 차이를 조금 더 자세히 알아보기 위한 예제를 또 보자.

POST 메서드로 뽀로로 학생을 생성해달라고 **2번** 요청하면 어떻게 될까?

```url
POST /student
{
   “name”: “뽀로로”,
   “grade”: 1
}
```

<br>

**id**가 **1과 2**인 뽀로로가 두 개가 생겨버린다.

POST는 **리소스를** **생성하기 위한** 메서드로 요청한 횟수마다 **새로운 리소스를 생성**한다.(물론 name을 unique key로 잡으면 같은 이름으로 생성 안되게 만들 순 있다.)

```url
HTTP/1.1 200 OK
{ “id”: 1, “name”: “뽀로로”, “grade”: 1 }

HTTP/1.1 200 OK
{ “id”: 2, “name”: “뽀로로”, “grade”: 1}
```

<br>

반대로 PUT으로 같은 요청을 **두 번** 보내면 어떻게 될까?

```url
PUT /student/3
{
  “name”: ”에디”
  “grade”: 2
}
```

<br>

2번 아니, 수백번 보내도 아래와 같은 응답이 온다.

**id**를 3을 가진 리소스는 없었으므로, 최소 한번은 생성되고, 그 후에는 생성되지 않는다.

```url
HTTP/1.1 200 OK
{ “id”: ”3”, “name”: “에디”, “grade”: 2 }
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 정리
</h4>

- **POST**
  - POST는 리소스의 생성을 담당한다.
  - POST는 요청 시 마다, 새로운 리소스가 생성된다.
- **PUT**
  - PUT은 리소스의 생성과 수정을 담당한다.
  - PUT은 요청 시 마다. 같은 리소스를 반환한다.
    - 물론, 리소스 안에 속성은 변경될 수 있다.

<br>

이를 어려운 말로 이야기하면, PUT은 <span style="background: rgb(251,243,219)">멱등</span>하다고 말할 수 있고 POST는 <span style="background: rgb(251,243,219)">명등</span>하지 않다고 말한다.
