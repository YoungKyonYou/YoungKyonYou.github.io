---
layout: post
title: API를 위한 인증처리-코드로 배우는 스프링 부트 웹 프로젝트-12.3
date: 2021-08-11 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, API Service]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>API를 위한 인증처리</center>

<br>

API를 이용한다면 일반적인 로그인의 URL이 아닌 별도의 URL로 로그인을 처리하는 것이 일반적이다. 폼 방식의 로그인과 달리 API는 URL이 변경되면 API를 이용하는 입장에서는 호출하는 URL를 변경해야 하기 때문에 위험한 일이다.

예제는 ApiLoginFilter를 작성한다. ApiLoginFilter는 특정한 URL로 외부에서 로그인이 가능하도록 하고, 로그인이 성공하면 클라이언트가 Authorization 헤더의 값으로 이용할 데이터를 전송할 것이다. 예제에서는 **'/api/login'**이라는 URL을 이용해서 외부의 클라이언트가 자신의 아이디와 패스워드로 로그인한다고 가정한다.(API를 사용하기 위해서 별도의 메뉴로 승인을 받는 것이 일반적이지만 예제에서는 좀 더 극단적으로 일반 로그인과 동일한 계정으로 로그인하면 일정 기간 동안 API를 호출할 수 있도록 구성한다)

<br>

작성하려는 코드는 ApiLoginFilter라는 이름으로 생성한다. 다만 이전의 ApiCheckFilter와 달리 org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter라는 스프링 시큐리티에서 제공하는 필터를 이용한다. security 패키지 밑에 filter 패키지를 찾아 ApiLoginFilter 클래스를 추가한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-16-47-33.png){: p}

<br>

**ApiLoginFilter.java**

```java
package org.young.club.security.filter;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.authentication.BadCredentialsException;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.AuthenticationException;
import org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Log4j2
public class ApiLoginFilter extends AbstractAuthenticationProcessingFilter {
    public ApiLoginFilter(String defaultFilterProcessesUrl){
        super(defaultFilterProcessesUrl);
    }
    @Override
    public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException, IOException, ServletException {
        log.info("-----------------------ApiLoginFilter----------------------");
        log.info("attemptAuthentication");

        String email=request.getParameter("email");
        String pw="1111";

        if(email==null){
            throw new BadCredentialsException("email cannot be null");
        }

        return null;
    }
}

```

<br>

attemptAuthentication()에서는 간단히 email이라는 파라미터가 있어야만 동작이 가능하다. 우선은 간단히 동작 여부를 확인하기 위한 용도이므로 메서드 내부의 내용은 앞으로 많이 수정될 것이다. SecurityConfig에 ApiLoginFilter를 추가한다. AbstractAuthenticationProcessingFilter는 반드시 AuthenticationManager가 필요하므로 AuthenticationManager()를 이용해서 추가해 주어야 한다.

<br>

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
       // http.authorizeRequests().antMatchers("/sample/all").permitAll()
                                //아래와 같이 설정하고 /sample/member'를 호출하면 Access Denied 된다.
      //                          .antMatchers("/sample/member").hasRole("USER");

        //인가/인증에 문제시 로그인 화면면
       http.formLogin();
       http.csrf().disable();

       http.logout();


       //이것을 추가해줌으로써 구글 로그인을 하면 이전과 달리 빈 화면만 보이게 된다.
       http.oauth2Login().successHandler(successHandler());

       //remember me 설정하는 것이다
        //rememberMe()를 적용할 때는 주로 쿠키를 얼마나 유지할 것인지를 같이 지정한다. 초(second) 단위로 설정하므로 이 코드는 7일간 쿠키가 유지되도록 지정하였다.
       http.rememberMe().tokenValiditySeconds(60*60*7).userDetailsService(userDetailsService());

       //실제 로그인 시에 OAuth를 사용한 로그인이 가능하도록 함
      // http.oauth2Login();

        http.addFilterBefore(apiCheckFilter(), UsernamePasswordAuthenticationFilter.class);
        http.addFilterBefore(apiLoginFilter(), UsernamePasswordAuthenticationFilter.class);
    }

    @Bean
    public ApiLoginFilter apiLoginFilter() throws Exception{
        ApiLoginFilter apiLoginFilter=new ApiLoginFilter("/api/login");
        apiLoginFilter.setAuthenticationManager(authenticationManager());

        return apiLoginFilter;
    }
