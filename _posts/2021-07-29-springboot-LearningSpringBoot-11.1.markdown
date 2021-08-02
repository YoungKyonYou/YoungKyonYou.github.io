---
layout: post
title: 스프링 시큐리티 소셜 로그인 처리
date: 2021-07-29 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, Google Social Login]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>구글 로그인 시나리오</center>

<br>

스프링 시큐리티를 사용할 때 가장 많이 요구되는 기능은 소셜 로그인이라고 할 수 있다. 소셜 로그인은 국내외 사이트 등에서 제공하는 로그인 통합 기능을 이용해서 사용자가 별도의 회원 가입 없이 자동으로 로그인이 이루어 지도록 구성하는 것이다.

<br>

구글 로그인을 위해서는 먼저 구글 개발자 콘솔을 이용해서 프로젝트를 생성한다. 이를 통해서 구글 클라우드 플랫폼 내에 프로젝트를 생성해주어야 한다.

구글 프로젝트에 현재 프로젝트를 등록하기 위해서는 <span style="color:#7EDBFF; font-weight:bold">Google Developers API Console</span>에 들어가야 한다. 링크는 아래에 두겠다.

<br>

**[Google Developers API Console](https://console.cloud.google.com/apis/dashboard)**

<br>

들어갔더니 예전에 만들어놓은 프로젝트가 있었는데 지금은 사용하지 않으므로 지우려고 찾아봤지만 찾기가 어려웠다... 물론 계속 찾아본 결과 찾았지만 다음에 헤매지 않게 방법을 추가로 기록해두려고 한다.

<br>

화면의 우측 상단에 보면 메뉴바가 있는데 그것을 클릭하면 <span style="color:#001f3f; font-weight:bold">프로젝트 설정</span>이 있다. 이것을 누른다.

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-32-00.png){: p}

<br>

화면 중앙에 바로 종료 버튼이 있는 것을 볼 수 있다. (찾느라 고생했다..)

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-32-18.png){: p}

<br>

자 이제 다 비워진 상태로 링크에 접속하면 아래 사진과 같다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-33-38.png){: p}

<br>

가장 우측에 보면 <span style="color:orange; font-weight:bold">프로젝트 만들기</span>가 보인다. 그것을 누른다. 그리고 프로젝트 이름을 설정하고 **만들기** 버튼을 누른다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-37-04.png){: p}

<br>

그리고 아래 사진과 같이 **API 및 서비스** 메뉴를 클릭하고 들어간다

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-38-48.png){: p}

<br>

그다음 **사용자 인증 정보**를 누르고 가운데에 상단에 있는 **사용자 인증 정보 만들기**->**OAuth 클라이언트 ID**를 클릭한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-39-19.png){: p}

<br>
OAuth 클라이언트 ID를 만드려면
아래 사진과 같이 **동의 화면 구성**을 먼저 해야 한다. **동의 화면 구성**를 클릭해서 설정하자.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-41-43.png){: p}

<br>

동의 화면 구성에서는 구글 계정이 있는 모든 사용자가 사용할 수 있도록 **외부**에 체크를 하고 만들기 버튼을 누른다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-43-48.png){: p}

<br>

다음 설정을 이어간다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-47-54.png){: p}

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-55-28.png){: p}

<br>

아래 사진에서 **범위 추가 또는 삭제**를 누른다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-56-58.png){: p}

<br>

세가지 항목에 체크를 한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-57-18.png){: p}

<br>

결과는 아래와 같다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-57-38.png){: p}

<br>

저장 후 계속을 누른다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-17-58-35.png){: p}

<br>

이제 OAuth ID를 만들 수 있으므로 다시 \*\*사용자 인증 정보로 와서 아래 사진과 같이 OAuth 클라이언트 ID를 다시 선택한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-18-32-11.png){: p}

<br>

아래 사진과 같이 설정하고 만들기를 누른다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-18-34-04.png){: p}

<br>

그리고 나면 OAuth 클라이언트가 생성되면서 <span style="color:#85144b; font-weight:bold">클라이언트 ID와 클라이언트 보안 비밀번호</span>가 나오는데 이 둘을 메모장에 복사 붙여넣기 해둔다.

<br>

챕터10에서 만들었던 프로젝트를 키고 **build.gradle**에 **OAuth**관련 **dependency**를 추가한다.

<br>

**build.gradle**

```gradle
(...)
implementation 'org.springframework.boot:spring-boot-starter-oauth2-client'
(...)
```

<br>

라이브러를 추가한 후에는 **application.properties** 파일을 수정해야 한다. 만일 앞으로 여러 개의 OAuth를 사용하고 싶다면 별도의 설정 파일을 만들어 주는 것이 더 낫다. 별도의 설정 파일 이름은 <span style="color:#7EDBFF; font-weight:bold">'application-xxx.properties'</span>와 같은 이름으로 생성한다. 예제에서는 <span style="color:#7EDBFF; font-weight:bold">'application-oauth.properties'</span>라는 파일을 생성해서 처리한다.(중간에 '-' 대신에 다른 기호를 사용하지 않도록 주의해야 합니다).

<br>

**application-oauth.properties**

```application.properties
spring.security.oauth2.client.registration.google.client-id=(발급 받은 클라이언트 ID)
spring.security.oauth2.client.registration.google.client-secret=(발급 받은 클라이언트 보안 비밀번호)
spring.security.oauth2.client.registration.google.scope=email
```

<br>

기존의 **application.properties**에서는 추가된 파일을 포함해서 동작하도록 설정을 추가한다.

<br>

**application.properties**

```application.properties
spring.profiles.include=oauth
```

<br>

이제 실제 로그인 시에 OAuth를 사용한 로그인이 가능하도록 HttpSecurity 설정을 변경하기 위해 SecurityConfig 클래스를 수정한다. HttpSecurity의 oauth2Login()이라는 부분을 추가하면 된다.

<br>

**SecurityConfig.java**

```java
(...)
public class SecurityConfig extends WebSecurityConfigurerAdapter {
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

       //실제 로그인 시에 OAuth를 사용한 로그인이 가능하도록 함
       http.oauth2Login();
    }
}

```

<br>

이제 프로젝트를 실행하고 <span style="color:orange; font-weight:bold">'/sample/member'</span>를 호출하면 이전과 달리 구글 로그인 링크가 추가된 화면을 아래 사진으로 확인할 수 있다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-23-13-24.png){: p}

<br>

위의 사진에서 **'Google'**를 선택하면 구글에 등록된 OAuth 클라이언트의 이름이 보이면서 로그인을 유도하게 된다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-23-14-21.png){: p}

<br>

정상적으로 로그인이 이루어지면 **'/sample/member'**가 호출되면서 화면에는 다음과 같은 결과가 출력된다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter11/11-1/2021-07-29-23-15-01.png){: p}

<br>

