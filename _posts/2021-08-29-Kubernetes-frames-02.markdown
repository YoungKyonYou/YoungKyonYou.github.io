---
layout: post
title: WebSocket을 사용하는 SpringBoot 앱을 로컬 쿠버네티스 클러스터에서 Deployment로 배포하기-2
date: 2021-08-29 09:00:00 0000
tags:
  [
    Kubernetes,
    Docker,
    SpringBoot,
    Docker Hub,
    WebSocket,
    Prometheus,
    Grafana,
    Deployment,
    ReplicaSet,
  ]
categories: [Kubernetes]
description: 안정적인 서버 운영을 위한 쿠버네티스 클러스터 사용
---

<br><br>
_**15시간을 컴퓨터 앞에서 불태웠다..**_
<br>
(Press the Button)

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

# <center>WebSocket을 다른 프로젝트로 분리하기</center>

<br>

이전 포스팅에 이어서 이야기 해보자.

<br>

<span style="color:orange; font-weight:bold">WebSocket</span>를 분리한 프로젝트는 아래 링크를 통해서 찾을 수 있다.

<br>

**[c](https://github.com/YoungKyonYou/Frames-Websocket/blob/master/build.gradle)**

<br>

그리고 기존에 있던 프로젝트에서 <span style="color:orange; font-weight:bold">WebSocket</span>를 분리 해야 한다. 그리고 원래 Spring Security를 통한 Login 기능도 있지만 이를 제거했다.

<br>

**[Frames-App](https://github.com/YoungKyonYou/Frames-App)**

<br>

위 프로젝트를 구성하면서 중요한 점들을 하나 하나 살펴보자.

<br>

먼저 <span style="color:orange; font-weight:bold">Frames-Websocket</span>의 <span style="color:orange; font-weight:bold">port</span>를 변경한다.

<br>

```yaml
server.port = 8081
```

<br>

그 다음 **FacilityController.java**에서 <span style="color:orange; font-weight:bold">SimpMessagingTemplate template</span>를 선언 해주는 것이 필요하다. 이를 사용해 client에게 <span style="color:orange; font-weight:bold">broadcasting</span>를 할 것이기 때문이다. 아래 코드를 보자

<br>

**FacilityController.java**

```java
package org.morgorithm.websocket.controller;


import org.morgorithm.websocket.dto.EventDTO;
import org.morgorithm.websocket.dto.RealTimeStatusDTO;
import org.morgorithm.websocket.service.StatusService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.messaging.handler.annotation.MessageMapping;
import org.springframework.messaging.handler.annotation.Payload;
import org.springframework.messaging.handler.annotation.SendTo;
import org.springframework.messaging.simp.SimpMessagingTemplate;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Controller;


@Controller
public class FacilityController {
    @Autowired
    StatusService statusService;
    @Autowired
    SimpMessagingTemplate template;


    @MessageMapping("/status.sendMessage")
    @SendTo("/topic/public")
    @Scheduled(fixedDelay=3000)
    public void sendMessage() {
        RealTimeStatusDTO dto = statusService.getFacilityStatus();
        template.convertAndSend("/topic/public", dto);
    }
}

```

<br>

위 코드에서는 Scheduled 어노테이션으로 3초 마다 해당 메소드를 호출하게끔 한다. 그리고 앞서 선언한 template을 사용해 <span style="color:orange; font-weight:bold">/topic/public</span>를 구독하는 client에게 dto를 payload에 담아서 보내준다.

<br>

그리고 **WebSocketEventListener.java**에 보면 <span style="color:orange; font-weight:bold">@CrossOrigin(origins = "http://192.168.1.17:8080")</span>라고 되어 있는 부분이 있다. 이는 CORS를 해결하기 위한 것이다. 나중에 이에 대해 더 자세히 다루겠다. 해당 ip 192.168.1.17은 쿠버네티스 클러스터에서 **Frames-App**를 외부에 노출 시킬 때 사용할 ip이다.

<br>

그리고 **Frames-App**의 핵심적인 부분을 살펴보자.

<br>

**facilityStatus.js**

```javascript
(...)
function connect() {


    var socket = new SockJS('http://192.168.1.16/ws', null, {transports: ["xhr-streaming", "xhr-polling"]});

    chatPage.classList.remove('hidden');
    stompClient = Stomp.over(socket);
    console.log("connected3");
    stompClient.connect({}, onConnected, onError);

}
function onConnected() {
    console.log("onConnected() in facilitStatus.js 호출");
    stompClient.subscribe('/topic/public', onMessageReceived);
    console.log("after stompClient.subscribe");


    connectingElement.classList.add('hidden');
}
(...)
```

<br>

위 코드에서 핵심적인 것은 이제 sendMessage() 함수를 없애버리는 것과 위의 SockJS에서 특정 IP에 요청을 보내는 부분이다. IP 192.168.1.16은 쿠버네티스 클러스터에서 외부에 **Frames-WebSocket** 앱을 노출시킬 때 사용할 IP이다.

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif; padding: 40px;">

여기서 포트를 명시하지 않은 이유는 우리가 쿠버네티스 클러스터에서 Frames-WebSocket를 노출 시킬 때 해당 ip로 접근하게 되면 자동으로 8081 포트로 매핑될 수 있도록 명시할 것이기 때문이다 </div>

<br>

이제 이 두 프로젝트를 도커 허브에 저장한 다음 pod로 배포한다.

<br>

도커 허브에 저장하는 과정은 아래 링크를 참고한다.

<br>

**[SpringBoot 앱을 도커 이미지로 변환 후 Deployment로 배포하고 접근하는 방법](http://localhost:4000/kubernetes/2021/08/27/Kubernetes-springboot.html)**

<br>

여기서 나는 Frames-Websocket은

<br>

```bash
docker build --tag youngkyonyou/springboot-project:websockettest .
docker push youngkyonyou/springboot-project:websockettest
```

<br>

으로 저장했고 Frames-App은

<br>

```bash
docker build --tag youngkyonyou/springboot-project:framesfinal .
docker push youngkyonyou/springboot-project:framesfinal
```

<br>

으로 저장을 했다.

<br>

이 이미지를 사용해서 deployment를 설정해 보자.

<br>

**frames-app.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: frames-pods
  name: frames-pods
spec:
  replicas: 3
  selector:
    matchLabels:
      app: frames-pods
      tier: backend
  template:
    metadata:
      labels:
        app: frames-pods
        tier: backend
    spec:
      containers:
        - image: youngkyonyou/springboot-project:framesfinal
          name: kubernetes-spring

---
apiVersion: v1
kind: Service
metadata:
  name: frames-service
  labels:
    app: frames-pods
spec:
  selector:
    app: frames-pods
  ports:
    - port: 80
      targetPort: 8080
      protocol: TCP
  type: LoadBalancer
  loadBalancerIP: 192.168.1.17
```

<br>

하나 하나 알아가자

<br>

**frames-app.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다. apps/v1에서는 .spec.selector 와 .metadata.labels 이
#설정되지 않으면 .spec.template.metadata.labels 은 기본 설정되지 않는다.
#그래서 이것들은 명시적으로 설정되어야 한다. 또한 apps/v1 에서는
#디플로이먼트를 생성한 후에는 .spec.selector 이 변경되지 않는 점을 참고한다.
apiVersion: apps/v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Deployment
metadata:
  #레이블을 설정한다. 나중에 이 레이블은 아래
  #서비스에서 서비스할 디플로이먼트를 지정하기 위해서 사용한다.
  labels:
    app: frames-pods

  #이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
  #오브젝트를 유일하게 구분지어 줄 데이터이다.
  #디플로이먼트 이름(name)은 frames-pods이다.
  #차후에 이 디플로이먼트를 delete할 때 이 이름으로 지운다.
  name: frames-pods
spec:
  #pod를 3개를 생성한다.
  replicas: 3

  #(.spec.selector)디플로이먼트가 관리할 파드를 찾는 방법을 정의한다.
  #이 사례에서는 파드 템플릿(아래 명시된 template)에 정의된 레이블(app:frames-pods)을 선택한다.
  selector:
    matchLabels:
      app: frames-pods
      tier: backend

  template:
    #파드는 .metadata.labels 필드를 사용해서
    #app: frames-pods레이블을 붙인다
    #바로 위의 selector.matchLabels.app이랑 동일하므로
    #이 컨테이너가 선택된다.
    metadata:
      labels:
        app: frames-pods
        tier: backend
    spec:
      containers:
        #해당 도커 허브에 저장된 이미지를 사용한다.
        - image: youngkyonyou/springboot-project:framesfinal
          name: kubernetes-spring

---
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Service

metadata:
  name: frames-service

  #여기서 위에서 deployment 관련 설정을 할때
  #.metadata.labels.app에 설정했던 이름과 동일시 해야
  #서비스가 서비스할 디플로이먼트를 찾는다.
  labels:
    app: frames-pods

spec:
  selector:
    app: frames-pods
  ports:
    #외부에서 80번 포트로 접근하는 것을 내부 8080으로 접근하게 해준다.
    - port: 80
      targetPort: 8080
      protocol: TCP

      #타입은 로드밸런서 타입으로 한다.
  type: LoadBalancer

  #로드밸런서의 고정아이피를 설정한다.
  loadBalancerIP: 192.168.1.17
```

<br>

그리고 마지막으로 websocket.yaml를 살펴보자.

<br>

**websocket.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: websocket
  name: websocket
spec:
  replicas: 1
  selector:
    matchLabels:
      app: websocket
  template:
    metadata:
      labels:
        app: websocket
    spec:
      containers:
        - image: youngkyonyou/springboot-project:websockettest
          name: kubernetes-spring
---
apiVersion: v1
kind: Service
metadata:
  name: websocket-service
  labels:
    app: websocket
spec:
  selector:
    app: websocket
  ports:
    - port: 80
      targetPort: 8081
      protocol: TCP
  type: LoadBalancer
  loadBalancerIP: 192.168.1.16
```

<br>

설명은 위와 다른 게 없음으로 생략한다.

이제 다음 명령으로 <span style="color:orange; font-weight:bold">deployment</span>와 <span style="color:orange; font-weight:bold">service</span>를 배포한다.

<br>

```bash
kubectl deployment -f websocket.yaml
kubectl deployment -f frames.yaml
```

<br>

결과는 아래와 같다.

<br>

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-15-25-20.png){: p}

<br>

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-15-25-39.png){: p}

<br>

파드와 서비스가 만들어졌지만 실제로 내부적으로 웹이 배포되는 데까지 시간이 좀 걸린다.

<br>

이때 커피 한 잔을 하도록 한다.

<br>

충분히 기다리고 External IP로 접속해 보면 아래와 같이 결과가 나온다.

<br>

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-15-27-03.png){: p}

<br>

다음 게시물에서는 부하분산 테스트와 grafana 대시보드로 네트워크 트래픽 등을 보도록 하겠다.
