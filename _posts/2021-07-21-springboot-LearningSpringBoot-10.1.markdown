---
layout: post
title: SpringBoot와 Spring Security 연동
date: 2021-07-21 10:00:00 0000
tags: [Intellij, SpringBoot, Spring Security]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_

<br><br>

# <center>SpringBoot와 Spring Security 연동</center>

<br>

이번 챕터에서는 아래와 같은 내용을 학습한다.

- 스프링 시큐리티에서 제공하는 로그인 처리 방식의 이해
- JPA와 연동하는 커스텀 로그인 처리
- Thymeleaf에서 로그인 정보 활용하기

<br>

**프로젝트 생성**

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-21-18-00-36.png)

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-21-18-01-05.png)

<br>

**의존성 추가**

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-21-18-01-42.png)

<br>

<style>

</style>

**build.gradle 설정**

```gradle
plugins {
    id 'org.springframework.boot' version '2.5.2'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
    id 'war'
}

group = 'org.young'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

configurations {
    compileOnly {
        extendsFrom annotationProcessor
    }
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-security'
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.thymeleaf.extras:thymeleaf-extras-springsecurity5'

    //추가한 부분
    //mysql 드라이버
    implementation group: 'mysql', name: 'mysql-connector-java', version: '8.0.25'
    //Thymeleaf 확장 플러그인은 화면을 제작할 때 스프링 시큐리티 객체들을 처리하는 용도이다.
    implementation group: 'org.thymeleaf.extras', name: 'thymeleaf-extras-springsecurity5', version: '3.0.4.RELEASE'
    implementation group: 'org.thymeleaf.extras', name: 'thymeleaf-extras-java8time', version: '3.0.4.RELEASE'
    //

    compileOnly 'org.projectlombok:lombok'
    developmentOnly 'org.springframework.boot:spring-boot-devtools'
    annotationProcessor 'org.projectlombok:lombok'
    providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testImplementation 'org.springframework.security:spring-security-test'
}

test {
    useJUnitPlatform()
}

```

<br>

**application.properties**

```application.properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springsecurity?serverTimezone=UTC&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=root

#서버 시작 시점에 DDL 문을 생성하여 DB에 적용한다
spring.jpa.hibernate.ddl-auto=update
#True로 하면 sql문을 보기 좋게 설정한다
spring.jpa.properties.hibernate.format_sql=true
#적용된 sql문을 보여준다.
spring.jpa.show-sql=true
#Thymeleaf 템플릿 캐싱 비활성화
#thymeleaf를 사용하다 수정 사항이 생길 대 수정을 하면
#재시작을 해줘야 한다. cache가 계속 쌓이기 때문이다.
#이를 방지하여 브라우저 새로고침만으로도 수정 사항을 확인하기 위해서 이것을 추가한다.
spring.thymeleaf.cache=false

spring.servlet.multipart.enabled=true
spring.servlet.multipart.location=C:\\Users\\nick1\\kpu\\spring_security\\upload
spring.servlet.multipart.max-request-size=30MB
spring.servlet.multipart.max-file-size=10MB

#업데이트 실시간 반영
spring.devtools.livereload.enabled=true

#시큐리티와 관련된 부분은 좀 더 로그 레벨을 낮게 설정해서 자세한 로그를 확인할 수 있도록 한다.
logging.level.org.springframework.security.web=debug
logging.level.org.young.security=debug
```

<br>

이 상태에서 어플리케이션이 제대로 작동하나 실행해 본다. 실행하면 아래 사진과 같이 **password**가 나온다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-16-06-24.png)

<br>

프로젝트 초기에 아무 계정도 없을 때 사용할 수 있는 임시 패스워드 역할을 한다. 프로젝트가 정상적으로 실행된다면 'http://localhost:8080/login'의 경로로 접근해서 화면에서 **'user'**라는 계정으로 설정하고 위의 패스워드를 입력해서 로그인을 테스트 한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-16-07-51.png)

<br>

컨트롤러가 작성되지 않았기 때문에 아래와 같이 나온다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-16-08-12.png)

<br>

시큐리티 설정 클래스를 작성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-16-20-04.png)

<br>

**SecurityConfig 클래스**

```java
package org.young.club.config;

//시큐리티 관련 기능을 쉽게 설정하기 위해서 WebSecurity ConfigurerAdapter라는 클래스를 상속으로 처리한다.
//WebSecurityConfigurer Adapter 클래스는 주로 override를 통해서 여러 설정을 조정하게 된다.

import lombok.extern.log4j.Log4j2;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@Log4j2
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
}

```

<br>

**SampleController 클래스**

```java
package org.young.club.controller;


import lombok.extern.log4j.Log4j2;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;

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
    public void exMember(){
        log.info("exMember.........");
    }
    //관리자(admin) 권한이 있는 사용자만이 접근할 수 있는 '/sample/admin'
    @GetMapping("/admin")
    public void exAdmin(){
        log.info("exAdmin.........");
    }
}

```

<br>

컨트롤러로 인한 페이지가 표시될 수 있도록 대응되는 html 파일을 구성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-16-21-36.png)

<br>