(...)
```

<br>

추가한 apiLoginFilter()는 '/api/login' 이라는 경로로 접근할 때 동작하도록 지정하고, UsernamePasswordAuthenticationFilter 전에 동작하도록 지정하였다. 프로젝트를 실행하고 '/api/login'을 email 파라미터 없이 전송하면 아래 사진과 같이 401 에러가 발생하는 것을 볼 수 있다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<br>

<div class="webnots-information webnots-notification-box">현재 url를 보면 포트가 8085로 되어 있는데 이는 내가 일부로 application.properties에 <span style="color:#85144b; font-weight:bold">server.port=8085</span>를 추가한 것이다. 스프링부트 앱을 실행하는데 8080포트에 오류가 나서 임시적으로 변경했다.</div>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-11-06.png){: p}

<br>

위 사진은 이메일이 없어서 발생하는 에러이다.

<br>

특정한 API르르 호출하는 클라이언트에서는 다른 서버나 Application으로 실행되기 때문에 쿠키나 세션을 활용할 수 없다. 이러한 제약 때문에 API를 호출하는 경우에는 Request를 전송할 때 Http 헤더 메시지에 특별한 값을 지정해서 전송한다.

<br>

Authorization 헤더는 이러한 용도로 사용한다. 클라이언트에서 전송한 Reqeust에 포함된 Authorization 헤더의 값을 파악해서 사용자가 정상적인 요청인지를 알아내는 것이다. ApiCheckFilter에서 Authorization 헤더를 추출하고 헤더의 값이 '12345678'인 경우에는 인증을 한다고 가정해 보자. 만일 헤더의 값이 정확하다면 다음 단계를 진행하고 그렇지 못하다면 다른 메시지를 전송해야 한다. 기존의 checkAuthHeader() 메서드를 추가해서 이러한 기능을 구현하면 아래와 같다.

<br>

**ApiCheckFilter.java**

```java
(...)
@Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        log.info("REQUESTURI: "+request.getRequestURI());

        log.info(antPathMatcher.match(pattern, request.getRequestURI()));
        if(antPathMatcher.match(pattern,request.getRequestURI())) {
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");


            //checkAuthHeader()에서 헤더의 값을 인증한다.
            boolean checkHeader=checkAuthHeader(request);

            if(checkHeader){
                filterChain.doFilter(request,response);
                return;
            }

            return;
        }


        //다음 필터의 단계로 넘어가는 역할을 위해서 필요하다
        filterChain.doFilter(request, response);
    }
    private boolean checkAuthHeader(HttpServletRequest request){
        boolean checkResult=false;


        //헤더의 값을 인증하기 위해서 Authorzation 헤더를 추출한다.
        String authHeader=request.getHeader("Authorization");

        //authHeader 문자열 변수가 문자열을 포함하는지 체크한다.
        if(StringUtils.hasText(authHeader)){
            log.info("Authorization exist: "+authHeader);
            if(authHeader.equals("12345678")){
                //"12345678"을 담고 있으면 true를 담는다.
                checkResult=true;
            }
        }
        return checkResult;
    }
