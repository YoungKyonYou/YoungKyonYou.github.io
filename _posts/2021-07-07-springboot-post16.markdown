---
layout: post
title: Springboot Intellij에서 Livereload 사용하기
date: 2021-07-07 12:00:00 0000
tags:
  [
    Intellij,
    DevTools,
    Springboot,
    Livereload,
    Chrome-Extension,
    Spring Document,
  ]
categories: [SpringBoot]
description: 스프링부트 실행 후 정적 리소스 변경 시 자동으로 업데이트하게 하는 법
---

<br><br>

# <center>Live Reload 사용하는 방법</center>

<br>

이 기능을 좀 더 빨리 알았더라면 시간을 많이 벌었을 것이다.

졸업작품을 스프링부트로 하고 있는데 프론트엔드를 설계하고 만드는 과정에서 매번 앱을 껐다 켰다를 반복했기 때문이다.

<br>

앱을 껐다가 키는데 걸리는 시간이 좀 걸리므로 그 방법은 추천하지 않는다...

<br>

그래서 Live Reload라는 기능을 알게 되었는데 이것은 스프링 부트 앱이 실행된 상태에서 정적 리소스에 변경이 발생한 경우 앱을 껐다가 다시 키지 않고서도 바로 업데이트를 확인할 수 있는 것이다.

<br>

사실 구글에다가 검색하면 관련 글이 많이 나오지만 아주 중요한 것을 알려주지 않아서 이렇게 글을 쓰게 됐다.

일단 거의 공통적으로 알려주는 것을 설정해보자.

---

> **1. build.gradle 설정**<br>

```dependencies
dependencies {
    compile("org.springframework.boot:spring-boot-devtools")
}
```

<br>

> **2. aplication.properties 설정**<br>

```application.properties
spring.devtools.livereload.enabled=true
```

> **3. Settings->Build->Compiler**<br>

**Build project automatically에 Check한다**

<br>

![](/images/SpringBoot/post16/2021-07-07-16-27-04.png)

<br>

> **4. Settings->Build,Execution,Deployment->Build Tools->Gradle**<br>

**Build and run using을 Gradle에서 Intellij IDEA로 변경**

<br>

![](/images/SpringBoot/post16/2021-07-07-16-28-29.png)

<br>

> **5. 크롬 사용시 크롬 확장프로그램 'LiveReload' 다운로드 받기**<br>

<br>

![](/images/SpringBoot/post16/2021-07-07-16-31-48.png)

<br>

> **6. ctrl+shift+a를 눌러서 검색 창에 Registry 입력하고 들어간다**

<br>

![](/images/SpringBoot/post16/2021-07-07-17-05-19.png)

<br>

**compiler.automake.allow.when.app.running에 체크한다.**

<br>

![](/images/SpringBoot/post16/2021-07-07-17-06-23.png)

<br>

이렇게 모든 설정이 끝났다. 이제부터 앱을 실행하고 정적 리소스를 변경하고나서 크롬에서 **F5(새로고침)**를 하면 업데이트가 될 것이다.
