---
layout: post
title: 시큐리티를 위한 UserDetailsService
date: 2021-07-26 10:00:00 0000
tags: [Intellij, SpringBoot, Spring Security]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_

<br><br>

# <center>시큐리티를 위한 UserDetailsService</center>

<br>

다음으로 진행할 작업은 스프링 시큐리티가 ClubMemberRepository를 이용해서 회원을 처리하는 부분을 제작해야 한다.

새로운 패키지와 자바 파일을 생성한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-4/2021-07-26-16-14-17.png)

<br>

**ClubAuthMemberDTO.java**

```java
package org.young.club.security.dto;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.User;

import java.util.Collection;

@Log4j2
//User 클래스는 UserDetailsService로부터 핵심 유저 정보를 모델링한다.
//User 클래스를 상속하고 부모 클래스인 User 클래스의 생성자를 호출할 수 있는 코드를 만든다.
//부모 클래스인 User 클래스에 사용자 정의 생성자가 있으므로 반드시 호출할 필요가 있다.

//ClubAuthMemberDTO는 DTO 역할을 수행하는 클래스인 동시에 스프링 시큐리티에서 인가/인증 작업에 사용할 수 있다.
//password는 부모 클래스를 사용하므로 별도의 멤버 변수로 선언하지 않는다.
public class ClubAuthMemberDTO extends User {
    private String email;
    private String name;
    private boolean fromSocial;
    public ClubAuthMemberDTO(String username, String password, boolean fromSocial, Collection<? extends GrantedAuthority> authorities){
        //User 클래스의 생성자를 호출한다.
        super(username, password, authorities);

        this.email=username;
        this.fromSocial=fromSocial;
    }
}

```

<br>

ClubMember가 ClubAuthMemberDTO라는 타입으로 처리된 가장 큰 이유는 사용자의 정보를 가져오는 핵심적인 역할을 하는 UserDetailsService라는 인터페이스 때문이다.

스프링 시큐리티의 구조에서 인증을 담당하는 AuthenticationManager는 내부적으로 UserDetailsService를 호출해서 사용자의 정보를 가져온다.

현재 예제와 같이 JPA로 사용자의 정보를 가져오고 싶다면 이 부분을 UserDetailsService가 이용하는 구조로 작성할 필요가 있다.

추가된 service패키지에는 이를 위한 ClubUserDetailsService 클래스를 다음과 같이 추가한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-4/2021-07-26-16-23-19.png)

<br>

**ClubUserDetailsService.java**

```java
package org.young.club.security.service;

import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

@Log4j2
//Service어노테이션을 사용해서 자동으로 스프링에서 빈으로 처리될 수 있게 한다.
//ClubUserDetailsService가 빈(Bean)으로 등록되면 이를 자동으로 스프링 시큐리티에서
//UserDetailsService로 인식하기 때문에 기존에 임시로 코드로 직접 설정한
//configure(AuthenticationManagerBuilder auth) 부분을 사용하지 않도록 수정한다.
@Service
public class ClubUserDetailsService implements UserDetailsService {

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        log.info("ClubUserDetailsService loadUserByUsername"+username);
        return null;
    }
}

```

<br>

이제 SecureConfig.java 에서 정의했던 configure 메서드가 필요없으므로 지우거나 주석 처리한다.

<br>

**SecureConfig.java**

```java
package org.young.club.config;

//시큐리티 관련 기능을 쉽게 설정하기 위해서 WebSecurity ConfigurerAdapter라는 클래스를 상속으로 처리한다.
//WebSecurityConfigurer Adapter 클래스는 주로 override를 통해서 여러 설정을 조정하게 된다.

import lombok.extern.log4j.Log4j2;
 (...)
@Configuration
@Log4j2
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests().antMatchers("/sample/all").permitAll()
                                //아래와 같이 설정하고 /sample/member'를 호출하면 Access Denied 된다.
                                .antMatchers("/sample/member").hasRole("USER");

        //인가/인증에 문제시 로그인 화면면
       http.formLogin();
    }

}

```

<br>

정상적인 처리를 위해서 ClubUserDetailsService와 ClubMemberRepository를 연동하는 것은 아래와 같이 처리할 수 있다.

<br>

**ClubUserDetailsService.java**

```java
package org.young.club.security.service;

import lombok.RequiredArgsConstructor;
import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;
import org.young.club.entity.ClubMember;
import org.young.club.repository.ClubMemberRepository;
import org.young.club.security.dto.ClubAuthMemberDTO;

import java.util.Optional;
import java.util.stream.Collectors;

@Log4j2
//Service어노테이션을 사용해서 자동으로 스프링에서 빈으로 처리될 수 있게 한다.
//ClubUserDetailsService가 빈(Bean)으로 등록되면 이를 자동으로 스프링 시큐리티에서
//UserDetailsService로 인식하기 때문에 기존에 임시로 코드로 직접 설정한
//configure(AuthenticationManagerBuilder auth) 부분을 사용하지 않도록 수정한다.
@Service
@RequiredArgsConstructor
public class ClubUserDetailsService implements UserDetailsService {
    private final ClubMemberRepository clubMemberRepository;
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        log.info("ClubUserDetailsService loadUserByUsername"+username);

        Optional<ClubMember> result=clubMemberRepository.findByEmail(username, false);
        System.out.println("username:"+username);
        if(result.isPresent()==false){
            throw new UsernameNotFoundException("Check Email or Social ");
        }

        ClubMember clubMember=result.get();

        System.out.println(clubMember.getRoleSet().toString());
        log.info("--------------------------");
        log.info(clubMember);

        //ClubMember를 UserDetails 타입으로 처리하기 위해서 ClubAuthMemberDTO 타입으로 변환
        ClubAuthMemberDTO clubAuthMember=new ClubAuthMemberDTO(
                clubMember.getEmail(),
                clubMember.getPassword(),
                clubMember.isFromSocial(),
                //ClubMemberRole은 스프링 시큐리티에서 사용하는 SimpleGrantedAuthority로 변환,
                //이때 'ROLE_'라는 접두어를 추가해서 사용한다.
                //user95@zerock.org 같은 경우 롤이 3개다 [USER, MANAGER, ADMIN]
                //이 각각을 [ROLE_ADMIN, ROLE_MANAGER, ROLE_USER]로 변환해서 Set으로 넣어주고 그 컬렉션을 반환한다.
                clubMember.getRoleSet().stream()
                .map(role->new SimpleGrantedAuthority("ROLE_"+role.name())).collect(Collectors.toSet()));

        clubAuthMember.setName(clubMember.getName());
        System.out.println(clubAuthMember.getAuthorities().toString());
        return clubAuthMember;
    }
}

```

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-4/2021-07-26-17-04-56.png)

<br>

정상적으로 로그인한 결과이다. 중요한 것은 AuthenticationManager는 내부적으로 UserDetailsService를 호출해서 사용자의 정보를 가져온다.
즉 **loadUserByUsername** 메서드를 통해서 사용자 정보(**clubAuthMember**)를 넘겨받는다. 그 clubAuthMember는 DTO형태로 포장되서 반환되는 것이다.