(...)
```

<br>

checkAuthHeader()는 'Authorization'이라는 헤더의 값을 확인하고 boolean 타입의 결과를 반환한다. 이를 이용해서 doFilterInternal()에서 다음 필터로 진행할 것인지를 결정한다. 테스트 도구로 '/notes/2'와 같이 기존에 테스트했던 URL을 확인한다.

Request를 전송하기 전에 'Add New Header'를 선택해서 'Authorization' 헤더 값을 조정한다.

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-35-25.png){: p}

<br>

이제 Send 버튼을 눌러서 결과를 확인한다.

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-35-11.png){: p}

<br>

위의 코드는 Authorization 헤더의 값이 정상일 때도 동작하지만 불행히도 Authorization 헤더가 없는 경우에는 정상이라는 메시지가 전송된다. 테스트 도구에서 Authorization 헤더를 삭제하고 테스트를 진행한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-36-47.png){: p}

<br>

실행 결과를 보면 아래와 같이 결과 데이터는 없어도 '200' 메시지가 발행된다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-41-17.png){: p}

<br>

위에 사진으로 잘 안 보일 수도 있으니 확대해서 보여주겠다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-17-41-40.png){: p}

<br>

이것은 ApiCheckFilter가 스프링 시큐리티가 사용하는 쿠키나 세션을 이용하지 않기 때문에 발생하는 문제이다. 이를 해결하기 위해서는 정상적인 인증을 처리하도록 AuthenticationManager를 이용하는 방식을 사용하거나 ApiCheckFilter에서 간단하게 JSON 포맷의 에러 메시지를 전송하는 방법을 사용할 수 있다. 예제에서는 간단히 JSON 데이터를 전송한다.

<br>

**ApiCheckFilter.java**

```java
(...)
@Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        log.info("REQUESTURI: "+request.getRequestURI());

        log.info(antPathMatcher.match(pattern, request.getRequestURI()));
        if(antPathMatcher.match(pattern,request.getRequestURI())) {
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");
            log.info("APICheckerFilter..................................");


            //checkAuthHeader()에서 헤더의 값을 인증한다.
            boolean checkHeader=checkAuthHeader(request);

            if(checkHeader){
                filterChain.doFilter(request,response);
                return;
            }else{
                //
                //403에러를 띄운다.
                response.setStatus(HttpServletResponse.SC_FORBIDDEN);
                //json 리턴 및 한글깨짐 수정.
                response.setContentType("application/json;charset=utf-8");
                JSONObject json=new JSONObject();
                String message="FAIL CHECK API TOKEN";
                json.put("code","403");
                json.put("message",message);

                PrintWriter out=response.getWriter();
                out.print(json);
                return;
            }
        }


        //다음 필터의 단계로 넘어가는 역할을 위해서 필요하다
        filterChain.doFilter(request, response);
    }
(...)
```

<br>

변경된 내용은 checkHeader()가 false를 반환하는 경우에 net.minidev.json.JSONObject.JSONObject를 이용해서 간단한 JSON 데이터와 403 에러 메시지를 만들어서 전송한다. 위의 코드를 반영하면 Authorization 헤더가 없거나 다른 값을 전송하는 경우 아래와 같은 결과가 생기는 것을 확인할 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-05-51.png){: p}

<br>

Authorization 헤더에 따라서 다르게 동작하는 코드가 완성되었다면 다음과 같은 작업을 처리해야 한다.

<br>

<div class="webnots-success webnots-notification-box">외부에서 인증할 수 있는 인증처리</div>
<div class="webnots-success webnots-notification-box">ApiCheckFilter가 Authorization 헤더의 값을 발행하기</div>

<br>

ApiLoginFilter가 정상적으로 동작하기 위해서는 내부적으로 AuthticationManager를 사용해서 동작하도록 수정해야 한다. AuthenticationManager는 authenticate() 메서드를 가지고 있는데 특이하게도 파라미터와 리턴 타입이 동일하게 Authentication 타입이다.

<br>

파라미터로 전송하는 Authentication 타입의 객체로는 'xxxToken'이라는 것을 사용한다. 예를 들어 UsernamePasswordAuthenticationFilter 클래스는 org.springframework.security.authentication.UsernamePasswordAuthenticationToken이라는 객체를 사용한다. 직접 Authentication 타입의 객체를 만들어서 파라미터로 전달할 수도 있지만 예제에서는 최대한 간단히 사용할 수 있는 UsernamePasswordAuthenticationToken을 사용해서 인증을 진행한다.

<br>

**ApiLoginFilter.java**

```java
(...)
@Override
    public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException, IOException, ServletException {
        log.info("-----------------------ApiLoginFilter----------------------");
        log.info("attemptAuthentication");

        String email=request.getParameter("email");
        String pw="1111";

        UsernamePasswordAuthenticationToken authToken=new UsernamePasswordAuthenticationToken(email,pw);

        if(email==null){
            throw new BadCredentialsException("email cannot be null");
        }

        return null;
    }
