---
layout: post
title: 스프링부트에서 테스트 코드를 작성하기-스프링 부트와 AWS로 혼자 구현하는 웹 서비스-2-1
date: 2021-08-13 13:00:00 0000
tags: [Intellij, SpringBoot, Book]
categories: [SpringBoot]
description: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '스프링 부트와 AWS로 혼자 구현하는 웹 서비스'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>스프링부트에서 테스트 코드를 작성하기</center>

<br>

테스트 코드를 작성해야 하는 이유는 아래와 같다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">단위 테스트는 개발단계 초기에 문제를 발견하게 도와준다.</div>
<div class="webnots-success webnots-notification-box">단위 테스트는 개발자가 나중에 코드를 리팩토링하거나 라이브러리 업그레이드 등에서 기존 기능이 올바르게 작동하는지 확인할 수 있다.</div>
<div class="webnots-success webnots-notification-box">단위 테스트는 기능에 대한 불확실성을 감소시킬 수 있다.</div>
<div class="webnots-success webnots-notification-box">단위 테스트는 시스템에 대한 실제 문서를 제공한다. 즉, 단위 테스트 자체가 문서로 사용할 수 있다. </div>

<br>

이 프로젝트로 이제 테스트 코드를 작성해 보자.

일단 main 함수를 잠깐 살펴보자.

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-38-08.png){: p}

<br>
**FreelecSpringbootBoardApplication.java**

```java
package com.yyk.app.freelecspringbootboard;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//이 어노테이션으로 인해 스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정된다.
//특히나 @SpringBootApplication이 있는 위치부터 설정을 일거아나기 때문에 이 클래스는 항상 프로젝트 최상단에 위치해야만 한다.
@SpringBootApplication
public class FreelecSpringbootBoardApplication {

    //SpringApplication.run으로 인해 내장 WAS(Web Application Sever)를 실행한다.
    public static void main(String[] args) {
        SpringApplication.run(FreelecSpringbootBoardApplication.class, args);
    }

}

```

<br>

설명은 주석을 참고한다.

그리고 패키지와 자바 파일을 하나 생성한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-43-15.png){: p}

<br>

**HelloController.java**

```java
package com.yyk.app.freelecspringbootboard.web;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

//컨트롤러를 JSON을 반환하는 컨트롤러로 만들어준다.
//예전에는 @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해준다.
@RestController
public class HelloController {
    
    //HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 준다.
    //  '/hello'로 요청이 오면 문자열 hello를 반환하는 기능을 가진다.
    @GetMapping("/hello")
    public String hello(){
        return "hello";
    }
}

```

<br>

작성한 코드가 제대로 동작하는지 테스트한다. 검증을 위해 아래 사진과 같이 패키지와 파일을 생성한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-47-27.png){: p}

<br>

**HelloControllerTest.java**

```java
package com.yyk.app.freelecspringbootboard.web;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

//테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킨다.
//여기서는 SpringRunner라는 스프링 실행자를 사용한다.
//즉 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 한다.
@RunWith(SpringRunner.class)

//여러 스프링 테스트 어노테이션 중 Web(Spring MVC)에 집중할 수 있는 어노테이션이다.
//선언할 경우 @Controller, @ControllerAdvice 등을 사용할 수 있다.
//단 @Service, @Component, @Repository 등은 사용할 수 없다.
//여기서는 컨트롤러만 사용하기 때문에 선언한다.
@WebMvcTest
public class HelloControllerTest {
    
    //스프링이 관리하는 빈(Bean)을 주입
    @Autowired
    //웹 API를 테스트할 때 사용
    //스프링 MVC 테스트의 시작점
    //이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트를 할 수 있다.
    private MockMvc mvc;

    @Test
    public void hello가_리턴된다() throws Exception{
        String hello="hello";

        //MockMvc를 통해 /hello 주소로 HTTP GET 요청을 한다.
        //체이닝이 지원해서 아래와 같이 여러 검증 기능을 이어서 선언할 수 있다.
        mvc.perform(get("/hello"))
                //mvc.perform의 결과를 검증한다.
                //HTTP Header의 Status를 검증한다
                //우리가 흔히 알고 있는 200, 404, 500 등의 상태를 검증한다.
                //여기선 OK 즉 200인지 아닌지를 검증한다.
                .andExpect(status().isOk())
                
                //mvc.perform의 결과를 검증한다.
                //응답 본문의 내용을 검증한다.
                //Controller에서 "hello"를 리턴하기 때문에 이 값이 맞는지 검증한다. 
                .andExpect(content().string(hello));
    }
}

```

<br>

코드를 모두 작성했다면 테스트 코드를 한번 실행해본다. 

<br>

테스트를 실행하고 다음과 같은 에러가 나올 수 있다.
<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-18-10-41.png){: p}

<br>

이땐 <span style="color:orange; font-weight:bold">Ctrl+Shift+a</span>를 누른다음 <span style="color:orange; font-weight:bold">settings</span>를 치고 들어가서 <span style="color:orange; font-weight:bold">Build, Execution, Deployment->Build Tools->Gradle</span> 창에서 <span style="color:orange; font-weight:bold">Run tests using</span>을 <span style="color:orange; font-weight:bold">Gradle</span>에서 <span style="color:orange; font-weight:bold">IntelliJ IDEA</span>로 바꿔준다.

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-18-11-29.png){: p}

<br>

그리고 다시 실행하면 아래와 같이 성공한다.


<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-18-13-57.png){: p}

<br>

