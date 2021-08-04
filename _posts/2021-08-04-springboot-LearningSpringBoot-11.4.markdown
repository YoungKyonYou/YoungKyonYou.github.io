---
layout: post
title: Remember me와 @PreAuthorize-코드로 배우는 스프링 부트 웹 프로젝트-11.4
date: 2021-08-02 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, Google Social Login]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>Remember me와 @PreAuthorize</center>

<br>

스프링 시큐리티의 편리한 기능 중에서 '자동 로그인'이라고 불리는 **'Remember me'**는 최근 모바일과 함께 많이 사용된다. **'Remember me'**는 웹의 인증 방식 중에 '쿠키(HttpCookie)'를 사용하는 방식이다. 이 기능을 활용하면 한번 로그인한 사용자가 브라우저를 닫은 후에 다시 서비스에 접속해도 별도의 로그인 저차 없이 바로 로그인 처리가 진행된다.

<br>

**'Remember me'**에 대한 설정은 아주 간단하다. SecurityConfig에 아래와 같이 remembeMe()설정을 추가하고 UserDetailsService를 지정하면 된다.

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

       http.logout();


       //이것을 추가해줌으로써 구글 로그인을 하면 이전과 달리 빈 화면만 보이게 된다.
       http.oauth2Login().successHandler(successHandler());

       //remember me 설정하는 것이다
        //rememberMe()를 적용할 때는 주로 쿠키를 얼마나 유지할 것인지를 같이 지정한다. 초(second) 단위로 설정하므로 이 코드는 7일간 쿠키가 유지되도록 지정하였다.
       http.rememberMe().tokenValiditySeconds(60*60*7).userDetailsService(userDetailsService());

       //실제 로그인 시에 OAuth를 사용한 로그인이 가능하도록 함
      // http.oauth2Login();
    }

    @Bean
    public ClubLoginSuccessHandler successHandler(){
        return new ClubLoginSuccessHandler(passwordEncoder());
    }
}
```

<br>

아래 사진과 같이 체크 박스가 생기는 것을 볼 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.4/2021-08-04-19-32-26.png){: p}

<br>

주의해야 할 점은 소셜 로그인으로 로그인했을 때는 remember-me를 사용할 수 없다는 점이다. 소셜 로그인을 사용하면 쿠기가 생성되지 않는다.

<br>

SecurityConfig를 사용해서 지정된 URL에 접근 제한을 거는 방식도 나쁘지는 않지만, 매번 URL을 추가할 때마다 이를 설정하는 일은 번거롭다. 스프링 시큐리티는 이런 설정으 어노테이션만으로도 지정할 수 있다. 이를 위해서는 두 가지만 추가하면 된다.

<br>

- <span style="color:orange; font-weight:bold">@EnableGlobalMethodSecurity의 적용</span>
- <span style="color:orange; font-weight:bold">접근 제한이 필요한 컨트롤러의 메서드에 @PreAuthorize 적용</span>

<br>

\*\*@EnableGlobalMethodSecurity는 어노테이션 기반의 접근 제한을 설정할 수 있도록 하는 설정이다. 일반적으로 SecurityConfig와 같이 시큐리티 관련 설정 클래스에 붙이는 것이 일반적이다.

<br>

**SecurityConfig.java**

```java
(...)

@Configuration
@Log4j2
@EnableGlobalMethodSecurity(prePostEnabled = true, securedEnabled = true)
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
(...)
```

<br>

**@EnableGlobalMethodSecurity**는 여러 속성이 있지만 **securedEnabled**는 예전 버전의 **@Secure** 어노테이션이 사용 가능한지를 지정하고 **@PreAuthorize**를 이용하기 위해서는 prePostEnabled 속성을 사용한다. **@PreAuthorize()**의 value로는 문자열로 된 표현식(expression)을 넣는다. 이전의 **@Secure**의 경우 지정된 값을 넣는 형태에서 좀 더 유연한 설정이 가능하다. SecurityConfig 클래스에서 접근 제한을 담당하는 부분의 코드를 주석으로 처리해 본다.

<br>

**SecurityConfig.java**

```java
(...)
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
       (...)
```

<br>

프로젝트를 실행해서 **'/sample/admin'**을 접근해 보면 아무 문제없이 접근이 된다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.4/2021-08-04-19-40-23.png){: p}

<br>

**'/sample/admin'**의 경우 **'ROLE_ADMIN'** 권한을 가진 사용자들만 접근이 가능하게 설정하고 싶다면 **SampleController**를 다음과 같이 수정할 수 있다.

<br>

**SampleController.java**

```java
(...)
 @PreAuthorize("hasRole('ADMIN')")
    @GetMapping("/admin")
    public void exAdmin(){
        log.info("exAdmin.........");
    }
    (...)
```

<br>

**permitAll()** 역시 유사하게 적용할 수 있다. **'/sample/all'**의 경우에는 아래와 같이 적용한다.

```java
@PreAuthorize("permitAll()")
    @GetMapping("/all")
    public void exAll(){
        log.info("exAll.........");
    }
```

<br>

가끔은 로그인이 된 사용자지만 좀 더 특별한 경우에만 사용하고 싶을 때가 있다. 예를 들어 게시판의 게시물 수정이나 삭제 작업 시에 해당 게시물의 작성자만이 해당 URL을 처리하게 하고 싶을 때나 사용자 중에서 특별히 정해진 사용자만이 해당 메서드를 실행하고 싶은 경우가 있을 수 있다.

<br>

**@PreAuthorize**의 value 표현식은 '#'과 같은 특별한 기호나 authentication 같은 내장 변수를 이용할 수 있다. 예를 들어 로그인한 사용자 중에서 'user95@zerock.org'인 사용자만이 접근이 가능하게 만들고 싶다면 아래와 같은 코드를 적용할 수 있다.

<br>

```java
@PreAuthorize("#clubAuthMember !=null && #clubAuthMember.username eq \"user95@zerock.org\"")
    @GetMapping("/exOnly")
    public String exMemberOnly(@AuthenticationPrincipal ClubAuthMemberDTO clubAuthMember){
        log.info("exMemberOnly...........");
        log.info(clubAuthMember);

        return "/sample/admin";
    }
```

<br>

위와 같이 적용한 상태에서 '/sample/exOnly'를 접근하면 로그인이 된 사용자라고 해도 **'user95@zerock.org'**가 아닌 사용자들은 아래와 같은 에러가 나타난다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.4/2021-08-04-19-50-57.png){: p}
