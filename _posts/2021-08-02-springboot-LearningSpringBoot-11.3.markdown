---
layout: post
title: 자동 회원 가입의 후처리-코드로 배우는 스프링 부트 웹 프로젝트-11.3
date: 2021-08-02 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, Google Social Login]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>자동 회원 가입의 후처리</center>

<br>

이제 자동으로 회원 가입이 되는 경우에는 다음과 같은 점들을 좀 고민해봐야 한다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">패스워드가 모두 '1111'로만 처리되는 점 - 만일 이메일을 알고 있다면 모든 패스워드는 1111로 고정되는 단점</div>
<div class="webnots-success webnots-notification-box">사용자의 이메일(email) 외에도 이름(name)을 닉네임처럼 사용할 수 없다는 점</div>

<br>

다행이도 현재 코드에는 fromSocial이라는 속성값을 이용한다.

<br>

<div class="webnots-success webnots-notification-box">폼방식의 로그인은 fromSocial 값이 false인 경우에만 로그인이 가능</div>
<div class="webnots-success webnots-notification-box">소셜의 경우에는 fromSocial 값이 true인 해당 이메일을 가진 사용자 조회</div>

<br>

위와 같은 방식을 이용해서 소셜로 가입한 이메일이 있더라도 일반적인 폼방식으로 로그인이 불가능하도록 처리한다. 아래 그림은 소셜 계정으로 로그인하는 경우에 로그인이 실패하는 화면이다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-18-17-58.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-18-18-18.png){: p}

<br>

만일 소셜 로그인을 한 사용자에 한해서 서비스에서 사용할 본인의 이름이나 패스워드를 수정하고자 한다면 로그인 이후에 폼 로그인과 달리 회원 정보를 수정할 수 있는 페이지로 이동할 필요가 있다. 

<br>

스프링 시큐리티의 로그인 관련 처리에는 **AuthenticationSuccessHandler**와 **AuthenticationFailureHandler**라는 인터페이스를 제공한다. 인터페이스의 이름에서 짐작할 수 있듯이 인증이 성공하거나 실패한 후에 처리를 지정하는 용도로 사용한다. HttpSecurity의 formLogin()이나 oauth2Login() 후에는 이러한 핸들러를 설정할 수 있다. 예제는 oauth2Login() 이후에 이를 적용한다고 가정한다. security 패키지 내에 handler라는 패키지를 추가하고 ClubLoginSuccessHandler라는 클래스를 추가한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-18-58-32.png){: p}

<br>

**ClubLoginSuccessHandler.java**
```java
package org.young.club.security.handler;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.Authentication;
import org.springframework.security.web.authentication.AuthenticationSuccessHandler;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Log4j2
public class ClubLoginSuccessHandler implements AuthenticationSuccessHandler {
    @Override
    public void onAuthenticationSuccess(HttpServletRequest request, HttpServletResponse response, Authentication authentication) throws IOException, ServletException {
        log.info("---------------------------------------");
        log.info("onAuthenticationSuccess");
    }
}

```

<br>

설정을 위해서 SecurityConfig 클래스를 아래와 같이 수정한다.

**SecurityConfig.java**

```java
(...)
@Override
    protected void configure(HttpSecurity http) throws Exception {
       //http.authorizeRequests()로 인증이 필요한 자원들을 설정할 수 있고 antMatchers()는
        // '**/*'와 같은 앤트 스타일의 패턴으로 원하는 자원을 선택할 수 있다.
        //마지막으로 permitAll()의 경우는 말 그대로 '모든 사용자에게 허락'한다는 의미이므로
        //로그인하지 않은 사용자도 익명의 사용자로 간주되어서 접근이 가능하게 된다.
        //프로젝트를 재시작해서 /sample/all에 접속하면 별도의 로그인 없이도 접근이 가능해 진다.
        http.authorizeRequests().antMatchers("/sample/all").permitAll()
                                //아래와 같이 설정하고 /sample/member'를 호출하면 Access Denied 된다.
                                .antMatchers("/sample/member").hasRole("USER");

        //인가/인증에 문제시 로그인 화면면
       http.formLogin();
       http.csrf().disable();
       
       //이것을 추가해줌으로써 구글 로그인을 하면 이전과 달리 빈 화면만 보이게 된다. 
       http.oauth2Login().successHandler(successHandler());

    }
    //ClubLoginSuccessHandler를 생성하는 메서드를 추가한다. 
    @Bean
    public ClubLoginSuccessHandler successHandler(){
        return new ClubLoginSuccessHandler();
    }
```

