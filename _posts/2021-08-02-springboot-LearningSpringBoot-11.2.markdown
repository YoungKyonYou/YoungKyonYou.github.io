---
layout: post
title: 현재 프로젝트와의 연동
date: 2021-08-02 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, Google Social Login]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>현재 프로젝트와의 연동</center>

<br>

이제는 아쉬운 점들을 찾아서 수정해본다.

아래와 같은 점들을 고려해 본다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">소셜 로그인 처리 시에 사용자의 이메일 정보를 추출한다.</div>
<div class="webnots-success webnots-notification-box">현재 데이터베이스와 연동해서 사용자 정보를 관리해야 한다.</div>
<div class="webnots-success webnots-notification-box">기존 방식으로도 로그인할 수 있어야 하고, 소셜 로그인으로도 동일하게 동작해야 한다. </div>

<br>

가장 먼저 해야 하는 작업은 구글과 같은 서비스에서 로그인 처리가 끝난 결과를 가져오는 작업을 사용할 수 있는 환경을 구성하는 것이다. 이를 위해서는 실제 소셜 로그인 과정에서 동작하는 존재인 <span style="color:orange; font-weight:bold">OAuth2UserService</span>라는 것을 알아야만 한다.

<br>

**org.springframework.security.oauth2.client.userinfo.OAuth2UserService 인터페이스**는 **UserDetailsService**의 **OAuth** 버전이라고 생각할 수 있다. 이를 구현하는 것은 **OAuth의 인증 결과**를 처리한다는 것이다.

<br>

인터페이스를 직접 구현할 수도 있지만 편하게 하고 싶다면 구현된 클래스 중에서 하나를 사용하는 방식이 더 편할 것이므로 **DefaultOAuth2UserService** 클래스를 상속해서 구현한다. security 패키지 내에 있는 service 패키지에 **DefaultOAuth2UserService**를 상속하는 클래스를 \*\*ClubOAuth2UserDetailsServices라는 클래스로 구성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.2/2021-08-02-16-54-43.png){: p}

<br>

**ClubOAuth2UserDetailsServices.java**

```java
package org.young.club.security.service;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.oauth2.client.userinfo.DefaultOAuth2UserService;
import org.springframework.security.oauth2.client.userinfo.OAuth2UserRequest;
import org.springframework.security.oauth2.core.OAuth2AuthenticationException;
import org.springframework.security.oauth2.core.user.OAuth2User;
import org.springframework.stereotype.Service;

@Log4j2
@Service
public class ClubOAuth2UserDetailsService extends DefaultOAuth2UserService {
    @Override
    public OAuth2User loadUser(OAuth2UserRequest userRequest) throws OAuth2AuthenticationException {
        log.info("---------------------------------------");
        log.info("userRequest:" +userRequest);
        return super.loadUser(userRequest);
    }
}

```

<br>

프로젝트를 재시작한 후에 '/sample/member'로 로그인을 시도하면 위의 코드가 정상적으로 동작하는 것을 확인할 수 있다.

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.2/2021-08-02-17-00-56.png){: p}

<br>

<span style="color:#85144b; font-weight:bold; font-size:30px">사용자의 이메일 추출</span>

loadUser()에서 사용하는 OAuth2UserRequest는 현재 어떤 서비스를 통해서 로그인이 이루어졌는지 알아내고 전달된 값들을 추출할 수 있는 데이터를 Map<String, Object>의 형태로 사용할 수 있다. 최대한 많은 정보를 조회하기 위해서 ClubOAuth2UserDetailsService의 loadUser()를 아래와 같이 수정한다.

**ClubOAuth2UserDetailsServices.java**

```java
package org.young.club.security.service;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.oauth2.client.userinfo.DefaultOAuth2UserService;
import org.springframework.security.oauth2.client.userinfo.OAuth2UserRequest;
import org.springframework.security.oauth2.core.OAuth2AuthenticationException;
import org.springframework.security.oauth2.core.user.OAuth2User;
import org.springframework.stereotype.Service;

@Log4j2
@Service
public class ClubOAuth2UserDetailsService extends DefaultOAuth2UserService {
    @Override
    public OAuth2User loadUser(OAuth2UserRequest userRequest) throws OAuth2AuthenticationException {
        log.info("---------------------------------------");
        log.info("userRequest:" +userRequest);

        String clientName=userRequest.getClientRegistration().getClientName();

        //OAuth로 연결한 클라이언트 이름과 이때 사용한 파라미터들을 출력한다.
        log.info("clientName: "+clientName);
        log.info(userRequest.getAdditionalParameters());

        //DefaultOAuth2UserService의 loadUser()는 OAuth2UserRequest라는 타입의 파라미터와 OAuth2User
        //라는 타입의 리턴 타입을 반환한다.
        OAuth2User oAuth2User=super.loadUser(userRequest);

        log.info("========================");

        //loadUser()에서 사용하는 OAuth2UserRequest는 현재 어떤 서비스를 통해서 로그인이 이루어졌는지
        //알아내고 전달된 값들을 추출할 수 있는 데이터를 Map<String, Object>의 형태로
        //사용할 수 있다. 최대한 많은 정보를 조회할 수 있다.
        oAuth2User.getAttributes().forEach((k,v)->{
            log.info(k+":"+v);
        });
        return oAuth2User;
    }
}

```

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.2/2021-08-02-17-23-54.png){: p}

<br>

위의 코드를 이용한 결과로 출력되는 내용은 구글에서 프로젝트를 등록하면서 지정한 'API 범위'의 항목과 **application-oauth.properties** 설정 파일과 관련이 있다.

<br>

위의 사진에서 sub, picture, email, email_verified 항목이 출력되는 것을 볼 수 있다. 위와 같이 **OAuth2User**를 이용하면 로그인한 사용자의 이메일 주소를 알아낼 수 있으므로 남은 작업은 이를 이용해서 데이터베이스에 추가하는 작업을 진행할 수 있다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">

<div class="webnots-success webnots-notification-box">이메일은 문제가 없지만 패스워드나 사용자의 이름 등을 데이터베이스에 추가하는 작업은 고민을 좀 해야 한다.</div>
