---
layout: post
title: Bean Scope
date: 2022-01-02 14:20:00 0000
tags: [Bean Scope, Singleton, Prototype, Request, Session]
categories: [Interview]
description: Bean Scope에 대하여
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Bean Scope
</h2>

<br>

스프링에서는 **Bean**으로 지정된 객체는 기본적으로 싱글톤 객체로 관리하게 된다. 하지만 요구사항에 따라 싱글톤이 아닌 방법으로 빈을 구성해야 하는 경우가 있는데 이와 같은 경우를 명시적으로 구분하기 위해 스프링에서는 **scope**라는 키워드를 사용한다.

스프링 빈은 <span style="background: rgb(251,243,219)">스프링 컨테이너의 시작</span>과 함께 생서되어서 <span style="background: rgb(251,243,219)">스프링 컨테이너가 종료</span>될 때까지 유지된다고 학습했다.(**기본적으로 싱글톤 스코프이기 때문**)

**scope**란 단어의 뜻 그대로 스프링 빈이 존재할 수 있는 범위를 의미한다.

즉, <span style="background: rgb(251,243,219)">생존할 수 있는 기간</span>을 뜻한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 스프링 빈(Spring Bean)이란?
</h4>

스프링 IoC 컨테이너에 의해서 관리되고 애플리케이션의 핵심을 이루는 객체들을 스프링 빈(Bean)이라고 한다. 빈은 스프링 컨테이너에 의해서 인스턴스화 되어 조립되고 관리된다. 스프링 컨테이너가 관리해준다는 점을 제외하면 자바 객체이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Scope의 종류
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Singleton
</h4>

- Spring 프레임워크에서 기본이 되는 스코프
- 스프링 컨테이너의 시작과 종료까지 1개의 객체로 유지됨

<br>

![](/images/Interview/post16/2022-01-04-16-17-57.png?style=centerme)

<br>

1. 싱글톤 스코프의 빈을 컨테이너에 요청한다.
2. 스프링 컨테이너는 본인이 관리하는 스프링 빈을 반환한다.
3. 이후에 동일한 요청이 들어와도 같은 객체 인스턴스를 반환한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Example
</h4>

<br>

**Singleton Scope Bean Test Code**

```java
public class SingletonTest {
    @Test
    void singletonBeanFind() {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SingletonBean.class);
        SingletonBean bean1 = ac.getBean(SingletonBean.class);
        SingletonBean bean2 = ac.getBean(SingletonBean.class);
        System.out.println("bean1 = " + bean1);
        System.out.println("bean2 = " + bean2);
        assertThat(bean1).isSameAs(bean2);

        ac.close();
    }
    static class SingletonBean {
        @PostConstruct
        public void init() {
            System.out.println("SingletonBean.init");
        }
        @PreDestroy
        public void destroy() {
            System.out.println("SingletonBean.destroy");
        }
    }
}
```

<br>

