---
layout: post
title: Spring WebFlux
date: 2021-12-26 10:00:00 0000
tags: [Spring WebFlux]
categories: [Interview]
description: Spring WebFlux 등장 배경 및 간단한 예제
---

<br><br>

_**오늘의 나보다 성장한 내일의 나를 위해...**_

<br>

<br><br>

<style>
.containercoffee {
  width: 300px;
  height: 280px;
  position: relative;
  top: calc(50% - 140px);
  left: calc(50% - 150px);
}
.coffee-header {
  width: 100%;
  height: 80px;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #ddcfcc;
  border-radius: 10px;
}
.coffee-header__buttons {
  width: 25px;
  height: 25px;
  position: absolute;
  top: 25px;
  background-color: #282323;
  border-radius: 50%;
}
.coffee-header__buttons::after {
  content: "";
  width: 8px;
  height: 8px;
  position: absolute;
  bottom: -8px;
  left: calc(50% - 4px);
  background-color: #615e5e;
}
.coffee-header__button-one {
  left: 15px;
}
.coffee-header__button-two {
  left: 50px;
}
.coffee-header__display {
  width: 50px;
  height: 50px;
  position: absolute;
  top: calc(50% - 25px);
  left: calc(50% - 25px);
  border-radius: 50%;
  background-color: #9acfc5;
  border: 5px solid #43beae;
  box-sizing: border-box;
}
.coffee-header__details {
  width: 8px;
  height: 20px;
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #9b9091;
  box-shadow: -12px 0 0 #9b9091, -24px 0 0 #9b9091;
}
.coffee-medium {
  width: 90%;
  height: 160px;
  position: absolute;
  top: 80px;
  left: calc(50% - 45%);
  background-color: #bcb0af;
}
.coffee-medium:before {
  content: "";
  width: 90%;
  height: 100px;
  background-color: #776f6e;
  position: absolute;
  bottom: 0;
  left: calc(50% - 45%);
  border-radius: 20px 20px 0 0;
}
.coffe-medium__exit {
  width: 60px;
  height: 20px;
  position: absolute;
  top: 0;
  left: calc(50% - 30px);
  background-color: #231f20;
}
.coffe-medium__exit::before {
  content: "";
  width: 50px;
  height: 20px;
  border-radius: 0 0 50% 50%;
  position: absolute;
  bottom: -20px;
  left: calc(50% - 25px);
  background-color: #231f20;
}
.coffe-medium__exit::after {
  content: "";
  width: 10px;
  height: 10px;
  position: absolute;
  bottom: -30px;
  left: calc(50% - 5px);
  background-color: #231f20;
}
.coffee-medium__arm {
  width: 70px;
  height: 20px;
  position: absolute;
  top: 15px;
  right: 25px;
  background-color: #231f20;
}
.coffee-medium__arm::before {
  content: "";
  width: 15px;
  height: 5px;
  position: absolute;
  top: 7px;
  left: -15px;
  background-color: #9e9495;
}
.coffee-medium__cup {
  width: 80px;
  height: 47px;
  position: absolute;
  bottom: 0;
  left: calc(50% - 40px);
  background-color: #FFF;
  border-radius: 0 0 70px 70px / 0 0 110px 110px;
}
.coffee-medium__cup::after {
  content: "";
  width: 20px;
  height: 20px;
  position: absolute;
  top: 6px;
  right: -13px;
  border: 5px solid #FFF;
  border-radius: 50%;
}
@keyframes liquid {
  0% {
    height: 0px;  
    opacity: 1;
  }
  5% {
    height: 0px;  
    opacity: 1;
  }
  20% {
    height: 62px;  
    opacity: 1;
  }
  95% {
    height: 62px;
    opacity: 1;
  }
  100% {
    height: 62px;
    opacity: 0;
  }
}
.coffee-medium__liquid {
  width: 6px;
  height: 63px;
  opacity: 0;
  position: absolute;
  top: 50px;
  left: calc(50% - 3px);
  background-color: #74372b;
  animation: liquid 4s 4s linear infinite;
}
.coffee-medium__smoke {
  width: 8px;
  height: 20px;
  position: absolute;  
  border-radius: 5px;
  background-color: #b3aeae;
}
@keyframes smokeOne {
  0% {
    bottom: 20px;
    opacity: 0;
  }
  40% {
    bottom: 50px;
    opacity: .5;
  }
  80% {
    bottom: 80px;
    opacity: .3;
  }
  100% {
    bottom: 80px;
    opacity: 0;
  }
}
@keyframes smokeTwo {
  0% {
    bottom: 40px;
    opacity: 0;
  }
  40% {
    bottom: 70px;
    opacity: .5;
  }
  80% {
    bottom: 80px;
    opacity: .3;
  }
  100% {
    bottom: 80px;
    opacity: 0;
  }
}
.coffee-medium__smoke-one {
  opacity: 0;
  bottom: 50px;
  left: 102px;
  animation: smokeOne 3s 4s linear infinite;
}
.coffee-medium__smoke-two {
  opacity: 0;
  bottom: 70px;
  left: 118px;
  animation: smokeTwo 3s 5s linear infinite;
}
.coffee-medium__smoke-three {
  opacity: 0;
  bottom: 65px;
  right: 118px;
  animation: smokeTwo 3s 6s linear infinite;
}
.coffee-medium__smoke-for {
  opacity: 0;
  bottom: 50px;
  right: 102px;
  animation: smokeOne 3s 5s linear infinite;
}
.coffee-footer {
  width: 95%;
  height: 15px;
  position: absolute;
  bottom: 25px;
  left: calc(50% - 47.5%);
  background-color: #41bdad;
  border-radius: 10px;
}
.coffee-footer::after {
  content: "";
  width: 106%;
  height: 26px;
  position: absolute;
  bottom: -25px;
  left: -8px;
  background-color: #000;
}
</style>

