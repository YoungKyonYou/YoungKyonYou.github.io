---
layout: post
title: WSL에서 Spring Cloug Config Server를 Docker 배포 중 Git 내용을 못 가지고 오는 문제
date: 2022-01-28 13:00:00 0000
tags: [Kubernetes, grafana]
categories: [Kubernetes]
description: cannot open git-upload-pack
---

<br><br>

<br><br>
_**커피 중독자되는 중...**_
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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> WSL Ubuntu 20.04 버전에서 Spring Cloud Config Server를 Docker로 구축하던 중 Git 내용을 못 가지고 오는 에러
</h2>

<br>

최근에 듣게 된 inflear 강의가 하나 있다.

바로 <span style="background: rgb(251,243,219)">이도원 강사</span>님의 <span style="background: rgb(251,243,219)">Spring Cloud로 개발하는 마이크로서비스 애플리케이션(MSA)</span>이다.

<br>

Spring MSA 관련해서 많은 내용을 다루고 실습도 알차서 매우 좋은 강의이다.

마지막 챕터를 향해 달려가던 중 문제가 생겼다. 로컬에서 잘 작동되던 config-server가 제대로 작동하지 않았다. 

어떤 에러인지는 내가 직접 inflear에 질문을 하고 직접 답변을 한 링크를 달겠다.

