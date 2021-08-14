---
layout: post
title: 롬복 소개 및 설치하기-스프링 부트와 AWS로 혼자 구현하는 웹 서비스-2-2
date: 2021-08-14 13:00:00 0000
tags: [Intellij, SpringBoot, Book]
categories: [SpringBoot]
description: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '스프링 부트와 AWS로 혼자 구현하는 웹 서비스'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>롬복 소개 및 설치하기</center>

<br>

롬복은 자바 개발할 때 자주 사용하는 코드 Getter, Setter, 기본생성자, toString 등을 어노테이션으로 자동 생성해 준다. 우리는 이미 프로젝트를 생성할 때 롬복 의존성을 gradle에 추가해줬다. 이는 아래 코드에서 확인할 수 있다.

<br>

**build.gradle**

```gradle
compileOnly 'org.projectlombok:lombok'
```

<br>

그리고 추가적으로 플러그인을 설치해줘야 한다. <span style="color:orange; font-weight:bold">윈도우 [Ctrl+Shift+A]</span>를 눌러서 Plugins Action을 선택하면 플러그인 설치 팝업이 나온다. Marketplace 탭으로 이동하여 "lombok"을 겁색하고 설치를 진행한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-14-16-59-33.png){: p}

<br>

난 <span style="color:#3D9970; font-weight:bold">Intellij가 Ultimate 버젼</span>이라서 그런지 이미 내장되어(bundled) 있다. 

<br>

이제 web 패키지에 dto 패키지를 추가한다. 앞으로 모든 응답 Dto는 이 Dto 패키지에 추가한다. 이 패키지에 HelloResponseDto를 생성한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-14-17-01-53.png){: p}

<br>

**HelloResponseDto.java**

```java
package com.yyk.app.freelecspringbootboard.web.dto;

import lombok.Getter;
import lombok.RequiredArgsConstructor;

//선언된 모든 필드의 get 메소드를 생성해준다.
@Getter
//선언된 모든 final 필드가 포함된 생성자를 생성해 준다.
//final이 없는 필드는 생성자에 포함되지 않는다.
@RequiredArgsConstructor
public class HelloResponseDto {
    private final String name;
    private final int amount;
}

```

<br>

이 Dto에 적용된 롬복이 잘 작동하는지 간단한 테스트 코드를 작성해 본다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-14-17-04-26.png){: p}

**HelloResponseDtoTest.java**

```java
package com.yyk.app.freelecspringbootboard.web.dto;

import org.junit.Test;

import static org.assertj.core.api.Assertions.assertThat;

public class HelloResponseDtoTest {

    @Test
    public void 롬복_기능_테스트(){
        String name="test";
        int amount=100;

        HelloResponseDto dto=new HelloResponseDto(name,amount);

        //assertThat은 assertj라는 테스트 검증 라이브러리의 검증 메소드이다.
        //검증하고 싶은 대상을 메소드 인자로 받는다
        //메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있다.
        //isEqualTo는 assertj의 동등 비교 메소드이다
        //assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공한다.
        assertThat(dto.getName()).isEqualTo(name);
        assertThat(dto.getAmount()).isEqualTo(amount);
    }
}

```

<br>

여기서 보면 Junit의 기본 assertThat이 아닌 assertj의 assertThat을 사용했다. assertj 역시 Junit에서 자동으로 라이브러리 등록을 해준다. Junit과 비교해서 assertj의 장점은 다음과 같다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">CoreMatchers와 달리 추가적으로 라이브러리가 필요하지 않다. 보통 Junit의 assertThat을 쓰면 is()와 같이 Matcher 라이브러리가 필요하다</div>
<div class="webnots-success webnots-notification-box">자동완성이 좀 더 확실하게 지원된다. IDE에서는 CoreMatchers와 같은 Matcher 라이브러리의 자동완성 기능이 약하다</div>

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-14-17-24-05.png){: p}

<br>

위의 사진과 같이 테스트가 성공한 것을 볼 수 있다. 

이제 HelloController에 새로 만든 ResponseDto를 사용하도록 추가한다.

<br>

**HelloController.java**

```java
@GetMapping("/hello/dto")
    //@RequestParam은 외부에서 API로 넘긴 파라미터를 가져오는 어노테이션이다.
    //여기서는 외부에서 name(@RequestParam("name")) 이란 이름으로 넘긴
    //파라미터를 메소드 파라미터 name(String name)에 저장하게 된다.
    public HelloResponseDto helloDto(@RequestParam("name") String name, @RequestParam("amount") int amount){
        return new HelloResponseDto(name, amount);
    }
```

<br>

name과 amount는 API를 호출하는 곳에서 넘겨준 값이다. 추가된 API를 테스트하는 코드를 **HelloControllerTest**에 추가한다.

<br>

**HelloControlleTest.java**

```java
package com.yyk.app.freelecspringbootboard.web;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.hamcrest.Matchers.is;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

//테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킨다.
//여기서는 SpringRunner라는 스프링 실행자를 사용한다.
//즉 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 한다.
@RunWith(SpringRunner.class)

//여러 스프링 테스트 어노테이션 중 Web(Spring MVC)에 집중할 수 있는 어노테이션이다.
//선언할 경우 @Controller, @ControllerAdvice 등을 사용할 수 있다.
//단 @Service, @Component, @Repository 등은 사용할 수 없다.
//여기서는 컨트롤러만 사용하기 때문에 선언한다.
@WebMvcTest(controllers=HelloController.class)
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

    @Test
    public void helloDto가_리턴된다() throws Exception{
        String name="hello";
        int amount=1000;


        mvc.perform(get("/hello/dto")
        .param("name",name)
        .param("amount", String.valueOf(amount)))
                .andExpect(status().isOk())
        //assertThat은 assertj라는 테스트 검증 라이브러리의 검증 메소드이다.
        //검증하고 싶은 대상을 메소드 인자로 받는다
        //메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있다.
        //isEqualTo는 assertj의 동등 비교 메소드이다
        //assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공한다.
                .andExpect(jsonPath("$.name", is(name)))
                .andExpect(jsonPath("$.amount",is(amount)));
        System.out.println("Json:"+jsonPath("$.name").toString());
        System.out.println("is name?:"+is(name));
    }
}

```

<br>

만약 <span style="color:#85144b; font-weight:bold">import static org.hamcrest.Matchers.is</span>가 제대로 import가 안 된다면 build.gradle에 아래 내용을 추가하고 sync한다.

**build.gradle**

```gradle
testImplementation group: 'org.hamcrest', name: 'hamcrest-core', version: '2.2'
```

<br>

아래 사진을 통해 테스트 통과한 모습을 볼 수 있다.

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-14-18-16-03.png){: p}