(...)
```

<br>

변경된 내용은 email, pw를 파라미터로 받아서 실제 인증을 처리하는 것이다. 브라우저를 이용해서 '/api/login?email=xxx&pw=xxx'와 같이 실제 사용자 계정으로 로그인을 시도해 보면 '/'로 이동하기는 하지만 정상적으로 로그인된 것을 확인할 수 있다.

<br>

로그인 후에 화면에는 '/'로 이동했지만 '/sample/member' 등의 URL을 호출하면 정상적으로 로그인된 것을 확인할 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-17-49.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-18-04.png){: p}

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

당연한 이야기지만 실제 위와 같이 로그인을 처리하는 것은 POST 방식으로 하고, 가능하면 전달되는 파라미터들 역시 암호화를 해 주어야 한다. 예제에서는 빨리 결과를 확인할 수 있게 GET 방식과 평문으로 데이터를 처리하였다.</div>

<br>

ApiLoginFilter로 직접 인증처리를 했다면 남은 작업은 인증 후 성공 혹은 실패에 따른 처리이다. 이러한 처리는 메서드를 override해서 처리하거나 별도의 클래스를 지정할 수 있으므로 예제에서는 2가지 모두를 소개하려 한다.

<br>

ApiLoginFilter에서 인증에 실패하는 경우 API 서버는 일반 화면이 아니라 JSON 결과가 전송되도록 수정해야 하고 성공하는 경우에는 클라이언트가 보관할 인증 토큰이 전송되어야 한다. AbstractAuthenticationProcessingFilter에는 setAuthenticationFailureHandler()를 이용해서 인증에 실패했을 경우 처리를 지정할 수 있다. security 패키지의 handler 패키지 내 ApiLoginFailHandler 클래스를 추가한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-23-56.png){: p}

<br>

**ApiLoginFailHandler.java**

```java
package org.young.club.security.handler;

import lombok.extern.log4j.Log4j2;
import net.minidev.json.JSONObject;
import org.springframework.security.core.AuthenticationException;
import org.springframework.security.web.authentication.AuthenticationFailureHandler;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@Log4j2
public class ApiLoginFailHandler implements AuthenticationFailureHandler {

    @Override
    public void onAuthenticationFailure(HttpServletRequest request, HttpServletResponse response, AuthenticationException exception) throws IOException, ServletException {
        log.info("login fail handler.............");
        log.info(exception.getMessage());

        response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
        //json리턴
        response.setContentType("application/json;charset=utf-8");
        JSONObject json=new JSONObject();
        String message=exception.getMessage();
        json.put("code","401");
        json.put("message",message);

        PrintWriter out=response.getWriter();
        out.print(json);
    }
}

```

<br>

ApiLoginFailHandler는 AuthenticationFailureHandler 인터페이스를 구현하는 클래스로 오직 인증에 실패하는 경우에 처리를 전담하도록 구성한다. 인증에 실패하면 '401' 상태 코드를 반환하도록 한다. SecurityConfig 클래스에는 ApiLoginFilter의 setAuthenticationFailureHandler()를 적용해 주어야 한다.

<br>

**SecurityConfig.java**

```java
(...)
    @Bean
    public ApiLoginFilter apiLoginFilter() throws Exception{
        ApiLoginFilter apiLoginFilter=new ApiLoginFilter("/api/login");
        apiLoginFilter.setAuthenticationManager(authenticationManager());

        apiLoginFilter.setAuthenticationFailureHandler(new ApiLoginFailHandler());
        return apiLoginFilter;
    }
(...)
```

<br>

프로젝트를 재시작하고 인증이 불가능한 정보를 전송하면 '401' 상태 코드와 함께 에러 메시지가 전송된다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-28-18.png){: p}

<br>

인증의 실패와 마찬가지로 인증의 성공 또한 별도의 클래스로 작성해서 처리할 수 있긴 하지만 AbstractAuthenticationProcessingFilter 클래스에는 successfulAuthentication()라는 메서드를 override 해서 구현이 가능하다.

<br>

**ApiLoginFilter.java**

```java
(...)
@Override
    protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authResult) throws IOException, ServletException {
        log.info("---------------------ApiLoginFilter--------------");
        log.info("successfulAuthentication: "+authResult);

        log.info(authResult.getPrincipal());
    }
