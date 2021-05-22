---
layout: post
title: 스프링부트에서 타임리프 Template 경로 바꾸기-2
date: 2021-05-16 10:00:00 0000
tags: [Intellij, SpringBoot, Thymeleaf]
categories: [SpringBoot]
description: Changing the Thymeleaf Template Directory in SpringBoot
---

<br><br>

# <center>Template 경로 변경하기-2</center>

<br>

스프링부트에서 타임리프의 정적 리소스 경로를 바꾸는 문서에 대한 링크는 아래에 달아놓겠다.

**[SpringBoot Document](https://www.baeldung.com/spring-thymeleaf-template-directory)**

<br>

지금부터 여기 문서에 적혀 있는 내용을 번역을 해볼까 한다. 발번역이여도 이해해주길 바란다...

## 소개

Thymeleaf는 스프링부트 어플리케이션에 사용할 수 있는 템플릿 엔진이다. 많은 것들과 함께 스프링부트는 우리의 templates(정적리소스)를 찾기 위한 디폴트 경로를 제공한다. 이번 짦은 튜토리얼에서는 우리는 tempate 경로를 어떻게 바꿀 수 있는지 알아볼 것이다. 그런 다음 우리는 다중 경로를 바꾸는 방법도 배울 것이다.

## 구성

타임리프를 쓰기 위해서는 pom.xml에 적절한 Spring Boot starter를 추가 해줘야 한다.

**pom.xml일 경우**

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
    <versionId>2.2.2.RELEASE</versionId>
</dependency>
```

<br>

**build.gradle일 경우**

```
dependencies {
    (...)
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
}
```

<br>

## 디폴트 경로 바꾸기

스프링부트는 디폴트로 **src/main/resources/templates**를 탐색하게 된다. 우리는 우리의 templates를 거기에 놓고 그 하위 폴더에서 구성(정적 리소스들:html, css, js등)하게 되면 아무 문제없이 할 수 있다.

이제 한번 templates이 **src/main/resources/templates** 아래가 아닌 **src/main/resources/tempates-2** 아래 구성되어야 하는 요구사항이 있다고 해보자.

실제로 한번 **src/main/resources/templates-2** 아래 html 파일 하나를 생성해보자.

**src/main/resouces/templates-2 아래 html 파일 내용**

**hello.html**

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <meta charset="UTF-8" />
    <title>Enums in Thymeleaf</title>
  </head>
  <body>
    <h2>Hello from 'templates/templates-2'</h2>
  </body>
</html>
```

<br>

그리고 controller도 필요할 것이다.

**HelloController.java**

```java
@GetMapping("/hello")
public String sayHello() {
    return "hello";
}
```

<br>

위와 같은 간단한 구성으로 application.properties 내에 아래 코드와 같이 설정함으로써 스프링부트가 **templates-2** 디렉토리를 사용하게끔 만든다.

**application.properties**

```
spring.thymeleaf.prefix=classpath:/templates-2/
```

<br>

## 다중 경로 사용하기

이제 우리는 디폴트 경로를 바꾸는 방법을 배웠다. 이제 다중 template 경로를 바꾸는 법에 대해서 알아보자. 이것을 하기 위해선 **ClassLoaderTemplateResolver bean**를 만들어야 된다.

```java
@Bean
public ClassLoaderTemplateResolver secondaryTemplateResolver() {
    ClassLoaderTemplateResolver secondaryTemplateResolver = new ClassLoaderTemplateResolver();
    secondaryTemplateResolver.setPrefix("templates-2/");
    secondaryTemplateResolver.setSuffix(".html");
    secondaryTemplateResolver.setTemplateMode(TemplateMode.HTML);
    secondaryTemplateResolver.setCharacterEncoding("UTF-8");
    secondaryTemplateResolver.setOrder(1);
    secondaryTemplateResolver.setCheckExistence(true);

    return secondaryTemplateResolver;
}
```

<br>

우리 커스텀 빈에서 우리는 prefix를 두 번째 디렉토리인 **templates-2**로 설정했다. 그리고 또한 **CheckExistance flag**를 **true**로 설정했다. 이것은 리졸버가 연쇄적으로 작동하게끔 만드는 열쇄이다. 이런 식의 설정은 우리가 templates를 디폴트 템플릿인 **main/resources/templates** 디렉토리와 두 번째 템플릿 경로인 **main/resources/templates-2**를 사용할 수 있게끔 해준다.

## 에러

Thymeleaf를 사용할 때 이런 에러를 볼 수 있다.

```
Error resolving template [hello], template might not exist or might not be accessible
by any of the configured Template Resolvers
```

<br>

이런 메시지는 타임리프가 template 경로를 찾을 수 없기 때문에 보는 메시지이다. 가능성 있는 이유들과 해결책들을 살펴보자.

### Controller 내 타이핑 에러

간단한 타이핑 에러로서 발생할 수도 있다. 가장 먼저 확인해야 할 것은 파일 이름에서 확장자를 뺀 파일 이름과 컨트롤러에서 요청하는 템플릿이 정확히 일치하는 것이다. 하위 디렉터리를 사용하는 경우 해당 디렉터리도 올바른지 확인해야합니다.

<br>

추가적으로 그 문제는 특정 운영 체제의 문제일 수 있다. Windows는 대소 문자를 구분하지 않지만 다른 운영 체제는 구분합니다. 예를 들어 로컬 Windows 시스템에서 제대로 작동하는데 배포할 시에 제대로 작동하지 않으면 살펴볼 필요가 있습니다.

### 컨트롤러에서 파일 확장자를 포함시키는 경우

우리의 파일이 전형적으로 확장자가 있기 때문에 controller에서 그것을 포함시켜서 template path로 리턴하는 것이 자연스러워 보일 수 있다. **타임리프는 자동으로 suffix(여기선 확장자)를 추가하기 때문에 확장자를 포함시키면 안 된다.**

### 디폴트 경로를 사용하지 않는 경우

만약 경로가 **src/main/resources/templates**가 아닌 다른 곳에 파일이 위치되어 있다면 이 에러가 발생할 수 있다. 만약 다른 경로를 사용하고 싶다면 **spring.thymeleaf.prefix** 속성을 세팅하거나 우리만의 **ClassLoaderTemplateResolver bean**를 만들어서 다중 경로를 사용할 수 있게끔 해야한다.

## 결론

이번 튜토리얼에서 우리는 타임리프 템플릿 경로에 대해서 배웠다. 먼저 우리는 디폴트 경로를 속성에서 설정해줌으로써 바꾸는 법을 배웠다. 그리고 우리 자신만의 **ClassLoaderTemplateResolver bean**를 만들어서 다중 경로를 사용하는 법에 대해서도 익혔다.

그리고 타임리프가 template경로를 찾지 못할 경우 나오는 에러와 해결방법에 대해서도 이야기 해봤다.

이 예제 코드는 항상 **[GitHub](https://github.com/eugenp/tutorials/tree/master/spring-web-modules/spring-thymeleaf-2)**에서 찾을 수 있다.
