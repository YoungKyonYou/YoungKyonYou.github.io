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

<div class="webnots-success webnots-notification-box">이메일은 문제가 없지만 패스워드나 사용자의 이름 등을 데이터베이스에 추가하는 작업은 고민을 좀 해야 한다.</div>

<br>

임의로 패스워드를 지정해서 데이터베이스에 저장하는 경우 나중에 문제가 될 수 있기 때문이다. 이에 대한 논의는 조금 미룬다. 우선은 데이터베이스에 저장하는 코드를 작성한다.

<br>

**ClubOAuth2UserDetailsService.java**

```java
package org.young.club.security.service;

import lombok.RequiredArgsConstructor;
import lombok.extern.log4j.Log4j2;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.oauth2.client.userinfo.DefaultOAuth2UserService;
import org.springframework.security.oauth2.client.userinfo.OAuth2UserRequest;
import org.springframework.security.oauth2.core.OAuth2AuthenticationException;
import org.springframework.security.oauth2.core.user.OAuth2User;
import org.springframework.stereotype.Service;
import org.young.club.entity.ClubMember;
import org.young.club.entity.ClubMemberRole;
import org.young.club.repository.ClubMemberRepository;

import java.util.Optional;

@Log4j2
@Service
@RequiredArgsConstructor
public class ClubOAuth2UserDetailsService extends DefaultOAuth2UserService {
    private final ClubMemberRepository repository;
    private final PasswordEncoder passwordEncoder;
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

        String email=null;

        //이메일 정보 추출
        if(clientName.equals("Google")){
            email=oAuth2User.getAttribute("email");
        }

        log.info("EMAIL: "+email);

        ClubMember member=saveSocialMember(email);

        return oAuth2User;
    }

    //ClubMemberRepository를 이용해서 소셜 로그인한 이메일을 처리하는 부분은 다음과 같다.
    private ClubMember saveSocialMember(String email){
        Optional<ClubMember> result=repository.findByEmail(email,true);

        //추출된 이메일 주소로 현재 데이터베이스에 있는 사용자가 아니라면 자동으로 회원 가입을 처리한다.
        if(result.isPresent()){
            return result.get();
        }

        ClubMember clubMember=ClubMember.builder().email(email)
                .name(email)
                .password(passwordEncoder.encode("1111"))
                .fromSocial(true)
                .build();

        clubMember.addMemberRole(ClubMemberRole.USER);
        repository.save(clubMember);
        return clubMember;
    }
}

```

<br>

DefaultOAuth2UserService의 loadUser()의 경우 일반적인 로그인과 다르게 OAuth2User 타입의 객체를 반환해야 하는데 지금까지 개발했던 코드로는 화면에서 아래와 같이 메일 주소가 아닌 사용자의 번호가 출력되는 것을 볼 수 있다.

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.2/2021-08-02-17-46-49.png){: p}

<br>

컨트롤러에서도 동일하게 같은 문제가 발생하는데 앞에서 만들어진 컨트롤러는 파라미터로 ClubAuthMemberDTO 타입을 사용하기 때문에 소셜 로그인을 하는 경우에는 null이라는 결과가 발생한다. 이를 해결하기 위해서는 OAuth2User 타입을 ClubAuthMemberDTO 타입으로 사용할 수 있도록 처리해 줄 필요가 있다. 다행히도 OAuth2User 타입은 인터페이스로 설계되어 있으므로 ClubAuthMemberDTO를 수정해서 이 문제를 해결한다.

<br>

**ClubAuthMemberDTO.java**

```java
package org.young.club.security.dto;

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.oauth2.core.user.OAuth2User;

import java.util.Collection;
import java.util.Map;

@Log4j2
//User 클래스는 UserDetailsService로부터 핵심 유저 정보를 모델링한다.
//User 클래스를 상속하고 부모 클래스인 User 클래스의 생성자를 호출할 수 있는 코드를 만든다.
//부모 클래스인 User 클래스에 사용자 정의 생성자가 있으므로 반드시 호출할 필요가 있다.

//ClubAuthMemberDTO는 DTO 역할을 수행하는 클래스인 동시에 스프링 시큐리티에서 인가/인증 작업에 사용할 수 있다.
//password는 부모 클래스를 사용하므로 별도의 멤버 변수로 선언하지 않는다.
@Getter
@Setter
@ToString
public class ClubAuthMemberDTO extends User implements OAuth2User {
    private String email;
    private String name;
    private String password;
    private boolean fromSocial;
    private Map<String, Object> attr;

    //OAuth2User는 Map 타입으로 모든 인증 결과를 attributes라는 이름으로 가지고 있기 때문에
    // ClubAuthMember 역시 attr이라는 변수를 만들어주고 getAttribute() 메서드를 override한 점이다.
    public ClubAuthMemberDTO(String username, String password, boolean fromSocial, Collection<? extends GrantedAuthority> authorities, Map<String, Object> attr){
        this(username,password, fromSocial, authorities);
        this.attr=attr;
    }
    public ClubAuthMemberDTO(String username, String password, boolean fromSocial, Collection<? extends GrantedAuthority> authorities){
        super(username, password, authorities);
        this.email=username;
        this.password=password;
        this.fromSocial=fromSocial;
    }

    @Override
    public Map<String, Object> getAttributes() {
        return this.attr;
    }
}

```

<br>

loadUser()의 내부는 다음과 같이 수정한다.

**ClubOAuth2UserDetailsService.java**

```java
(...)
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

        String email=null;

        //이메일 정보 추출
        if(clientName.equals("Google")){
            email=oAuth2User.getAttribute("email");
        }

        log.info("EMAIL: "+email);
        //조금 뒤에 사용
       // ClubMember member=saveSocialMember(email);
      //  return oAuth2User;
        ClubMember member=saveSocialMember(email);
        ClubAuthMemberDTO clubAuthMember=new ClubAuthMemberDTO(member.getEmail(),member.getPassword(),true,member.getRoleSet().stream()
                .map(role->new SimpleGrantedAuthority("ROLE_"+role.name()))
        .collect(Collectors.toList()),
                oAuth2User.getAttributes());
        clubAuthMember.setName(member.getName());
        return clubAuthMember;
    }

    //ClubMemberRepository를 이용해서 소셜 로그인한 이메일을 처리하는 부분은 다음과 같다.
    private ClubMember saveSocialMember(String email){
        Optional<ClubMember> result=repository.findByEmail(email,true);

        //추출된 이메일 주소로 현재 데이터베이스에 있는 사용자가 아니라면 자동으로 회원 가입을 처리한다.
        if(result.isPresent()){
            return result.get();
        }

        ClubMember clubMember=ClubMember.builder().email(email)
                .name(email)
                .password(passwordEncoder.encode("1111"))
                .fromSocial(true)
                .build();

        clubMember.addMemberRole(ClubMemberRole.USER);
        repository.save(clubMember);
        return clubMember;
    }
}
```

<br>

loadUser()에서 가장 달라지는 점은 다음과 같다.

<div class="webnots-success webnots-notification-box">saveSocialMember()한 결과로 나오는 ClubMember를 이용해서 ClubAuthMemberDTO를 구성한다.</div>
<div class="webnots-success webnots-notification-box">OAuth2User의 모든 데이터는 ClubAuthMemberDTO의 내부로 전달해서 필요한 순간에 사용할 수 있도록 한다.</div>

<br>

위오 같은 구조를 가진 후에 구글 계정으로 '/sample/member'를 시도하면 아래와 같이 구글 계정을 이용하더라도 이메일 주소를 사용할 수 있게 된다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-11.2/2021-08-02-18-00-32.png){: p}