(...)
```

<br>

successfulAuthentication()의 마지막 파라미터는 성공한 사용자의 인증 정보를 가지고 있는 Authentication 객체이다. 이를 통해서 인증에 성공한 사용자의 정보를 로그에서 확인할 수 있다. 브라우저에서 '/api/login?email=user90@zerock.org@pw=1111'과 같이 정상적인 계정 정보를 이용하면 아래와 같은 로그가 기록되는 것을 볼 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-11-18-32-25.png){: p}

<br>

인증에 성공한 후에는 사용자가 '/notes/xx'와 같은 api를 호출할 때 사용할 적절한 데이터를 만들어서 전송해 주어야 한다. 여기서 JWT(JSON Web Token)를 이용할 것이다. 이늦ㅇ이 성공한 사용자에게는 특수한 문자열(JWT)을 전송해 주고, API를 호출할 때는 이 문자열을 읽어서 해당 Request가 정상적인 요청인지를 확인하는 용도로 사용할 것이다.

JWT를 사용하기 위해 라이브러리를 사용한다.

<br>

**build.gradle**

```gradle
implementation group: 'io.jsonwebtoken', name: 'jjwt', version: '0.9.1'
```

<br>

JWT를 현재 프로젝트에서는 1) 인증에 성공했을 때 JWT 문자열을 만들어서 클라이언트에게 전송하는 것과, 2) 클라이언트가 보낸 토큰의 값을 검증하는 경우에 사용된다. 예제 프로젝트 내에는 security 패키지 내에 util이라는 패키지를 구성하고 JWTUtil이라는 클래스를 추가한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-12-17-35-18.png){: p}

<br>

**JWTUitl.java**

```java
package org.young.club.security.util;

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.impl.DefaultClaims;
import io.jsonwebtoken.impl.DefaultJws;
import lombok.extern.log4j.Log4j2;

import java.nio.charset.StandardCharsets;
import java.time.ZonedDateTime;
import java.util.Date;

@Log4j2
public class JWTUtil {
    //이 키를 이용해서 Signature를 생성한다. 
    private String secretKey="zerock12345678";

    //1month
    //JWT 문자열 자체를 알면 누구든 API를 사용할 수 있다는 문제가 생기므로 만료 기간(expire) 값을 설정한다
    private long expire=60*24*30;

    //JWT 토큰을 생성하는 역할을 한다. 
    public String generateToken(String content) throws Exception{
        return Jwts.builder()
                //언제 발행되는지 세팅한다. 이것을 실행하는 현재 시간과 날짜로 설정함
                .setIssuedAt(new Date())
                
                //위에 설정한 유효기간을 설정한다.
                .setExpiration(Date.from(ZonedDateTime.now().plusMinutes(expire).toInstant()))
                //사용자의 이메일 주소를 입력해 주어서 나중에 사용할 수 있도록 구성한다. 
                .claim("sub", content)
                //getBytes는 secretKey 문자열을 바이트로 인코딩한다.
                .signWith(SignatureAlgorithm.ES256, secretKey.getBytes("UTF-8"))
                //JWT를 빌드하고 시리얼라이즈 한다.
                .compact();
    }

    //인코딩된 문자열에서 원하는 값을 추출하는 용도이다. 
    //여기서는 JWT 문자열을 검증하는 역할을 한다. JWT가 만료기간이 지난 것이라면 이 과정에서 Exception이 발생한다. 
    public String validateAndExtract(String tokenStr) throws Exception{
        String contentValue=null;
        try{
            //parseClaimsJws는 시리얼라이즈된 특정 JWS 문자열을 파싱해서 JWS 객체를 반환한다
            DefaultJws defaultJws=(DefaultJws)Jwts.parser().setSigningKey(secretKey.getBytes("UTF-8")).parseClaimsJws(tokenStr);

            log.info(defaultJws);

            log.info(defaultJws.getBody().getClass());
            
            //getBody()는 JWT 바디를 리턴한다(문자열일 수도 있고 Claim 객체일 수도 있다.) 
            DefaultClaims claims=(DefaultClaims)defaultJws.getBody();

            log.info("----------------");

            //Returns the JWT sub (subject) value or null if not present.
            contentValue= claims.getSubject();
        }catch(Exception e){
            e.printStackTrace();
            log.error(e.getMessage());
            contentValue=null;
        }
        return contentValue;
    }
}

```

<br>

이제 test를 해본다.

<br>


![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-12-17-53-46.png){: p}

<br>

**JWTTests.java**

```java
package org.young.club.security;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.young.club.security.util.JWTUtil;

public class JWTTests {
    private JWTUtil jwtUtil;