<div class="containercoffee">
    <div class="coffee-header">
      <div class="coffee-header__buttons coffee-header__button-one"></div>
      <div class="coffee-header__buttons coffee-header__button-two"></div>
      <div class="coffee-header__display"></div>
      <div class="coffee-header__details"></div>
    </div>
    <div class="coffee-medium">
      <div class="coffe-medium__exit"></div>
      <div class="coffee-medium__arm"></div>
      <div class="coffee-medium__liquid"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-one"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-two"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-three"></div>
      <div class="coffee-medium__smoke coffee-medium__smoke-for"></div>
      <div class="coffee-medium__cup"></div>
    </div>
    <div class="coffee-footer"></div>
</div>

<br><br><br><br><br><br><br><br>

<br>

### Spring WebFlux

<br>

우리가 보통 사용하던 Spring MVC + RDBMS 패턴은 <span style="color:#2ECC40; font-weight:bold">Blocking IO</span> 방식이다.

<span style="color:#2ECC40; font-weight:bold">Blocking IO</span> 방식이라는 것은 요청을 처리하기 전까지는 다른 작업을 수행할 수 없는 상태라는 것을 말한다.

동시에 여러 요청을 처리하기 위해서는 <span style="color:#2ECC40; font-weight:bold">Thread</span> 수를 늘려서 하는 방법이 존재하기는 하지만 오버헤드가 발생한다.

이를 개선하기 위해서 나온 기술이 <span style="color: rgba(131, 24, 67); font-weight:bold">Non-Blocking IO</span> 방식인 <span style="color: rgba(131, 24, 67); font-weight:bold">Spring WebFlux</span>이다.

<span style="color: rgba(131, 24, 67); font-weight:bold">Spring WebFlux</span>는 동시에 처리되어야 할 많은 요청에 대해 효율적으로 처리해줄 수 있다.

<br>

스레드 풀을 이용한 동기식 호출 방식은 코드가 간단하고 순차적으로 동작하기 때문에 개발자가 코드를 직관적이고 빠르게 작성할 수 있다.

하지만 이렇게 작성한 코드로 만든 서버도 빠르게 동작하고 많은 요청을 처리할 수 있을까?

동기식 호출 방식에서는 상대편의 응답이 올 때까지 스레드는 기다려야(blocking)한다.

응답이 빨리 오면 그 기다림은 길지 않겠지만 만약 응답이 늦게 오면 서버가 요청에 대한 응답을 기다리는 데 스레드를 모두 소진해서 추가 요청을 처리할 수 없는 상태가 될 수 있다.

특히 MSA에서는 타임아웃이 발생할 정도의 지연이 발생하면 순식간에 다른 모듈로 전파되어 전체 시스템이 마비되는 등의 악영향을 끼칠 수 있다.

<br>

여기서 의문점이 생긴다.

쓰레드가 서버로 요청을 하고 나서 꼭 응답을 기다리면서 아무 것도 하지 않고 대기해야 할까?

쓰레드가 응답을 기다리지 않고 다른 일을 처리하다가 응답이 왔을 때 해당 일을 처리한다면 응답만 기다리면서 불필요하게 리소스를 점유하는 일은 없을 것이다.

이러한 요구 사항에서 나온 것이 이벤트 루프를 이용한 <span style="color:#2ECC40; font-weight:bold">비동기 프로그래밍</span>이다.

<br>

이벤트 루프를 활용하면 요청을 보내고 응답이 올 때까지 무작정 기다리는 대신 자신에게 할당된 다른 여러 소켓의 요청을 순차적으로 빠르게 처리한다.

이제 우리의 서버와 클라이언트의 스레드는 더이상 blocking되지 않는다.

Spring 생태계에서도 버전 5부터 도입된 WebFlux를 통해 비동기 프로그래밍을 본격적으로 도입하고 있다.

<br>

물론 단점도 있다.

순차적으로 처리되는 방식이 아니라 디버깅이 힘들고 개발이 어렵다.

즉 SI에서 사용하기는 좀 힘든 부분이 있다.

<br>

#### Example

<br>

아래 예제는 **Spring.io**에 있는 간단한 <span style="color:#85144b; font-weight:bold">Reactive RESTful Web Service</span>이다.

