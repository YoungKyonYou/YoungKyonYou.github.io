---
layout: post
title: 인텔리제이로 스프링부트 시작하기-스프링 부트와 AWS로 혼자 구현하는 웹 서비스-1
date: 2021-08-13 11:00:00 0000
tags: [Intellij, SpringBoot, Book]
categories: [SpringBoot]
description: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '스프링 부트와 AWS로 혼자 구현하는 웹 서비스'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>인텔리제이로 스프링부트 시작하기</center>

<br>

프로젝트를 생성하는 것부터 시작한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-00-00.png){: p}

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-01-54.png){: p}

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-03-15.png){: p}

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-03-32.png){: p}

<br>

위와 같은 작업이 모두 끝나면 그레이들 기반의 자바 프로젝트가 생성된다.

<br>

그리고 위의 사진을 보면 Dependencies로 5가지를 추가하는 것을 볼 수 있는데 이는 책에 없는 내용이고 내가 임의로 한 것이다. 차후에 있을 게시물에서 저런 것들을 쓸 것이다.

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">
<div class="webnots-information webnots-notification-box">참고로 책에서는 Thymeleaf 대신 Mustache를 사용한다.</div>

<br>

이제 <span style="color:orange; font-weight:bold">build.gradle</span>를 열고 수정을 해야 한다. 우리는 일단 책에서 나온 대로 JUnit4를 쓰고 repository를 <span style="color:orange; font-weight:bold">mavenCentral</span>와 <span style="color:orange; font-weight:bold">jcenter</span>를 사용한다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

이전부터 mavenCentral을 많이 사용해 왔지만 본인이 만든 라이브러리를 업로드하기 위해서는 정말 많은 과정과 설정이 필요하다. 그러다 보니 개발자들이 직접 만든 라이브러리를 업로드하는 것이 힘들어 점점 공유가 안 되는 상황이 발생했다. 최근에 나온 jcenter는 이런 문제점을 개선하여 라이브러리 업로드를 간단하게 하였다. 또한 여기서 한 걸음 더 나아가 jcenter에 라이브러리를 업로드하면 mavenCentral에도 업로드될 수 있도록 자동화를 할 수 있다. 그러다 보니 개발자들의 라이브러리가 점점 jcenter로 이동하고 있다. 여기서는 mavenCentral, jcenter 둘 다 등록해서 사용한다. </div>

라고 나와있으나.. jcenter는 현재 <span style="color:#85144b; font-weight:bold">deprecated</span>라고 나온다. 책에서는 둘 다 쓰지만 여기서는 <span style="color:orange; font-weight:bold">mavenCentral</span>만 쓰겠다.

<br>

완성 된 **build.gradle**를 보자.

**build.gradle**

```gradle
plugins {
    id 'org.springframework.boot' version '2.5.3'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
    id 'war'
}

group = 'com.yyk.app'
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
    //implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    // 'org.springframework.boot:spring-boot-starter-security'
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    //implementation 'org.thymeleaf.extras:thymeleaf-extras-springsecurity5'
    implementation 'junit:junit:4.12'
    compileOnly 'org.projectlombok:lombok'
    developmentOnly 'org.springframework.boot:spring-boot-devtools'
    annotationProcessor 'org.projectlombok:lombok'
    providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
   // testImplementation 'org.springframework.security:spring-security-test'
}

test {
    useJUnitPlatform()
}


```

<br>

<div class="webnots-warning webnots-notification-box">implementation 'org.springframework.boot:spring-boot-starter-data-jpa' 는 지금은 주석처리를 해 놓는다. 하지 않고 앱을 실행할 경우 에러가 발생한다. 추후에 사용할 예정이다.</div>
<div class="webnots-warning webnots-notification-box">spring security 부분도 마찬가지로 주석 처리를 해놓는다. 나중에 사용한다. 이를 하지 않을 경우 앱을 실행하고 브라우저로 앱을 접속하게 되면 login를 하라는 창이 나온다.</div>

그리고 깃허브랑 연동을 하기 위해서 윈도우일 경우 <span style="color:#7EDBFF; font-weight:bold">[Ctrl+shift+A]</span> 맥일 경우 <span style="color:#7EDBFF; font-weight:bold">[Command+Shift+A]</span>를 사용해 Action 검색창을 열어 <span style="color:orange; font-weight:bold">share project on github</span>을 검색한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-22-49.png){: p}

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-24-13.png){: p}

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-1/2021-08-13-16-24-37.png){: p}

<br>

위 사진에서 **Add**를 클릭한다.

<br>

자 이제 불필요한 파일이 올라가는 것을 방지하기 위해서 **.gitignore**를 구성해야 한다.

<br>

**.gitignore**

```github
HELP.md
.gradle
build/
!gradle/wrapper/gradle-wrapper.jar
!**/src/main/**/build/
!**/src/test/**/build/

### STS ###
.apt_generated
.classpath
.factorypath
.project
.settings
.springBeans
.sts4-cache
bin/
!**/src/main/**/bin/
!**/src/test/**/bin/

### IntelliJ IDEA ###
.idea
*.iws
*.iml
*.ipr
out/
!**/src/main/**/out/
!**/src/test/**/out/

### NetBeans ###
/nbproject/private/
/nbbuild/
/dist/
/nbdist/
/.nb-gradle/

### VS Code ###
.vscode/

```

<br>

위는 그냥 디폴트로 작성이 되어 있는 그대로 나둔다. 중요한 것은

- .gradle<br>
- .idea<br>

<br>

이 되어 있는지만 체크한다.

<br>

이제 본격적으로 개발할 수 있는 프로젝트를 만든 것이다.