**all.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <h1>For All</h1>
  </body>
</html>
```

<br>

**admin.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <h1>For Admin</h1>
  </body>
</html>
```

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
  </body>
</html>
```

<br>

PasswordEncoding를 사용하기 위해서 SecurityConfig 클래스에 추가한다.

<br>

**SecurityConfig.java**

```java
package org.young.club.config;

//시큐리티 관련 기능을 쉽게 설정하기 위해서 WebSecurity ConfigurerAdapter라는 클래스를 상속으로 처리한다.
//WebSecurityConfigurer Adapter 클래스는 주로 override를 통해서 여러 설정을 조정하게 된다.

import lombok.extern.log4j.Log4j2;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
@Log4j2
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    //PasswordEncoder는 패스워드를 인코딩하는 것인데 주목적은 역시 패스워드를 암호화하는 것이다
    //PasswordEncoder는 인터페이스로 설계되어 있으므로 실제 설정에서는 이를 구현하거나 구현된 클래스를 이용해야만 한다.
    //스프링 시큐리티에는 여러 종류의 PasswordEncoder를 제공하고 있는데 그중에서도 가장 많이 사용하는 것은
    //BCryptPasswordEncoder라는 클래스이다. 이는 'bcrypt'라는 해시 함수를 이용해서 패스워드를 암호화하는 목적으로 설계됐다.
    //SecurityConfig에는 @Bean을 이용해서 BCryptPasswordEncoder를 지정한다.
    @Bean
    PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }
}

```

<br>

PasswordTests라는 테스트 클래스를 작성해 본다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-08-02.png)

<br>

**PasswordTests.java**

```java
package org.young.club.security;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.security.crypto.password.PasswordEncoder;

@SpringBootTest
public class PasswordTests {

    @Autowired
    private PasswordEncoder passwordEncoder;

    //BCryptPasswordEncoder로 암호화된 패스워드는 다시 원래대로 복호화가 불가능하다
    //매번 암호화된 값도 다르게 된다
    //대신에 특정한 문자열이 암호화된 결과인지만을 확인할 수 있다.(.matches()함수를 통해서)
    @Test
    public void testEncoder(){
        String password="1111";

        String enPw=passwordEncoder.encode(password);

        System.out.println("enPw:"+enPw);

        boolean matchResult=passwordEncoder.matches(password, enPw);

        System.out.println("matchResult: "+matchResult);
    }
}

```

<br>

위 테스트를 통해 인코딩된 password가 나타난다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-24-06.png)

<br>

enPw에 나오는 내용을 복사해두고 다시 SecurityConfig.java로 돌아와 코드를 추가한다.

**SecurityConfig.java**

```java
package org.young.club.config;

//시큐리티 관련 기능을 쉽게 설정하기 위해서 WebSecurity ConfigurerAdapter라는 클래스를 상속으로 처리한다.
//WebSecurityConfigurer Adapter 클래스는 주로 override를 통해서 여러 설정을 조정하게 된다.

import lombok.extern.log4j.Log4j2;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
@Log4j2
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    //PasswordEncoder는 패스워드를 인코딩하는 것인데 주목적은 역시 패스워드를 암호화하는 것이다
    //PasswordEncoder는 인터페이스로 설계되어 있으므로 실제 설정에서는 이를 구현하거나 구현된 클래스를 이용해야만 한다.
    //스프링 시큐리티에는 여러 종류의 PasswordEncoder를 제공하고 있는데 그중에서도 가장 많이 사용하는 것은
    //BCryptPasswordEncoder라는 클래스이다. 이는 'bcrypt'라는 해시 함수를 이용해서 패스워드를 암호화하는 목적으로 설계됐다.
    //SecurityConfig에는 @Bean을 이용해서 BCryptPasswordEncoder를 지정한다.
    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    //SecurityConfig에는 AuthenticationManager의 설정을 쉽게 처리할 수 있도록 도와주는
    //configure() 메서드를 override해서 처리한다. 파라미터의 타입인 AuthenticationManagerBuilder는
    //말 그대로 코드를 통해서 직접 인증 매니저를 설정할 때 사용한다.
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        //사용자 계정은 user1, 일단 인메모리 스피링 시큐리티를 실험한다.
        //inMemoryAuthentication()는 인 메모리 authentication를 AuthenticationManagerBuilder에 추가하고
        //원하는데로 인 메모리 authentication를 구성하는 것이 가능한 InMemoryUserDetailsManagerConfigurer 타입을 반환한다.
        //withUser()는 생성되는 UserDetailsManager에 user를 추가하는 것을 허용한다
        //이 함수는 다수의 users를 등록하기 위해서 여러 번 호출이 가능하다
        auth.inMemoryAuthentication().withUser("user1")
        //1111 패스워드 인코딩 결과
        .password("$2a$10$3mm3ssAaaIYCfmJQu2w5KedCy.1yO7O3J9/Me72i5drQkHm54F2CW")
        //사용자가 가지는 권한은 USER라는 권한으로 지정한다.
        .roles("USER");
    }
}

