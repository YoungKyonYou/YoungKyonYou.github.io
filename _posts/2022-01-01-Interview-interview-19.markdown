---
layout: post
title: IoC 컨테이너와 DI(Dependency Injection)
date: 2022-01-01 11:00:00 0000
tags: [IoC Container, DI]
categories: [Interview]
description: IoC 컨테이너와 DI에 관하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> IoC 컨테이너와 DI
</h2>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> IoC(Inversion Of Control)의 이해
</h3>

<br>

<span style="color:#3D9970; font-weight:bold">IoC(제어권의 역전)이란,</span> **객체의 생성, 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀌었다는 것을 의미한다.**

<br>

> IoC(Inversion Of Control): 의존 관계 주입(DI)이라고도 하며, 어떤 객체가 사용하는 의존 객체를 직접 만들어 사용하는 것이 아닌, 주입을 받아서 사용하는 방법

<br>

스프링 프레임워크도 **객체에 대한 생성 및 생명주기를 관리**할 수 있는 기능을 제공하고 있다. 즉, IoC 컨테이너 기능을 제공한다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> IoC 컨테이너의 특징
</h3>

- IoC 컨테이너는 **객체의 생성**을 책임지고, **의존성**을 관리한다.
- **POJO**의 생성, 초기화, 서비스, 소멸에 대한 **권한**을 가진다.
- 개발자들이 직접 **POJO**를 생성할 수 있지만 **컨테이너**에게 맡긴다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IoC의 장점
</h4>

- 인터페이스 기반 설계가 가능
- 컴포넌트 재사용성 증가
- 체계적이고 효율적인 Dependency 관리

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IoC의 단점
</h4>

- 순환참조가 발생할 가능성이 있다.
- 의존성이 숨어 있다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> IoC의 분류
</h3>

- **DL**

> 저장소에 저장되어 있는 Bean에 접근하기 위해 컨테이너가 제공하는 API를 이용하여 Bean을 Lookup하는 것

<br>

아래와 같이 Bean에 대한 정보가 있는 xml 파일이 있다고 해보자.

```xml
<beans>
    <bean id="myObject" class="com.example.MyObject"/>
</beans>
```

<br>

java에서는 해당 xml의 Bean 정보들을 보고 어떤 클래스를 사용할지 검색하여 주입하게 된다.

아래 자바코드를 보자면

<br>

```java
String myConfigLocation = "classpath:myApplicationCTX.xml";
AbstractApplicationContext ctx = new GenericXmlApplicationContext(myConfigLocation);
MyObject myObject = ctx.getBean("myObject", MyObject.class);
```

<br>

그 결과 위와 같은 코드를 통해 적절한 <span style="background: rgb(251,243,219)">MyObject</span>클래스를 가져올 수 있다.

<br>

**DL 장점**

- JNDI등을 이용하는데 Object간에 Decoupling을 해준다.

<br>

**DL 단점**

- Dependency Lookup으로 획득한 객체는 컨테이너 밖에서 실행할 수 없음
- Bean 변경 시 객체 내에 변경에 대한 부분을 반영해야 하므로 일일이 수정해야 한다 따라서 테스가 어렵다
- 캐스팅이 어렵다. Strong Typed가 아니기 때문에 매번 Casting 해야 한다.

<br>

**DI**

> 각 클래스간의 의존관계를 빈 설정(Bean Definition) 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것<br><br> - Setter Injection<br> - Constructor Injection<br> - Method Injection

<br>

**DI 장점**

- Object가 Container에 의존적이지 않아서 Lookup의 관한 코드가 사라진다.
- 클래스 상속의 필요가 사라지게 된다.
- 코드가 단순해진다.
- 컴포넌트 간 결합도가 낮아진다
- 결합도를 낮추면서 유연성과 확장성 향상

<br>

**DI 단점**

- Spring 내부에 등록된 Bean 끼리만 의존성 설정이 가능하다.

<br>

DL 사용시 <span style="background: rgb(251,243,219)">컨테이너와의 종속이 증가</span>하며, 주로 DI를 사용한다.

<br>

