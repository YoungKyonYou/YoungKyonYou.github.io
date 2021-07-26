---
layout: post
title: Thymeleaf/Controller에서 사용자 정보 출력하기
date: 2021-07-26 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_

<br><br>

# <center>Thymeleaf/Controller에서 사용자 정보 출력하기</center>

<br>

로그인이 정상적으로 처리되었다면 사용자의 정보를 화면이나 컨트롤러에서 출력하는 작업을 시도해 본다.

member.html를 수정한다.

<br>

**member.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <h1>For Member</h1>

    <div sec:authorize="hasRole('USER')">Has USER ROLE</div>
    <div sec:authorize="hasRole('MANAGER')">Has MANAGER ROLE</div>
    <div sec:authorize="hasRole('ADMIN')">Has ADMIN ROLE</div>

    <div sec:authorize="isAuthenticated()">
      Only Authenticated user can see this Text
    </div>

    Authenticated username:
    <div sec:authentication="name"></div>
    Authenticated user roles:
    <div sec:authentication="principal.authorities"></div>
  </body>
</html>
```

<br>

**sec**은 시큐리티와 관련된 부분을 처리하는데 사용한다.
<br>

sec:authorize를 이용하면 인가(authorization)와 관련된 정보를 알아내거나 제어가 가능하다. Authentication의 principal이라는 변수를 사용하면 ClubAuthMemberDTO의 내용을 이용할 수 있다. 정상적으로 로그인한 사용자는 아래와 같은 결과를 확인할 수 있다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-5/2021-07-26-17-36-48.png)

<br>

이제 @AuthenticationPrincipla 어노테이션을 사용해서 로그인된 사용자 정보를 확인하는 방법에 대해 알아본다.

<br>

**SampleController.java**

```java
package org.young.club.controller;


import lombok.extern.log4j.Log4j2;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.young.club.security.dto.ClubAuthMemberDTO;

@Controller
@Log4j2
@RequestMapping("/sample/")
//시큐리티와 관련된 설정이 정상적으로 돌아가는지 확인하기 위한 간단한 컨트롤러 구성
public class SampleController {
    //로그인을 하지 않은 사용자도 접근할 수 있는 /sample/all
    @GetMapping("/all")
    public void exAll(){
        log.info("exAll.........");
    }


    //로그인한 사용자만이 접근할 수 있는 '/sample/member'
    @GetMapping("/member")
    //컨트롤러에서 로그인된 사용자 정보를 확인하는 방법은 크게 2가지이다.
    //SecurityContextHolder라는 객체를 사용하는 방법과 직접 파라미터와 어노테이션을 사용하는 방식이 있는데
    //예제에서는 @AuthenticationPrincipla 어노테이션을 사용해서 처리한다.
    public void exMember(@AuthenticationPrincipal ClubAuthMemberDTO clubAuthMember){
        log.info("exMember.........");

        log.info("-------------------------");
        log.info(clubAuthMember);
    }
    //관리자(admin) 권한이 있는 사용자만이 접근할 수 있는 '/sample/admin'
    @GetMapping("/admin")
    public void exAdmin(){
        log.info("exAdmin.........");
    }
}

```

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-5/2021-07-26-17-45-44.png)
