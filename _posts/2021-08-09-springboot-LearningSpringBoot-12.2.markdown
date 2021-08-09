---
layout: post
title: API 서버를 위한 필터-코드로 배우는 스프링 부트 웹 프로젝트-12.2
date: 2021-08-09 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, API Service]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>API 서버를 위한 필터</center>

<br>

지금까지 작성한 '/notes'라는 경로는 외부에서 데이터를 주고받기 위한 경로이다. 이 경로를 외부에서 아무런 제약없이 호출하는 것은 서버에 상당한 부담을 주기 때문에 인증을 거친 사용자에 한해서 서비스를 제공하고자 한다. 

<br>

기존 웹 애플리케이션의 쿠키(Cookie)나 세션(Session)을 사용하는 경우 동일한 사이트에서만 동작하기 때문에 API 서버처럼 외부에서 자유롭게 데이터를 주고받을 때는 유용하지 못하다. 외부에서 API를 호출할 때는 주로 '인증 정보나 인증 키(key)'를 같이 전송해서 처리한다. 

<br>

예를 들어 앞에서 소셜 로그인을 하기 위해서 구글에서 키(key)를 발급받아서 사용했듯이 API를 이용할 때 자신의 고유한 키(key)를 같이 전송하고 이를 이용해서 해당 요청이 정상적인 사용자임을 알아내는 방식을 사용한다. 이러한 키(key)를 토큰(token)이라는 용어로 사용하기도 하는데 예제에서는 JWT(JSON Web Token)라는 것을 이용한다.

<br>

외부에서는 특정한 API를 호출할 때 반드시 인증에 사용할 토큰을 같이 전송하고, 서버에서는 이를 검증한다. 이 과정에서 필요한 것은 특정한 URL을 호출할 때 전달된 토큰을 검사하는 필터이다. 스프링 시큐리티는 원하는 필터를 사용자가 작성하고 이를 설정에서 시큐리티 동작의 일부로 추가할 수 있다. 필터를 추가할 때는 기존에 있는 여러 필터 사이에 위치시킬 수 있다. 

<br>

가장 먼저 살펴볼 필터는 **org.springframework.web.filter.OncePerRequestFilter**이다. OncePerRequestFilter는 추상 클래스로 제공되는 필터로 가장 일반적이며 매번 동작하는 기본적인 필터라고 생각하면 된다. OncePerRequestFilter는 추상 클래스이므로 이를 사용하기 위해서는 상속으로 구현해서 사용한다. 프로젝트에 securiy 패키지 내에 filter 패키지를 추가하고, ApiCheckFilter라는 클래스를 추가한다. 

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-09-15-48-25.png){: p}

<br>

**ApiCheckFilter.java**

```java
package org.young.club.security.filter;

import lombok.extern.log4j.Log4j2;
import org.springframework.web.filter.OncePerRequestFilter;

import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Log4j2
public class ApiCheckFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        log.info("APICheckerFilter..................................");
        log.info("APICheckerFilter..................................");
        log.info("APICheckerFilter..................................");

        //다음 필터의 단계로 넘어가는 역할을 위해서 필요하다
        filterChain.doFilter(request, response);
    }
}

```

<br>

그 다음 SecurityConfig를 통해서 스프링의 빈으로 설정한다.

**SecurityConfig.java**

```java
(...)
    @Bean
    public ApiCheckFilter apiCheckFilter(){
        return new ApiCheckFilter();
    }
(...)
```

<br>

ApiCheckFilter의 동작 순서를 조절하고 싶다면 기존에 있는 특정한 필터의 이전이나 다음에 동작하도록 지정할 수 있다. 예를 들어 여러 필터 중에서 UsernamePasswordAuthenticationFilter는 사용자의 아디이(username)와 패스워드를 기반으로 동작하는 필터이다. 조금 전에 작성한 ApiCheckFilter를 UsernamePasswordAuthenticationFilter 이전에 동작하도록 지정하려면 다음과 같이 작성한다. 

<br>

**Securityconfig.java**

```java
(...)
@Override
    protected void configure(HttpSecurity http) throws Exception {
      (...)
        http.addFilterBefore(apiCheckFilter(), UsernamePasswordAuthenticationFilter.class);
    }
(...)
```

<br>

필터의 순서를 조정하기는 했지만 ApiCheckFilter는 오직 **'/notes/..'**로 시작하는 경우에만 동작하는게 바람직할 것이다.(기존 로그인과 달리 토큰 기반이므로). 이를 처리하는 방법으로는 AntPathMatcher라는 것을 사용한다. AntPathMatcher는 엔트 패턴(Ant Pattern은 중간에 ?,*,** 와 같은 기호를 이용해서 패턴을 표시)에 맞는지를 검사하는 유틸리티라고 생각하면 된다. ApiCheckFilter에 문자열로 된 패턴을 넣어서 패턴에 맞는 경우에는 다른 동작을 하도록 변경한다.

<br>

**ApiCheckFilter.java**

```java
(...)
@Log4j2
public class ApiCheckFilter extends OncePerRequestFilter {
    private AntPathMatcher antPathMatcher;
    private String pattern;
    
    public ApiCheckFilter(String pattern){
        this.antPathMatcher=new AntPathMatcher();
        this.pattern=pattern;
    }
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        log.info("REQUESTURI: "+request.getRequestURI());
        
        log.info(antPathMatcher.match(pattern, request.getRequestURI()));
        if(antPathMatcher.match(pattern,request.getRequestURI())){
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");
            
            return;
        }


        //다음 필터의 단계로 넘어가는 역할을 위해서 필요하다
        filterChain.doFilter(request, response);
    }
    
}
```

<br>

변경된 ApiCheckFilter 클래스는 문자열로 패턴을 입력받는 생성자가 추가되었으므로 SecurityConfig를 아래와 같이 수정한다.

<br>

**SecurityConfig.java**

```java
(...)
    @Bean
    public ApiCheckFilter apiCheckFilter(){
        return new ApiCheckFilter("/notes/**/*");
    }
(...)

<br>

위와 같이 변경된 후에 프로젝트를 실행하면 **'/notes'**로 시작하는 경로에만 로그가 출력되는 것을 볼 수 있다.

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-09-16-02-51.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-09-16-03-06.png){: p}