<br>

이제 어플리케이션을 다시 실행하고 ClubLoginSuccessHandler가 정상적으로 동작하는 것을 로그를 통해서 확인한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-19-04-31.png){: p}

<br>

이전에 로그인 후에 자동으로 **'/sample/member'** 주소로 redirect 되는 현상은 Redirect Strategy로 처리할 수 있다. 이를 활용해서 일반적인 로그인은 기존과 동일하게 이동하고 소셜 로그인은 회원 정보를 수정하는 경로로 이동하도록 구현할 수 있다. RedirectStrategy 인터페이스는 주로 구현 클래스인 DefaultRedirectStrategy라는 클래스를 사용해서 처리하는데 소셜 로그인은 대상 URL을 다르게 지정하는 용도로 사용한다. 

<br>

예를 들어 소셜 로그인으로 로그인한 사용자의 패스워드가 **'1111'**인 경우라면 회원 정보를 수정해야겠다고 판단하면 PasswordEncoder를 주입해서 패스워드를 확인하고 회원 수정 페이지로 이동시킬 수 있다.

<br>

**ClubLoginSuccessHandler.java**

```java
package org.young.club.security.handler;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.Authentication;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.DefaultRedirectStrategy;
import org.springframework.security.web.RedirectStrategy;
import org.springframework.security.web.authentication.AuthenticationSuccessHandler;
import org.young.club.security.dto.ClubAuthMemberDTO;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Log4j2
public class ClubLoginSuccessHandler implements AuthenticationSuccessHandler {
    
    //이것을 이용해서 소셜 로그인은 회원 정보를 수정하는 경로로 이동하도록 구현할 수도 있다. 
    private RedirectStrategy redirectStrategy=new DefaultRedirectStrategy();
    
    
    //Password를 바꿔주는 기능을 구현하기 위해서 인코더 객체 선언
    private PasswordEncoder passwordEncoder;
    
    public ClubLoginSuccessHandler(PasswordEncoder passwordEncoder){
        this.passwordEncoder=passwordEncoder;
    }
    @Override
    public void onAuthenticationSuccess(HttpServletRequest request, HttpServletResponse response, Authentication authentication) throws IOException, ServletException {
        log.info("---------------------------------------");
        log.info("onAuthenticationSuccess");

        
        ClubAuthMemberDTO authMember=(ClubAuthMemberDTO) authentication.getPrincipal();
        
        
        //소셜 로그인한 사용자인지 판별
        boolean fromSocial=authMember.isFromSocial();
        
        log.info("Need Modify Member?"+fromSocial);
        
        
        //패스워드가 1111과 매칭이 되는지 판별
        boolean passwordResult=passwordEncoder.matches("1111",authMember.getPassword());
        
        //소셜 로그인이고 패스워드가 1111인 경우 localhost:8080/member/modify로 리다이렉트 된다.
        if(fromSocial && passwordResult){
            redirectStrategy.sendRedirect(request,response, "/member/modify?from=social");
        }
    }
}

```

<br>
위의 코드에서 **(ClubAuthMemberDTO) authentication.getPrincipal()**는 아래 사진에서와 같이 **Principal** 정보를 반환받는 것이다. 

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-19-20-02.png){: p}

<br>

ClubLoginSuccessHandler는 PasswordEncoder가 필요하므로 SecurityConfig 클래스를 조금 수정해 준다.

**SecurityConfig.java**

```java
(...)
    @Bean
    public ClubLoginSuccessHandler successHandler(){
        return new ClubLoginSuccessHandler(passwordEncoder());
    }   
(...)

```

<br>

위의 코드가 적용된 후에는 소셜 로그인을 하는 경우에는 다음과 같은 로그가 기록된다. 

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-19-18-11.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.3/2021-08-04-19-18-44.png){: p}