**[Inflear 질문 링크](https://www.inflearn.com/questions/418419)**

<br>

```bash
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.6.2)

2022-01-27 05:40:46.884  INFO 1 --- [           main] c.e.c.ConfigServiceApplication           : The following profiles are active: default
2022-01-27 05:40:48.525  INFO 1 --- [           main] faultConfiguringBeanFactoryPostProcessor : No bean named 'errorChannel' has been explicitly defined. Therefore, a default PublishSubscribeChannel will be created.
2022-01-27 05:40:48.564  INFO 1 --- [           main] faultConfiguringBeanFactoryPostProcessor : No bean named 'integrationHeaderChannelRegistry' has been explicitly defined. Therefore, a default DefaultHeaderChannelRegistry will be created.
2022-01-27 05:40:48.768  INFO 1 --- [           main] o.s.cloud.context.scope.GenericScope     : BeanFactory id=2d1905bd-ddb1-3c02-8186-79b2dca87272
2022-01-27 05:40:48.887  INFO 1 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-27 05:40:48.896  INFO 1 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'bindersHealthContributor' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration$BindersHealthContributor] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-27 05:40:48.899  INFO 1 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'bindersHealthIndicatorListener' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration$BindersHealthIndicatorListener] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-27 05:40:48.915  INFO 1 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.integration.config.IntegrationManagementConfiguration' of type [org.springframework.integration.config.IntegrationManagementConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-27 05:40:48.928  INFO 1 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'integrationChannelResolver' of type [org.springframework.integration.support.channel.BeanFactoryChannelResolver] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-27 05:40:49.360  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8889 (http)
2022-01-27 05:40:49.391  INFO 1 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2022-01-27 05:40:49.391  INFO 1 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.56]
2022-01-27 05:40:49.479  INFO 1 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2022-01-27 05:40:49.479  INFO 1 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 2551 ms
2022-01-27 05:40:51.740  INFO 1 --- [           main] o.s.c.s.m.DirectWithAttributesChannel    : Channel 'application-1.springCloudBusInput' has 1 subscriber(s).
2022-01-27 05:40:52.579  INFO 1 --- [           main] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 1 endpoint(s) beneath base path '/actuator'
2022-01-27 05:40:52.753  INFO 1 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : Adding {logging-channel-adapter:_org.springframework.integration.errorLogger} as a subscriber to the 'errorChannel' channel
2022-01-27 05:40:52.753  INFO 1 --- [           main] o.s.i.channel.PublishSubscribeChannel    : Channel 'application-1.errorChannel' has 1 subscriber(s).
2022-01-27 05:40:52.755  INFO 1 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : started bean '_org.springframework.integration.errorLogger'
2022-01-27 05:40:52.757  INFO 1 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Creating binder: rabbit
2022-01-27 05:40:52.941  INFO 1 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Caching the binder: rabbit
2022-01-27 05:40:52.942  INFO 1 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Retrieving cached binder: rabbit
2022-01-27 05:40:53.035  INFO 1 --- [           main] c.s.b.r.p.RabbitExchangeQueueProvisioner : declaring queue for inbound: springCloudBus.anonymous.dVyf_-Z1QfO2gWPEnaJ2Bg, bound to: springCloudBus
2022-01-27 05:40:53.043  INFO 1 --- [           main] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [rabbitmq:5672]
2022-01-27 05:40:53.167  INFO 1 --- [           main] o.s.a.r.c.CachingConnectionFactory       : Created new connection: rabbitConnectionFactory#125c082e:0/SimpleConnection@43034809 [delegate=amqp://guest@172.18.0.2:5672/, localPort= 45018]
2022-01-27 05:40:53.267  INFO 1 --- [           main] o.s.c.stream.binder.BinderErrorChannel   : Channel 'springCloudBus.anonymous.dVyf_-Z1QfO2gWPEnaJ2Bg.errors' has 1 subscriber(s).
2022-01-27 05:40:53.269  INFO 1 --- [           main] o.s.c.stream.binder.BinderErrorChannel   : Channel 'springCloudBus.anonymous.dVyf_-Z1QfO2gWPEnaJ2Bg.errors' has 2 subscriber(s).
2022-01-27 05:40:53.298  INFO 1 --- [           main] o.s.i.a.i.AmqpInboundChannelAdapter      : started bean 'inbound.springCloudBus.anonymous.dVyf_-Z1QfO2gWPEnaJ2Bg'
2022-01-27 05:40:53.321  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8889 (http) with context path ''
2022-01-27 05:40:53.369  INFO 1 --- [           main] c.e.c.ConfigServiceApplication           : Started ConfigServiceApplication in 7.994 seconds (JVM running for 8.791)
2022-01-27 05:41:01.962  INFO 1 --- [nio-8889-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2022-01-27 05:41:01.963  INFO 1 --- [nio-8889-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2022-01-27 05:41:01.967  INFO 1 --- [nio-8889-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 4 ms
2022-01-27 05:41:05.532  WARN 1 --- [nio-8889-exec-1] .c.s.e.MultipleJGitEnvironmentRepository : Error occured cloning to base directory.

org.eclipse.jgit.api.errors.TransportException: https://github.com/YoungKyonYou/spring-cloud-config: cannot open git-upload-pack
        at org.eclipse.jgit.api.FetchCommand.call(FetchCommand.java:224) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.CloneCommand.fetch(CloneCommand.java:303) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.CloneCommand.call(CloneCommand.java:178) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.cloneToBasedir(JGitEnvironmentRepository.java:658) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.copyRepository(JGitEnvironmentRepository.java:633) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.createGitClient(JGitEnvironmentRepository.java:616) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.refresh(JGitEnvironmentRepository.java:296) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.getLocations(JGitEnvironmentRepository.java:262) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.getLocations(MultipleJGitEnvironmentRepository.java:139) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.AbstractScmEnvironmentRepository.findOne(AbstractScmEnvironmentRepository.java:55) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.findOneFromCandidate(MultipleJGitEnvironmentRepository.java:188) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.findOne(MultipleJGitEnvironmentRepository.java:173) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.CompositeEnvironmentRepository.findOne(CompositeEnvironmentRepository.java:64) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentEncryptorEnvironmentRepository.findOne(EnvironmentEncryptorEnvironmentRepository.java:61) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentController.getEnvironment(EnvironmentController.java:132) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentController.defaultLabel(EnvironmentController.java:109) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:78) ~[na:na]
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:566) ~[na:na]
        at org.springframework.util.ReflectionUtils.invokeMethod(ReflectionUtils.java:282) ~[spring-core-5.3.14.jar!/:5.3.14]
        at org.springframework.cloud.context.scope.GenericScope$LockedScopedProxyFactoryBean.invoke(GenericScope.java:485) ~[spring-cloud-context-3.1.0.jar!/:3.1.0]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:753) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:698) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.cloud.config.server.environment.EnvironmentController$$EnhancerBySpringCGLIB$$60d7694f.defaultLabel(<generated>) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:78) ~[na:na]
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:566) ~[na:na]
        at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:205) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:150) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:117) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:895) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:808) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1067) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:963) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:898) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:655) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:764) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:227) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53) ~[tomcat-embed-websocket-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.boot.actuate.metrics.web.servlet.WebMvcMetricsFilter.doFilterInternal(WebMvcMetricsFilter.java:96) ~[spring-boot-actuator-2.6.2.jar!/:2.6.2]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:197) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:97) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:540) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:135) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:78) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:357) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:382) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:895) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1732) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1191) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:659) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at java.base/java.lang.Thread.run(Thread.java:831) ~[na:na]
Caused by: org.eclipse.jgit.errors.TransportException: https://github.com/YoungKyonYou/spring-cloud-config: cannot open git-upload-pack
        at org.eclipse.jgit.transport.TransportHttp.connect(TransportHttp.java:749) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.TransportHttp.openFetch(TransportHttp.java:465) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.FetchProcess.executeImp(FetchProcess.java:142) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.FetchProcess.execute(FetchProcess.java:94) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.Transport.fetch(Transport.java:1309) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.FetchCommand.call(FetchCommand.java:213) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        ... 79 common frames omitted
Caused by: java.net.UnknownHostException: github.com: Temporary failure in name resolution
        at java.base/java.net.Inet4AddressImpl.lookupAllHostAddr(Native Method) ~[na:na]
        at java.base/java.net.InetAddress$PlatformNameService.lookupAllHostAddr(InetAddress.java:932) ~[na:na]
        at java.base/java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1517) ~[na:na]
        at java.base/java.net.InetAddress$NameServiceAddresses.get(InetAddress.java:851) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName0(InetAddress.java:1507) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName(InetAddress.java:1366) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName(InetAddress.java:1300) ~[na:na]
        at org.apache.http.impl.conn.SystemDefaultDnsResolver.resolve(SystemDefaultDnsResolver.java:45) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.conn.DefaultHttpClientConnectionOperator.connect(DefaultHttpClientConnectionOperator.java:112) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.conn.PoolingHttpClientConnectionManager.connect(PoolingHttpClientConnectionManager.java:376) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.MainClientExec.establishRoute(MainClientExec.java:393) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.MainClientExec.execute(MainClientExec.java:236) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.ProtocolExec.execute(ProtocolExec.java:186) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.RetryExec.execute(RetryExec.java:89) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.RedirectExec.execute(RedirectExec.java:110) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.InternalHttpClient.doExecute(InternalHttpClient.java:185) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:83) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:108) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:56) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.eclipse.jgit.transport.http.apache.HttpClientConnection.execute(HttpClientConnection.java:274) ~[org.eclipse.jgit.http.apache-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.http.apache.HttpClientConnection.getResponseCode(HttpClientConnection.java:251) ~[org.eclipse.jgit.http.apache-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.util.HttpSupport.response(HttpSupport.java:205) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.TransportHttp.connect(TransportHttp.java:654) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        ... 84 common frames omitted

2022-01-27 05:41:05.541  WARN 1 --- [nio-8889-exec-1] o.s.c.c.s.e.EnvironmentController        : Error getting the Environment with name=ecommerce profiles=default label=null includeOrigin=false

org.springframework.cloud.config.server.environment.NoSuchRepositoryException: Cannot clone or checkout repository: https://github.com/YoungKyonYou/spring-cloud-config
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.refresh(JGitEnvironmentRepository.java:320) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.getLocations(JGitEnvironmentRepository.java:262) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.getLocations(MultipleJGitEnvironmentRepository.java:139) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.AbstractScmEnvironmentRepository.findOne(AbstractScmEnvironmentRepository.java:55) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.findOneFromCandidate(MultipleJGitEnvironmentRepository.java:188) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.MultipleJGitEnvironmentRepository.findOne(MultipleJGitEnvironmentRepository.java:173) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.CompositeEnvironmentRepository.findOne(CompositeEnvironmentRepository.java:64) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentEncryptorEnvironmentRepository.findOne(EnvironmentEncryptorEnvironmentRepository.java:61) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentController.getEnvironment(EnvironmentController.java:132) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.EnvironmentController.defaultLabel(EnvironmentController.java:109) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:78) ~[na:na]
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:566) ~[na:na]
        at org.springframework.util.ReflectionUtils.invokeMethod(ReflectionUtils.java:282) ~[spring-core-5.3.14.jar!/:5.3.14]
        at org.springframework.cloud.context.scope.GenericScope$LockedScopedProxyFactoryBean.invoke(GenericScope.java:485) ~[spring-cloud-context-3.1.0.jar!/:3.1.0]
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:753) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:698) ~[spring-aop-5.3.14.jar!/:5.3.14]
        at org.springframework.cloud.config.server.environment.EnvironmentController$$EnhancerBySpringCGLIB$$60d7694f.defaultLabel(<generated>) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:78) ~[na:na]
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
        at java.base/java.lang.reflect.Method.invoke(Method.java:566) ~[na:na]
        at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:205) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:150) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:117) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:895) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:808) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1067) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:963) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:898) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:655) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883) ~[spring-webmvc-5.3.14.jar!/:5.3.14]
        at javax.servlet.http.HttpServlet.service(HttpServlet.java:764) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:227) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53) ~[tomcat-embed-websocket-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.boot.actuate.metrics.web.servlet.WebMvcMetricsFilter.doFilterInternal(WebMvcMetricsFilter.java:96) ~[spring-boot-actuator-2.6.2.jar!/:2.6.2]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:117) ~[spring-web-5.3.14.jar!/:5.3.14]
        at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:189) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:162) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:197) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:97) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:540) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:135) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:78) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:357) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:382) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:895) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1732) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1191) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:659) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-9.0.56.jar!/:na]
        at java.base/java.lang.Thread.run(Thread.java:831) ~[na:na]
Caused by: org.eclipse.jgit.api.errors.TransportException: https://github.com/YoungKyonYou/spring-cloud-config: cannot open git-upload-pack
        at org.eclipse.jgit.api.FetchCommand.call(FetchCommand.java:224) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.CloneCommand.fetch(CloneCommand.java:303) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.CloneCommand.call(CloneCommand.java:178) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.cloneToBasedir(JGitEnvironmentRepository.java:658) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.copyRepository(JGitEnvironmentRepository.java:633) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.createGitClient(JGitEnvironmentRepository.java:616) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        at org.springframework.cloud.config.server.environment.JGitEnvironmentRepository.refresh(JGitEnvironmentRepository.java:296) ~[spring-cloud-config-server-3.1.0.jar!/:3.1.0]
        ... 73 common frames omitted
Caused by: org.eclipse.jgit.errors.TransportException: https://github.com/YoungKyonYou/spring-cloud-config: cannot open git-upload-pack
        at org.eclipse.jgit.transport.TransportHttp.connect(TransportHttp.java:749) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.TransportHttp.openFetch(TransportHttp.java:465) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.FetchProcess.executeImp(FetchProcess.java:142) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.FetchProcess.execute(FetchProcess.java:94) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.Transport.fetch(Transport.java:1309) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.api.FetchCommand.call(FetchCommand.java:213) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        ... 79 common frames omitted
Caused by: java.net.UnknownHostException: github.com: Temporary failure in name resolution
        at java.base/java.net.Inet4AddressImpl.lookupAllHostAddr(Native Method) ~[na:na]
        at java.base/java.net.InetAddress$PlatformNameService.lookupAllHostAddr(InetAddress.java:932) ~[na:na]
        at java.base/java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1517) ~[na:na]
        at java.base/java.net.InetAddress$NameServiceAddresses.get(InetAddress.java:851) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName0(InetAddress.java:1507) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName(InetAddress.java:1366) ~[na:na]
        at java.base/java.net.InetAddress.getAllByName(InetAddress.java:1300) ~[na:na]
        at org.apache.http.impl.conn.SystemDefaultDnsResolver.resolve(SystemDefaultDnsResolver.java:45) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.conn.DefaultHttpClientConnectionOperator.connect(DefaultHttpClientConnectionOperator.java:112) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.conn.PoolingHttpClientConnectionManager.connect(PoolingHttpClientConnectionManager.java:376) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.MainClientExec.establishRoute(MainClientExec.java:393) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.MainClientExec.execute(MainClientExec.java:236) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.ProtocolExec.execute(ProtocolExec.java:186) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.RetryExec.execute(RetryExec.java:89) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.execchain.RedirectExec.execute(RedirectExec.java:110) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.InternalHttpClient.doExecute(InternalHttpClient.java:185) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:83) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:108) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:56) ~[httpclient-4.5.13.jar!/:4.5.13]
        at org.eclipse.jgit.transport.http.apache.HttpClientConnection.execute(HttpClientConnection.java:274) ~[org.eclipse.jgit.http.apache-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.http.apache.HttpClientConnection.getResponseCode(HttpClientConnection.java:251) ~[org.eclipse.jgit.http.apache-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.util.HttpSupport.response(HttpSupport.java:205) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        at org.eclipse.jgit.transport.TransportHttp.connect(TransportHttp.java:654) ~[org.eclipse.jgit-5.12.0.202106070339-r.jar!/:5.12.0.202106070339-r]
        ... 84 common frames omitted
```

<br>

일주일동안 이 에러에 시달렸던 것 같다.
아무리 구글링을 해도 찾을 수가 없었고 결국 한줄한줄 읽어보며 뭐가 문제인지 찾아봤던 것 같다.

```bash
(...)

2022-01-27 05:41:05.532  WARN 1 --- [nio-8889-exec-1] .c.s.e.MultipleJGitEnvironmentRepository : Error occured cloning to base directory.

org.eclipse.jgit.api.errors.TransportException: https://github.com/YoungKyonYou/spring-cloud-config: cannot open git-upload-pack
(...)

org.springframework.cloud.config.server.environment.NoSuchRepositoryException: Cannot clone or checkout repository: https://github.com/YoungKyonYou/spring-cloud-config
(...)
```

<br>

읽다가 위 내용에 신경이 좀 가게됐다. 일단 컨테이너 내부적으로 git clone 명령을 해서 해당 리포지토리를 가지고 온다음 거기서 원하는 리소스를 가져오는 방법인 것 같았다.

그렇다면 어떤 디렉토리 아래 폴더에 clone를 하고 가져오는지 찾는 게 중요했다. 

<br>

어디에서 clone를 하는지 찾기 위해서 도커로 배포 안 하고 단순히 WSL Ubuntu 환경에서 jar 파일을 실행시키고 로그를 살펴보았다. 신기하게 이때는 제대로 작동하고 원하는 리소를 가져온다.

<br>

**WSL Ubuntu에서 실행시킨 Config-Server jar파일의 Log**

```bash
youngyou@DESKTOP-KCDHFKO:~/configuration-service-docker$ java -jar config-service-1.0.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.6.2)

2022-01-28 17:20:52.574  INFO 8835 --- [           main] c.e.c.ConfigServiceApplication           : The following profiles are active: dev
2022-01-28 17:20:54.410  INFO 8835 --- [           main] faultConfiguringBeanFactoryPostProcessor : No bean named 'errorChannel' has been explicitly defined. Therefore, a default PublishSubscribeChannel will be created.
2022-01-28 17:20:54.455  INFO 8835 --- [           main] faultConfiguringBeanFactoryPostProcessor : No bean named 'integrationHeaderChannelRegistry' has been explicitly defined. Therefore, a default DefaultHeaderChannelRegistry will be created.
2022-01-28 17:20:54.648  INFO 8835 --- [           main] o.s.cloud.context.scope.GenericScope     : BeanFactory id=2d1905bd-ddb1-3c02-8186-79b2dca87272
2022-01-28 17:20:54.791  INFO 8835 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-28 17:20:54.806  INFO 8835 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'bindersHealthContributor' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration$BindersHealthContributor] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-28 17:20:54.810  INFO 8835 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'bindersHealthIndicatorListener' of type [org.springframework.cloud.stream.config.BindersHealthIndicatorAutoConfiguration$BindersHealthIndicatorListener] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-28 17:20:54.836  INFO 8835 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.integration.config.IntegrationManagementConfiguration' of type [org.springframework.integration.config.IntegrationManagementConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-28 17:20:54.853  INFO 8835 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'integrationChannelResolver' of type [org.springframework.integration.support.channel.BeanFactoryChannelResolver] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2022-01-28 17:20:55.435  INFO 8835 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8889 (http)
2022-01-28 17:20:55.457  INFO 8835 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2022-01-28 17:20:55.458  INFO 8835 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.56]
2022-01-28 17:20:55.575  INFO 8835 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2022-01-28 17:20:55.575  INFO 8835 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 2971 ms
2022-01-28 17:20:58.216  INFO 8835 --- [           main] o.s.c.s.m.DirectWithAttributesChannel    : Channel 'application-1.springCloudBusInput' has 1 subscriber(s).
2022-01-28 17:20:59.499  INFO 8835 --- [           main] o.s.cloud.commons.util.InetUtils         : Cannot determine local hostname
2022-01-28 17:21:00.095  INFO 8835 --- [           main] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 1 endpoint(s) beneath base path '/actuator'
2022-01-28 17:21:00.283  INFO 8835 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : Adding {logging-channel-adapter:_org.springframework.integration.errorLogger} as a subscriber to the 'errorChannel' channel
2022-01-28 17:21:00.284  INFO 8835 --- [           main] o.s.i.channel.PublishSubscribeChannel    : Channel 'application-1.errorChannel' has 1 subscriber(s).
2022-01-28 17:21:00.289  INFO 8835 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : started bean '_org.springframework.integration.errorLogger'
2022-01-28 17:21:00.295  INFO 8835 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Creating binder: rabbit
2022-01-28 17:21:00.481  INFO 8835 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Caching the binder: rabbit
2022-01-28 17:21:00.481  INFO 8835 --- [           main] o.s.c.s.binder.DefaultBinderFactory      : Retrieving cached binder: rabbit
2022-01-28 17:21:00.584  INFO 8835 --- [           main] c.s.b.r.p.RabbitExchangeQueueProvisioner : declaring queue for inbound: springCloudBus.anonymous.z1QYk6O7QyOl8Wtxk65Hxw, bound to: springCloudBus
2022-01-28 17:21:00.592  INFO 8835 --- [           main] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [127.0.0.1:5672]
2022-01-28 17:21:00.747  INFO 8835 --- [           main] o.s.a.r.c.CachingConnectionFactory       : Created new connection: rabbitConnectionFactory#13cda7c9:0/SimpleConnection@4bb003e9 [delegate=amqp://guest@127.0.0.1:5672/, localPort= 56002]
2022-01-28 17:21:00.920  INFO 8835 --- [           main] o.s.c.stream.binder.BinderErrorChannel   : Channel 'springCloudBus.anonymous.z1QYk6O7QyOl8Wtxk65Hxw.errors' has 1 subscriber(s).
2022-01-28 17:21:00.922  INFO 8835 --- [           main] o.s.c.stream.binder.BinderErrorChannel   : Channel 'springCloudBus.anonymous.z1QYk6O7QyOl8Wtxk65Hxw.errors' has 2 subscriber(s).
2022-01-28 17:21:00.958  INFO 8835 --- [           main] o.s.i.a.i.AmqpInboundChannelAdapter      : started bean 'inbound.springCloudBus.anonymous.z1QYk6O7QyOl8Wtxk65Hxw'
2022-01-28 17:21:00.987  INFO 8835 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8889 (http) with context path ''
2022-01-28 17:21:01.990  INFO 8835 --- [           main] o.s.cloud.commons.util.InetUtils         : Cannot determine local hostname
2022-01-28 17:21:02.037  INFO 8835 --- [           main] c.e.c.ConfigServiceApplication           : Started ConfigServiceApplication in 13.415 seconds (JVM running for 14.725)
2022-01-28 17:21:40.099  INFO 8835 --- [nio-8889-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2022-01-28 17:21:40.101  INFO 8835 --- [nio-8889-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2022-01-28 17:21:40.103  INFO 8835 --- [nio-8889-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 2 ms
2022-01-28 17:21:42.635  INFO 8835 --- [nio-8889-exec-1] o.s.c.c.s.e.NativeEnvironmentRepository  : Adding property source: Config resource 'file [/tmp/config-repo-14397014959275925187/ecommerce.yml]' via location 'file:/tmp/config-repo-14397014959275925187/'
2022-01-28 17:21:42.635  INFO 8835 --- [nio-8889-exec-1] o.s.c.c.s.e.NativeEnvironmentRepository  : Adding property source: Config resource 'file [/tmp/config-repo-14397014959275925187/application.yml]' via location 'file:/tmp/config-repo-14397014959275925187/'
2022-01-28 17:21:42.641  WARN 8835 --- [nio-8889-exec-1] o.s.c.c.s.e.CipherEnvironmentEncryptor   : Cannot decrypt key: token.secret (class java.lang.IllegalStateException: Cannot load keys from store: URL [file:/Users/nick1/Spring_MSA_Study/keystore/apiEncryptionKey.jks]) 
```
<br>

여기서 중요한 단서를 찾을 수 있었다.

<br>

```bash
(...)
2022-01-28 17:21:42.635  INFO 8835 --- [nio-8889-exec-1] o.s.c.c.s.e.NativeEnvironmentRepository  : Adding property source: Config resource 'file [/tmp/config-repo-14397014959275925187/ecommerce.yml]' via location 'file:/tmp/config-repo-14397014959275925187/'
2022-01-28 17:21:42.635  INFO 8835 --- [nio-8889-exec-1] o.s.c.c.s.e.NativeEnvironmentRepository  : Adding property source: Config resource 'file [/tmp/config-repo-14397014959275925187/application.yml]' via location 'file:/tmp/config-repo-14397014959275925187/'
(...)
```

<br>

위 로그를 통해서 내가 만약 <span style="background: rgb(251,243,219)">Dockerfile</span>를 통해 컨테이너를 실행하게 되면 config-server는 컨테이너의 <span style="background: rgb(251,243,219)">/tmp/config-repo-(랜덤 숫자들)</span> 폴더 안에서 리소스를 가져온다는 것이다. <span style="background: rgb(251,243,219)">ecommerce.yml과 application.yml</span> 파일의 내용이 내가 원하는 리소스 내용이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

정리하면 내가 Dockerfile를 통해 이미지를 만들고 <span style="background: rgb(251,243,219)">run</span>하게 되면 config-server가 내부적으로 /tmp/config-repo-(랜덤숫자들) 디렉토리 안에서 <span style="background: rgb(251,243,219)">git clone url</span>를 하게 되는 것이다. 그리고 그렇게 clone한 리소스를 우리가 특정 url로 접근하게 되면 보여주는 것이다.

<br>

확인을 위해 다시 도커 이미지를 실행시키고 <span style="background: rgb(251,243,219)">sudo docker exec -it [컨테이너 ID] bash</span> 명령을 통해 터미널로 들어가보았다.

역시 예상했던 대로 /tmp/config-repo 폴더가 생성이 되어 있었고 안에는 아무 내용이 없었다. 그리고 git clone [내 리소스가 있는 url] 명령을 치자 clone이 되지 않았다. 물론 그전에 이 명령어들을 실행하고 다운받는 것이 필요하다
<br>

```bash
apt-get update -y; \
apt-get upgrade -y; \
apt-get install git -y;
```

<br>

git clone만 된다면 문제는 해결될 것이다. 구글링을 하다가 나와 비슷한 문제가 발생한 사람의 질문 중 답변을 확인해보니 <span style="background: rgb(251,243,219)">ping github.com</span>의 결과가 제대로 나오는지 보라는 것이었다. 

<br>

역시나 제대로 작동하지 않았다. 그렇다면 WSL 안에 컨테이너가 외부 네트워크랑 통신을 못하고 있다고 가정을 하게 되었다.

그리고 여러 자료를 찾다가 해결 방안을 2가지 찾았다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> (해결 1) /etc/resolv.conf 파일 수정하기
</h3>

<br>

컨테이너 안으로 이전에 했던 명령어 <span style="background: rgb(251,243,219)">exec -it</span>로 터미널에 들어가고 <span style="background: rgb(251,243,219)">/etc/resolv.conf</span> 파일을 열게되면 아래와 같은 사진의 내용이 보인다.

<br>

![](/images/Interview/post16/2022-01-28-17-39-10.png?style=centerme)

<br>

이 내용을 아래와 같이 수정하는 것이다.

```bash
nameserver 127.0.0.11
nameserver 8.8.8.8
nameserver 8.8.4.4
options edns0
```

<br>

그리고 /tmp/config-repo-(랜덤 숫자들) 폴더 아래 <span style="background: rgb(251,243,219)">git clone [원하는 리소스가 있는 리포지토리 url]</span>를 하면 제대로 접근이 된다.

하지만 이 방법은 일일이 컨테이너를 없애고 만들때마다 해줘야 하며 이는 매우 불편하다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> (해결 2) /etc/default 디렉터리 아래 docker 파일 수정하기
</h3>

<br>

기본 WSL Ubuntu 터미널에서 docker를 다운받았다면 /etc/default 디렉터리 안에 docker라는 파일이 있다 이를 아래와 같이 수정한다.

<br>

```bash
# Docker Upstart and SysVinit configuration file

#
# THIS FILE DOES NOT APPLY TO SYSTEMD
#
#   Please see the documentation for "systemd drop-ins":
#   https://docs.docker.com/engine/admin/systemd/
#

# Customize location of Docker binary (especially for development testing).
#DOCKERD="/usr/local/bin/dockerd"

# Use DOCKER_OPTS to modify the daemon startup options.
DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"

# If you need Docker to use an HTTP proxy, it can also be specified here.
#export http_proxy="http://127.0.0.1:3128/"

# This is also a handy place to tweak where Docker's temporary files go.
#export DOCKER_TMPDIR="/mnt/bigdrive/docker-tmp"
```

<br>

이렇게 하고 config-server를 배포하게 되면 정상적으로 리소스를 가져올 수 있고 <span style="background: rgb(251,243,219)">해결 1</span> 방안보다 더 좋다.

<br>