![](/images/Interview/post16/2022-01-04-16-23-18.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Prototype
</h4>

- 요청이 오면 항상 새로운 인스턴스를 생성하여 반환하고 이후에 관리하지 않음
- 프로토타입을 받은 클라이언트가 객체를 관리해야 함
  - 스프링 컨테이너는 프로토타입 스프링 빈의 생성과 의존관계 주입까지만 관여하고 이후의 과정은 관여하지 않는다.
    - 즉 생성에서 의존관계 주입까지 컨테이너의 관리를 받고 이후는 해당 빈을 호출한 사용자에 의해서 종료된다.

<br>

![](/images/Interview/post16/2022-01-04-16-18-45.png?style=centerme)

<br>

![](/images/Interview/post16/2022-01-04-16-18-53.png?style=centerme)

<br>

1. 프로토타입 스코프의 빈을 컨테이너에 요청한다.
2. 스프링 컨테이너는 해당 시점에 프로토타입 빈을 생성하고, 필요한 의존관계를 주입한다.
3. 스프링 컨테이너는 생성한 프로토타입 빈을 클라이언트에 반환한다.
4. 이후에 동일한 요청이 들어올 경우, 항상 새로운 인스턴스를 생성해서 반환한다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

여기서 우리가 알 수 있는 점은 스프링 컨테이너는 프로토타입 빈을 생성하고 의존관계 주입, 초기화까지만 처리한다는 것이다. 클라이언트에게 반환 이후부터 스프링 컨테이너는 해당 스프링 빈에 대한 관리를 하지 않는다. 이후 빈의 종료까지 프로토타입을 관리할 책임은 빈을 요청한 클라이언트에게 있다. 그래서 @PreDestroy같은 종료 메서드가 호출 되지 않는다.</div>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Example
</h4>

<br>

**Prototype Scope Bean Test Code**

```java
public class PrototypeTest {
    @Test
    void prototypeBeanFind() {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class);
        PrototypeBean bean1 = ac.getBean(PrototypeBean.class);
        PrototypeBean bean2 = ac.getBean(PrototypeBean.class);
        System.out.println("bean1 = " + bean1);
        System.out.println("bean2 = " + bean2);
        assertThat(bean1).isNotSameAs(bean2);

        bean1.destroy();
        bean2.destroy();

        ac.close();
    }
    @Scope("prototype")
    static class PrototypeBean{
        @PostConstruct
        public void init() {
            System.out.println("PrototypeBean.init");
        }

        @PreDestroy
        public void destroy() {
            System.out.println("PrototypeBean.close");
        }
    }
}
```

<br>

![](/images/Interview/post16/2022-01-04-16-24-00.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Web
</h4>

- **Request:** 각각의 요청이 들어오고 나갈 때까지 유지되는 scope
- **Session:** 세션이 생성되고 종료될 때까지 유지되는 scope
- **Application:** 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 scope

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Example
</h3>

<br>

**PetOwner.java**

```java
package com.spring;

public class PetOwner {
    String userName;
    public AnimalType animal;

    public PerOwner(AnimalType animal) { this.animal = animal; }

    public String getUserName() {
        System.out.println("Person name is " + , userName);
        return userName;
    }
    public void setUserName(String userName) { this.userName = userName; }

    public void play() { animal.sound(); }
}
```

<br>

**Main.java**

```java
package com.spring;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainApp {
    public static void main(String[] args) {
        /* main함수에서 Contaier를 생성 */
        // 설정 파일은 인자로 넣고, 해당 설정 파일에 맞게 bean들을 만든다.
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/spring/beans/bean.xml");

        // getBean()을 통해 bean의 주소값을 가져온다.
        PetOwner person1 = (PerOwner) context.getBean("petOwner");
        person1.setUserName("Alice");
        person1.getUserName();

        PetOwner person2 = (PerOwner) context.getBean("petOwner");
        person2.getUserName();

        context.close();
    }
}
```

<br>

**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd">

    <bean id="dog" class="com.spring.Dog">
        <property name="myName" value="poodle"></property>
    </bean>

    <bean id="cat" class="com.spring.Cat">
        <property name="myName" value="bella"></property>
    </bean>

    <bean id="petOwner" class="com.spring.PetOwner" scope="singleton">
        <constructor-arg name="animal" ref="dog"></constructor-arg>
    </bean>
</beans>
https://gmlwjd9405.github.io/2018/11/10/spring-beans.html
```

<br>

![](/images/Interview/post16/2022-01-02-15-40-19.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 문제점
</h3>

<br>

스프링 컨테이너가 거의 모든 빈을 <span style="background: rgb(251,243,219)">싱글톤</span>으로 관리한다. 그래서 대부분 싱글톤 빈으로 프로토타입 빈을 호출하게 되는데 이때 문제가 생긴다.

<br>

**클라이언트가 요청을 하면 프로토티압을 생성하고 숫자를 증가시키는 로직을 호출한다는 상황을 가정하자.**

이때 프로토타입이라면 항상 새로운 객체를 반환해야 하기 때문에 몇 번 호출이 되던 **0 -> 1**로 카운팅이 되어야 할 것이다.

<br>

![](/images/Interview/post16/2022-01-04-17-01-06.png?style=centerme)

<br>

하지만 싱글톤 빈은 항상 같은 객체를 반환하기 때문에 위의 **SingletonBean**이 **프로토타입 빈**을 호출할 경우 우리의 기대와는 다르게 <span style="background: rgb(251,243,219)">호출되는 만큼 숫자가 누적</span>해서 증가한다.

이는 **SingletonBean**이 내부에 가지고 있는 프로토타입 빈은 이미 과거에 주입이 끝난 상태이기 때문이다.

즉, 주입 시점에 컨테이너에 요청을 하여 프로토타입이 생성이 된 것이지 사용할 때마다 새로 생성되는 것이 아니라는 것이다.

하지만 이렇게 되면 <span style="background: rgb(251,243,219)">프로토타입</span>을 사용하는 이규아 없다.(그냥 싱글톤 빈을 사용하면 되기 때문)

<br>

**문제 발생 케이스**

- <span style="color:#093145; font-weight:bold">싱글톤 스프링 빈 내부에 의존관계로 주입되는 스프링 빈이 프로토타입인 경우</span>

```java
package hello.core.scope;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Scope;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

import static org.assertj.core.api.Assertions.assertThat;

public class SingletonWithPrototypeTest1 {

    @Test
    void singletonClientUserPrototype() {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(ClientBean.class, PrototypeBean.class);

        ClientBean clientBean1 = ac.getBean(ClientBean.class);
        int count1 = clientBean1.logic();
        assertThat(count1).isEqualTo(1);

        ClientBean clientBean2 = ac.getBean(ClientBean.class);
        int count2 = clientBean2.logic();
        assertThat(count2).isEqualTo(2);



    }

    static class ClientBean{
        private final PrototypeBean prototypeBean;

        @Autowired
        public ClientBean(PrototypeBean prototypeBean) {
            this.prototypeBean = prototypeBean;
        }

        public int logic() {
            prototypeBean.addCount();
            int count = prototypeBean.getCount();
            return count;
        }

    }

    @Scope("prototype")
    static class PrototypeBean{
        private int count = 0 ;

        public void addCount() {
            count ++;
        }

        public int getCount() {
            return count;
        }

        @PostConstruct
        public void init() {
            System.out.println("PrototypeBean.init");
        }

        @PreDestroy
        public void destroy() {
            System.out.println("PrototypeBean.destroy");
        }

    }

}
```

<br>

![](/images/Interview/post16/2022-01-04-17-04-02.png?style=centerme)

<br>

- PrototypeBean은 프로토타입 스코프지만 clientBean은 싱글톤 스코프이기 때문에, 싱글톤 빈에서 프로토타입 빈을 사용한다.
- 싱글톤 빈의 스코프는 스프링 컨테이너와 같은데, 프로토타입 스코프의 스프링 빈이 새로 생성되기는 했지만 싱글톤 빈과 함께 사용되기 때문에 계속 유지된다.
- 그래서 빈을 2회 요청하지만 동일한 프로토타입 빈을 사용하게 되어 count는 1이 아닌 2가 된다.
- 프로토타입 빈만 클라이언트가 직접 사용하는 경우라면 상관 없지만 싱글톤 빈과 함께 사용하면서 프로토타입 빈이 자기의 스코프를 지키고 매번 새롭게 생성하기 위해서는 어떻게 해야 할까?

<br>

![](/images/Interview/post16/2022-01-04-17-06-12.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 Provider
</h4>

<br>

위에서 싱글톤 빈과 프로토타입 빈을 혼용하는 경우 프로토타입의 의도대로 동작하지 않는 문제점을 발견했다.

그럼 어떻게 싱글톤 빈과 혼용하더라도 프로토타입 빈을 매번 새롭게 생성하면서 사용할 수 있을까?

간단히 사용해보면 싱글톤 빈에서 프로토타입 빈을 매번 새로 호출해서 사용하는 방법이 있을 것이다.

<br>

**ClientBean 핵심 코드 수정**

```java
static class ClientBean{
		@Autowired
    private ApplicationContext ac;

    public int logic() {
				PrototypeBean prototypeBean = ac.getBean(PrototypeBean.class);
        prototypeBean.addCount();
        int count = prototypeBean.getCount();
        return count;
    }

}
```

<br>

- 매번 **프로토타입 빈(PrototypeBean)**을 새로 생성하는 것을 확인할 수 있다.
- 이렇게 의존관계를 외부에서 주입(DI) 받는 것이 아닌 직접 필요한 의존관계를 찾는 것을 **Dependency Lookup(DL) 의존관계 조회(탐색)**이라 한다.
- 하지만, 이렇게 스프링 애플리케이션 컨텍스트 전체를 주입받게 되면 **스프링 컨테이너와 종속석**이 생기고 **테스트**도 어려워진다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> ObjectFactory, ObjectProvider
</h4>

<br>

- **ObjectFactory:** 지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공해준다. 아주 단순하게 **getObject** 하나만 제공하는 FunctionalInterface이고, 별도의 라이브러리도 필요없다. 그리고 스프링에 의존한다.
- **ObjectProvider:** ObjectFactory에 편의 기능들(Optional, Stream...) 추가해서 만들어진 객체이다. 별도의 라이브러리는 필요없고 스프링에 의존한다.

<br>

**적용 코드**

```java
static class ClientBean{
    @Autowired
    private ObjectProvider<PrototypeBean> prototypeBeanProvider;

    public int logic() {
        PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
        prototypeBean.addCount();
        int count = prototypeBean.getCount();
        return count;
    }
}
```

<br>

- 위에서 실행한 **ac.getBean(PrototypeBean.class)**와 동일하게 매번 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다.
- **ObjectProvider**의 **getObject()**를 호출하면 내부에서 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다.(DL)
- 스프링에 종속적인 것은 동일하지만, 기능이 단순해서 단위 테스트 및 Mock을 이용한 Test Double을 준비하기 쉽다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> JSR-330 Provider
</h4>

<br>

이런 스프링의 의존성이 마음에 들지 않으면 <span style="background: rgb(251,243,219)">javax.inject.Provider</span> 패키지의 **JSR-330** 자바 표전을 사용하는 방법이 있다. 이 방법을 사용하기 위해서는 <span style="background: rgb(251,243,219)">javax.inject:javax.inject:1</span> 라이브러리를 추가해야 한다.

**build.gradle에 라이브러리 추가**

```gradle에
...

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter'
    implementation 'javax.inject:javax.inject:1'

		...
}
```

<br>

**테스트 코드 변경**

```java
import javax.inject.Provider;

...
static class ClientBean{
    @Autowired
    private Provider<PrototypeBean> prototypeBeanProvider;

    public int logic() {
        PrototypeBean prototypeBean = prototypeBeanProvider.get();
        prototypeBean.addCount();
        int count = prototypeBean.getCount();
        return count;
    }
}
```

<br>

- 의도한대로 매번 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다.
- **ObjetProvider**의 **getObject**대신 get 메서드를 사용해 **Dependency Lookup(DL)**한다.
- 자바 표준이고, 기능이 단순하기에 단위 테스트도 가능하고 Test Double도 쉽다.
  - 그렇기에 스프링이 아닌 다른 컨테이너에서도 사용 가능하다.
- 별도의 라이브러리가 필요하다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프로토타입 빈을 언제 사용해야 하는가?
</h3>

<br>

<span style="background: rgb(251,243,219)">javax.inject</span> 패키지에 가보면 **DL**을 언제 사용하는 지에 대한 예시가 Document로 작성되어 있다.

<br>

- 여러 인스턴스를 검색해야 하는 경우
- 인스턴스를 지연 혹은 선택적으로 찾아야 하는 경우
- 순환 종속성을 깨기 위해서
- 스코프에 포함된 인스턴스로부터 더 작은 범위의 인스턴스를 찾아 추상화 하기 위해서 사용한다.