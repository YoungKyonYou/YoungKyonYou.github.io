---
layout: post
title: Spring vs SpringBoot
date: 2022-01-01 12:00:00 0000
tags: [Spring, SpringBoot]
categories: [Interview]
description: Spring과 SpringBoot의 차이
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Spring vs SpringBoot
</h2>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Spring의 특징
</h3>

<br>

- 제어의 역전(IoC)
- 의존선 주입(DI)
- 관점 지향 프로그래밍(AOP)

<br>

Spring의 3가지 특징은 위에 명시된 것과 같다. 이런 특징으로 인해 <span style="background: rgb(251,243,219)">결합도를 낮춰(Loose Coupling)</span> 유연한 개발이 가능해졌다.

간단하게 살펴보도록 하자 (**[자세한 내용 - 링크](https://youngkyonyou.github.io/interview/2022/01/01/Interview-interview-19.html)** )

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 제어의 역전(IoC)
</h4>

<br>

제어의 역전 패턴이 인기를 끄는 이유는 <span style="background: rgb(251,243,219)">생명주기에 대한 제어권이 웹 애플리케이션 컨테이너에 있기 때문이다.</span>

즉, 사용자가 직접 new 연산자를 통해 인스턴스를 생성하고 메서드를 호출하는 일련의 생명주기에 대한 작업들을 스프링에 <span style="background: rgb(251,243,219)">위임</span>할 수 있게 되는 것이다.

IoC는 직관적이지 못하기 때문에 IoC를 구현하는 방법으로는 **의존성 주입(DI)**가 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 의존성 주입(DI: Dependency Injection)
</h4>

<br>

객체 사이에 필요한 의존 관계에 대해서 스프링 컨테이너가 자동으로 연결해 주는 것을 말한다.

스프링 컨테이너는 DI를 이용하여 빈(Bean) 객체를 관리하며 스프링 컨테이너에 클래스를 등록하면 스프링이 클래스의 인스턴스를 관리해 준다.

**스프링 컨테이너에 빈(Bean)을 등록하고 설정하는 방법은 크게 두 가지가 있다.**

**(1)** XML 설정을 통한 DI
**(2)** 어노테이션(Annotations)을 이용한 DI

<br>

첫 번째로 XML 설정을 통한 DI에 대해서 알아보자

<br>

**applicationContext.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
	xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd">
	<bean id="UserAddController" class="com.lotts.web.user.UserAddController">
		<property name="userImpl" ref="userImpl"/>
	</bean>
	<bean id="userImpl" class="com.lotts.domain.logic.UserImpl">
		<property name="userDao" ref="userDao"/>
		<property name="orgDao" ref="orgDao"/>
		<property name="uploadpath" value="${file.upload.path}" />
	</bean>
	<bean id="userDao" class="com.lotts.dao.ibatis.SqlMapUserDao">
		<property name="sqlMapClient" ref="sqlMapClient"/>
	</bean>
	<bean id="OrgDao" class="com.lotts.dao.ibatis.SqlMapOrgDao">
		<property name="sqlMapClient" ref="sqlMapClient"/>
	</bean>
	<bean id="sqlMapClient" class="org.springframework.orm.ibatis.SqlMapClientFactoryBean">
		<property name="configLocation" value="WEB-INF/config/SqlMap.xml"/>
		<property name="dataSource" ref="dataSource"/>
	</bean>
```

<br>

**SpringTest.java**

```java
public class SpringTest {
    public static void main(String ar[]) {
        ApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        UserFacade userImpl = (UserImpl) ctx.getBean("userImpl");
        userImpl.사용자_정보를_조회한다();
        userImpl.사용자를_등록한다();
    }
}
```

<br>

이제 어노테이션을 이용한 DI에 대해 알아보자.

<br>

@Component를 사용하여 해당 클래스를 찾아 @Autowired가 붙은 클래스를 자동적으로 객체로 만들어주고 사용할 수 있게 해준다.

또한, XML에 설정에 auto scan을 설정하면 해당 패키지 범위에 Component를 설정하여 사용할 수 있다.

<br>

```xml
<context:component-scan base-package="com.lotts.web" />
```

<br>

@Component의 확장된 어노테이션을 사용하면 스프링은 패키지 및 하위 패키지 내에서 해당 어노테이션을 찾아서 인젝션을 한다.

<br>

- **@Repository**: 데이터베이스에서 정보를 검새하는 DAO(Data Access Objects)에 사용된다.
- **@Service**: 서비스 계층 클래스에 사용되며 데이터 및 비즈니스 로직 처리에 사용된다.
- **@Controller**: UI에서 요청 처리에 사용된다.

<br>

**Example**

```java
@Controller
public class InfoController extends MultiActionController {
    @Autowired private InfoServiceImpl InfoService;
}

@Service("InfoService")
public class InfoServiceImpl implements InfoService {
    @Autowired private InfoDaoImpl InfoDao;
}

@Repository("InfoDao")
 public class InfoDaoImpl implements InfoDao {
    @Autowired private SqlSessionTemplate sst;
}
```

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Spring과 SpringBoot의 차이점
</h3>

<br>

앞에서 설명한 것처럼 스프링은 IOC나 DI를 통해 의존성을 주입할 수 있기 때문에 다양한 스프링 모듈을 사용할 수 있다.

<br>

![](/images/Interview/post16/2022-01-01-17-37-40.png?style=centerme)

<br>

Spring MVC 프레임워크를 사용할 때 위에 applicationContext.xml이외에 다양한 설정을 통해 의존성을 주입한다.

Spring MVC는 DispatcherServlet, View Resolver, Interceptor, Handler, View 등으로 구성되어 있으며 아래의 설정은 실무에서 약간씩 가져온 대략적인 설정이다.

<br>

기존의 Spring과의 차이점을 대략 정리해 보자면 아래와 같다.

<br>

**(1)** <span style="background: rgb(251,243,219)">내장 톰캣</span>

내장 톰캣을 사용하기 때문에 따로 톰캣을 설치하거나 매번 버전을 관리해 주지 않아도 된다.

<br>

**(2)** <span style="background: rgb(251,243,219)">starter를 통한 dependency를 자동화</span>

기존의 Spring에서는 dependency들의 호환되는 버전을 일일히 맞추어 주어야 했고 이 때문에 하나의 dependency 버전을 바꾸게 되는 경우 나머지의 버전 또한 직접 설정해주어야 했다

<br>

```gradle
/* gradle */ implementation 'org.springframework.boot:spring-boot-starter-aop:2.2.0.RELEASE'
```

<br>

위와 같이 작성해주면 스프링 부트에서는 이 starter를 통해 종속된 모든 라이브러리를 알맞게 찾아서 함께 가져오기 때문에 의존성이나 호환버전에 대해 신경 쓸 필요가 없다.

<br>

**(3)** <span style="background: rgb(251,243,219)">XML</span>

View Resolver, 데이터 액세스 등의 xml 설정을 하지 않아도 된다.

<br>

**(4)** <span style="background: rgb(251,243,219)">jar</span>

jar file을 이용해 자바 옵션만으로 손쉽게 배포가 가능하다

<br>

**(5)** <span style="background: rgb(251,243,219)">AutoConfigurator</span>

공통적으로 필요한 설정을 어노테이션을 이용하여 대신할 수 있다.

예를 들어 스프링부트의 main 메서드는 @SpringBootApplication이라는 어노테이션을 가지고 있는데 이것은 @ComponentScan+@Configuration+@EnableAutoConfiguration 등의 어노테이션을 합쳐놓았다.

<br>

**(6)** <span style="background: rgb(251,243,219)">Spring Initializr</span>

https://starter.spring.io/ 에서 스프링이 공식적으로 제공하는 Spring Initilizr를 사용하면 실행 환경이나 의존성 관리 등의 인프라 부분을 신경 쓸 필요 없이 바로 코딩을 시작할 수 있게끔 환경을 제공해 준다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

![](/images/Interview/post16/2022-01-01-17-44-13.png?style=centerme)