    //@BeforeEach는 @Test 어노테이션이 붙은 메서드가 호출되기 전에 먼저 호출되어야 한다는 의미를 지닌다.
    @BeforeEach
    public void testBefore(){
        System.out.println("testBefore.........");
        jwtUtil=new JWTUtil();
    }

    @Test
    public void testEncode() throws Exception{
        String email="user95@zerock.org";

        String str=jwtUtil.generateToken(email);

        System.out.println(str);
    }
}

```

<br>

기존의 테스트 코드와는 달리 JWTTests 클래스는 스프링을 이용하는 테스트가 아니므로 내부에서 직접 JWTUtil 객체를 만들어서 사용할 필요가 있다. testEncode()를 이용해서 만들어지는 JWT 문자열을 확인할 수 있다.

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-12-18-10-34.png){: p}

<br>

이제 JWTUtil의 generateToke()에 대한 검증을 테스트 코드에서도 확인해 볼 필요가 있다.

<br>

**JWTTests.java**

```java
(...)
    @Test
    public void testValidate() throws Exception{
        String email="user95@zerock.org";
        
        String str=jwtUtil.generateToken(email);
        
        Thread.sleep(5000);
        
        String resultEmail=jwtUtil.validateAndExtract(str);
        
        System.out.println(resultEmail);
    }
(...)
```

<br>

위의 테스트 코드를 실행했을 때 결과는 email 변수의 값과 동일한 문자열이 출력되는지 확인한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.3/2021-08-12-18-14-08.png){: p}

<br>

JWT에 대한 생성과 검증에 문제가 없다면 최종적으로 ApiLoginFilter/ApiCheckFilter에 적용해야 한다.

ApiLoginFilter에서는 성공한 후에 JWT 문자열을 사용자에게 전송한다.

<br>

**ApiLoginFilter.java**

```java
(...)
@Log4j2
public class ApiLoginFilter extends AbstractAuthenticationProcessingFilter {
    private JWTUtil jwtUtil;

    public ApiLoginFilter(String defaultFilterProcessesUrl){
        super(defaultFilterProcessesUrl);
        this.jwtUtil=jwtUtil;
    }
(...)
```

<br>

주입 받은 JWTUtil을 이용해서 successfulAuthentication() 내에서 문자열을 발행해 준다.

<br>

**ApiLoginFilter.java**

```java
(...)
@Log4j2
public class ApiLoginFilter extends AbstractAuthenticationProcessingFilter {
    private JWTUtil jwtUtil;

    public ApiLoginFilter(String defaultFilterProcessesUrl, JWTUtil jwtUtil) {

        super(defaultFilterProcessesUrl);
        this.jwtUtil = jwtUtil;
    }
    @Override
    public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException, IOException, ServletException {
        log.info("-----------------ApiLoginFilter---------------------");
        log.info("attemptAuthentication");

        String email = request.getParameter("email");
        String pw = request.getParameter("pw");

        UsernamePasswordAuthenticationToken authToken =
                new UsernamePasswordAuthenticationToken(email, pw);

        return getAuthenticationManager().authenticate(authToken);
    }

    @Override
    protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authResult) throws IOException, ServletException {

        log.info("-----------------ApiLoginFilter---------------------");
        log.info("successfulAuthentication: " + authResult);

        log.info(authResult.getPrincipal());

        //email address
        String email = ((ClubAuthMemberDTO)authResult.getPrincipal()).getUsername();

        String token = null;
        try {
            token = jwtUtil.generateToken(email);

            response.setContentType("text/plain");
            response.getOutputStream().write(token.getBytes());

            log.info(token);


        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

<br>

SecurityConfig 클래스에서는 ApiLoginFilter를 생성하는 부분에 JWTUitl을 생성자에서 사용할 수 있도록 수정해 준다.

<br>

**SecurityConfig.java**

```java
(...)
@Bean
    public ApiLoginFilter apiLoginFilter() throws Exception{

        ApiLoginFilter apiLoginFilter =  new ApiLoginFilter("/api/login", jwtUtil());
        apiLoginFilter.setAuthenticationManager(authenticationManager());

        apiLoginFilter
                .setAuthenticationFailureHandler(new ApiLoginFailHandler());

        return apiLoginFilter;
    }
    @Bean
    public JWTUtil jwtUtil() {
        return new JWTUtil();
    }
(...)
```

<br>

프로젝트를 실행하고 브라우저에서 'h