**[원문 링크](https://spring.io/guides/gs/reactive-rest-service/)**

<br>

원문을 하나하나 해석해 보자.

<br>

#### 목적

<br>

이제부터 우리는 Spring WebFlux를 이용하여 RESTful web service와 service의 WebClient consumer를 만들게 될 것이다.

우리는 아래로 요청했을 때의 **System.out**의 출력 값을 확인할 수 있다.

```url
http://localhost:8080/hello
```

<br>

#### 시작 전 필요한 것들

<br>

- 15분 정도의 시간

<br>

- 좋은 텍스트 에디터 아니면 IDE

<br>

- JDK 1.8 이상

<br>

- Gradle 4+ 아니면 Maven 3.2+

<br>

- 코드를 IDE로 바로 가져올 수도 있음
  - **[Spring Tool Suite (STS)](https://spring.io/guides/gs/sts/)**
  - **[IntelliJ IDEA](https://spring.io/guides/gs/intellij-idea/)**

<br>

**pom.xml**

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
  </dependency>

  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
  </dependency>
  <dependency>
    <groupId>io.projectreactor</groupId>
    <artifactId>reactor-test</artifactId>
    <scope>test</scope>
  </dependency>
</dependencies>

```

<br>

이중 pom.xml 을 열어보면 이렇게 spring-boot-starter-webflux dependency를 가지고 있는것을 확인할 수 있다.

이번엔 hello package 내의 클래스를 하나씩 보면서 어떤 방식으로 동작하는지 알아보자.

<br>

**Handler**

```java
package hello;

import org.springframework.http.MediaType;
import org.springframework.stereotype.Component;
import org.springframework.web.reactive.function.BodyInserters;
import org.springframework.web.reactive.function.server.ServerRequest;

import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.core.publisher.Mono;

@Component
public class GreetingHandler {

    public Mono<ServerResponse> hello(ServerRequest request) {

        return ServerResponse.ok().contentType(MediaType.TEXT_PLAIN)
                .body(BodyInserters.fromValue("Hello, Spring!"));
    }
}
```

<br>

Spring Reactive 접근 방식에서는 Handler를 사용하여 요청을 처리하고 응답을 생성한다. 이 예제에서는 요청에 대해 "Hello, Spring!"을 반환하는 역할을 해주고 있다. 여기서 Mono라는 객체가 나오는데 이것은 Reactor에서 결과값을 처리하기 위한 객체라고 이해하면 된다. 주로 0개~1개의 결과값은 Mono에 담고 Flux 객체는 Mono와 유사한데 0개~n개의 결과값을 처리하는 객체이다.

<br>

**Router**

```java
package hello;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.MediaType;
import org.springframework.web.reactive.function.server.RequestPredicates;
import org.springframework.web.reactive.function.server.RouterFunction;
import org.springframework.web.reactive.function.server.RouterFunctions;
import org.springframework.web.reactive.function.server.ServerResponse;
@Configuration
public class GreetingRouter {
    @Bean
    public RouterFunction<ServerResponse> route(GreetingHandler greetingHandler) {
        return RouterFunctions
                .route(RequestPredicates.GET("/hello").and(RequestPredicates.accept(MediaType.TEXT_PLAIN)), greetingHandler::hello);
    }
}
```

<br>

Spring MVC의 Controller의 역할 중 RequestMapping의 역할을 하는 녀석이 Router라고 생각하면 이해가 빠를것 같다. 예제에서는 /hello 라는 요청을 greetingHandler::hello 에 매핑을 시켜주고 있다.

<br>

**WebClient**

```java
package hello;
import org.springframework.http.MediaType;
import org.springframework.web.reactive.function.client.ClientResponse;
import org.springframework.web.reactive.function.client.WebClient;
import reactor.core.publisher.Mono;
public class GreetingWebClient {
    private WebClient client = WebClient.create("http://localhost:8080");
    private Mono<ClientResponse> result = client.get()
            .uri("/hello")
            .accept(MediaType.TEXT_PLAIN)
            .exchange();
    public String getResult() {
        return ">> result = " + result.flatMap(res -> res.bodyToMono(String.class)).block();
    }
}

```

<br>

WebClient는 외부와 통신을 하는 창구 역할을 한다고 보면 된다.

기존에는 RestTemplate을 이용해서 HTTP 통신을 했지만 이것은 Blocking IO 방식이다. 그래서 Non-Blocking IO 방식과 비동기 방식을 지원하기 위한 WebClient 를 만들었고 WebFlux에서는 이것을 써야 한다.

가장 간단한 예제라 create()를 통해서 WebClient를 생성했지만 다른 옵션들을 더 추가하려면 build() 를 써야 한다.

<br>

**Aplication.java**

```java
package hello;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
        GreetingWebClient gwc = new GreetingWebClient();
        System.out.println(gwc.getResult());
    }
}

```

<br>

![](/images/Interview/post14/2021-12-26-12-16-37.png?style=centerme)

<br>

서버는 tomcat 이 아닌 embedded Netty 를 사용한다. Application.java 에서 WebClient에서 result를 가지고 오라고 되어 있어서 구동할때도 result = Hello, Spring! 을 출력해준다. 또한 http://localhost:8080/hello 를 입력하면 result 인 Hello, Spring! 가 출력되는 것을 볼수 있다.