```

<br>

애플리케이션을 실행하고 위에서 설정한 아이디와 비밀번호를 통해서 localhost:8080/sample/all에 접속해 본다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-27-48.png)

<br>

그리고 인가(Authorization)가 필요한 리소스 설정을 한다

**SecurityConfig.java**

```java
package org.young.club.config;
(...)
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    (...)

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        (...)
    }

    //스프링 시큐리티를 이용해서 특정한 리소스에 접근 제한을 하는 방식은 크게 두 가지이다.
    //1) 설정을 통해서 패턴을 지정하거나
    //2) 어노테이션을 이용해서 적용하는 방법이 있다.
    //어노테이션을 이용하는 방식이 더 간단하긴 하지만 우선은 SecurityConfig 클래스로 설정해 본다.
    @Override
    protected void configure(HttpSecurity http) throws Exception {
       //http.authorizeRequests()로 인증이 필요한 자원들을 설정할 수 있고 antMatchers()는
        // '**/*'와 같은 앤트 스타일의 패턴으로 원하는 자원을 선택할 수 있다.
        //마지막으로 permitAll()의 경우는 말 그대로 '모든 사용자에게 허락'한다는 의미이므로
        //로그인하지 않은 사용자도 익명의 사용자로 간주되어서 접근이 가능하게 된다.
        //프로젝트를 재시작해서 /sample/all에 접속하면 별도의 로그인 없이도 접근이 가능해 진다.
        http.authorizeRequests().antMatchers("/sample/all").permitAll();
    }
}

```

<br>

애플리케이션을 다시 시작하고 '/sample/all'에 접속하면 별다른 로그인 없이도 페이지에 접근한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-38-03.png)

<br>

반면 다시 아래와 같이 설정을 변경하고 '/sample/member'를 호출하면 Access Denied된다.

<br>

**SecurityConfig.java**

```java
package org.young.club.config;
(...)
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    (...)

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        (...)
    }

    //스프링 시큐리티를 이용해서 특정한 리소스에 접근 제한을 하는 방식은 크게 두 가지이다.
    //1) 설정을 통해서 패턴을 지정하거나
    //2) 어노테이션을 이용해서 적용하는 방법이 있다.
    //어노테이션을 이용하는 방식이 더 간단하긴 하지만 우선은 SecurityConfig 클래스로 설정해 본다.
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
    }
}

```

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-42-04.png)

<br>

HttpSecurity의 formLogin()이라는 기능은 이와 같이 인가/인증 절차에서 문제가 발생했을 때 로그인 페이지를 보여주도록 지정할 수 있고 화면으로 로그인 방식을 지원한다는 의미로 사용된다.

<br>

**SecurityConfig.java**

```java
package org.young.club.config;
(...)
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    (...)

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        (...)
    }

    //스프링 시큐리티를 이용해서 특정한 리소스에 접근 제한을 하는 방식은 크게 두 가지이다.
    //1) 설정을 통해서 패턴을 지정하거나
    //2) 어노테이션을 이용해서 적용하는 방법이 있다.
    //어노테이션을 이용하는 방식이 더 간단하긴 하지만 우선은 SecurityConfig 클래스로 설정해 본다.
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
    }
}

```

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-44-41.png)

<br>

위 사진과 같이 formLogin()이 적용되면 인가/인증에 실패하는 경우에 로그인 페이지를 볼 수 있게 된다.

<br>

formLogin()과 마찬가지로 logout() 메서드를 이용하면 로그아웃 처리가 가능하다. formLogout() 역시 로그인과 마찬가지로 별도의 설정이 없는 경우에는 스프링 시큐리티가 제공하는 웹 페이지를 보게 된다. SecurityConfig에 logout()을 적용해주기만 하면 된다.

<br>

**SecurityConfig.java**

```java
package org.young.club.config;
(...)
//모든 시큐리티 관련 설정이 추가되는 부분이므로 앞으로 작성하는 예제에서 핵심적인 역할을 한다.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    (...)

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        (...)
    }

    //스프링 시큐리티를 이용해서 특정한 리소스에 접근 제한을 하는 방식은 크게 두 가지이다.
    //1) 설정을 통해서 패턴을 지정하거나
    //2) 어노테이션을 이용해서 적용하는 방법이 있다.
    //어노테이션을 이용하는 방식이 더 간단하긴 하지만 우선은 SecurityConfig 클래스로 설정해 본다.
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
        //csrf 토큰을 발행하지 않는다.
       http.csrf().disable();
       //로그아웃 처리
       http.logout();
    }
}

```

<br>

프로젝트를 다시 실행하고 /sample/member로 접근하면 아래와 같이 로그아웃 되고 다시 로그인을 하라는 상태가 된다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-10.1/2021-07-24-17-59-51.png)

<br>

logout()에서 주의해야 할 점은 CSRF 토큰을 사용할 때는 반드시 POST 방식으로만 로그아웃을 처리한다는 점이다. CSRF 토큰을 이용하는 경우에는 /logout 이라는 URL을 호출했을 때는 <form> 태그와 버튼으로 구성된 화면을 보게 되지만 CSRF 토큰을 disable()로 비활성화 시키면 GET 방식('/logout')으로도 로그아웃 처리된다.(위 그림과 같이)