![](/images/Interview/post16/2022-01-01-15-05-30.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> DI의 이해
</h3>

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> DI의 개념
</h3>

각 클래스간의 <span style="background: rgb(251,243,219)">의존관계</span>를 <span style="background: rgb(251,243,219)">빈 설정</span> (Bean Definition) 정보를 바탕으로 <span style="background: rgb(251,243,219)">컨테이너가 자동으로 연결</span>해주는 것을 말한다.

개발자들은 단지 <span style="background: rgb(251,243,219)">빈 설정 파일</span>에서 <span style="background: rgb(251,243,219)">의존관계</span>가 필요하다는 정보를 추가하면 된다.

객체 레퍼런스를 <span style="background: rgb(251,243,219)">컨테이너</span>로부터 주입 받아서 실행 시에 <span style="background: rgb(251,243,219)">동적으로 의존관계</span>가 생성된다.

컨테이너가 흐름의 주체가 되어 <span style="background: rgb(251,243,219)">애플리케이션 코드</span>에 <span style="background: rgb(251,243,219)">의존관계를 주입</span>해 주는 것이다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> DI의 장점
</h3>

- 코드가 단순해진다.
- 컴포넌트 간의 결합도가 낮아진다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> DI의 유형
</h3>

<br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">Setter Injection (Setter 메서드를 이용한 의존성 삽입)</span>: 의존성을 입력 받는 setter 메서드를 만들고 이를 통해 의존성을 주입한다.

- <span style="color: rgba(131, 24, 67); font-weight:bold">Constructor Injection (생성자를 이용한 의존성 삽입)</span>: 필요한 의존성을 포함하는 클래스의 생성자를 만들고 이를 통해 의존성을 주입한다.

- <span style="color: rgba(131, 24, 67); font-weight:bold">Method Injection (일반 메서드를 이용한 의존성 삽입)</span>: 의존성을 입력 받는 일반 메서드를 만들고 이를 통해 의존성을 주입한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Spring DI 컨테이너에 대한 이해
</h3>

<br>

Spring 애플리케이션에서 <span style="background: rgb(251,243,219)">컴포넌트들의 중앙 저장소</span>, <span style="background: rgb(251,243,219)">Bean 설정 소스</span>로부터 Bean 정의를 읽어들이고 <span style="background: rgb(251,243,219)">Bean을 구성</span> 하고 <span style="background: rgb(251,243,219)">제공</span>해주는 <span style="background: rgb(251,243,219)">컨테이너</span>이다. 또한 실제 <span style="background: rgb(251,243,219)">IoC 컨테이너</span>는 <span style="background: rgb(251,243,219)">ApplicationContext 인터페이스</span>를 구현한 <span style="background: rgb(251,243,219)">클래스의 오브젝트</span>이다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> Spring DI 컨테이너의 개념
</h3>

<br>

Spring DI 컨테이너가 관리하는 객체를 **빈(bean)** 이라고 하고, 이 빈(bean)들을 관리한다는 의미로 컨테이너를 **빈 팩토리(Bean Factory)**라고 부른다.

- 객체의 생성과 객체 사이의 런타임(run-time) 관계를 DI관점에서 볼 때는 컨테이너를 BeanFactory라고 한다.
- BeanFactory에 여러 가지 컨테이너 기능을 추가하여 **애플리케이션 컨텍스(Application Contect)**라고 부른다.

<br>

<h3 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="23" width="23"> BeanFactory와 ApplicationContext
</h3>

<br>

- **BeanFactory**
  - Bean을 등록, 생성, 조회, 반환 관리함.
  - 보통은 BeanFactory를 바로 사용하지 않고, 이를 확장한 ApplicationContext를 사용한다.
  - getBean() 메서드가 정의되어 있다.

<br>

- **ApplicationContext**

  - Bean을 등록, 생성, 조회, 반환 관리하는 기능은 BeanFactory와 같다
  - Spring의 각종 부가 서비스를 추가로 제공한다.
  - Spring이 제공하는 ApplicationContext 구현 클래스가 여러 가지 종류가 있다.

  <br>

  ![](/images/Interview/post16/2022-01-01-15-14-23.png?style=centerme)
