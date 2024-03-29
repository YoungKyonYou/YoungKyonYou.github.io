---
layout: post
title: WebSocket을 사용하는 SpringBoot 앱을 로컬 쿠버네티스 클러스터에서 Deployment로 배포하기-1
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

이번 포스팅에서는 내가 지난 몇 일간 뻘짓?과 엄청난 시간을 들여서 시도한 프로젝트에 대한 내용을 써볼까 한다. 아마 이번 게시물 시리즈는 나말고 다른 이들이 보면 이해를 못할 가능성이 크다. 왜냐면 내가 개인적으로 뻘짓한 것을 다음에 또 실수하지 않게 하려고 적은 것이기 때문이다. 그럼으로 괜한 시간 낭비를 안 하기 바란다.

<br>

<span style="color:#001f3f; font-weight:bold">머리가 나빠서 기록을 꼭 해 놔야 한다.</span>

<br>

SpringBoot 프로젝트는 내가 이번 대학교를 다니면서 졸업작품을 했던 프로젝트를 대상으로 한다. 그래서 아마 이번 포스팅은 다른 사람들이 보는 데 이해가 가지 않을 수 있다.

사실 내 개인적인 기록용이라고 생각하면 될 것 같다.

<br>

먼저 내가 지난 몇 일간 한 일에 대해 말하기 앞서 먼저 사전 작업이 되어 있어야 한다.

<br>

해당 SpringBoot 앱은 아래 링크에서 찾을 수 있다.

<br>

**[Frames-Web-Server](https://github.com/YoungKyonYou/frames-web-server)**

<br>

이번 졸업작품으로 만든 <span style="color:#7EDBFF; font-weight:bold">얼굴 인식 기반 전자출입 명부</span>이다. 상세한 내용은 설명하지 않는다.

<br>

그리고 이전 포스팅에서 설정한 것들이 있다 아래 링크를 참고한다.

<br>

**[쿠버네티스 클러스터 생성](lhttp://localhost:4000/kubernetes/2021/07/20/Kubernetes-3.1.3.htmlink)**

<br>

**[쿠버네티스와 Mysql Workbench 연동하기](http://localhost:4000/kubernetes/2021/07/27/Kubernetes-Mysql.html)**

<br>

**[온프레미스에서 로드밸런서를 제공하는 MetalLB](http://localhost:4000/kubernetes/2021/08/01/Kubernetes-MetalLB-3.3.4.html)**

<br>

**[프로메테우스로 모니터링 데이터 수집과 통합하기-1](http://localhost:4000/kubernetes/2021/08/09/Kubernetes-Prometheus-6.2-1.htmllink)**

<br>

**[프로메테우스로 모니터링 데이터 수집과 통합하기-2](http://localhost:4000/kubernetes/2021/08/11/Kubernetes-Prometheus-6.2-2.html)**

<br>

추가로 Grafana를 연동시켜 놔야하는데 그것에 대한 포스팅은 아직 하지 않았다. 하지만 추후에 할 예정이다.

오늘 이야기하는 것은 위의 링크들에서 설치한 것들이 이미 설치되었다고 가정하고 이야기 한다.

사실 이번 포스팅을 쓰려고 생각하지 않았다. 왜냐면 SpringBoot 앱을 쿠버네티스 클러스터에 배포하는 것은 **[링크](http://localhost:4000/kubernetes/2021/08/27/Kubernetes-springboot.html)** 여기서 다뤘기 때문이다.

<br>

물론 과정은 저 링크에서 소개하는 것과 같다. 하지만 문제가 생겼다. 애초에 나는 안정적인 서버 운영을 위해서 <span style="color:orange; font-weight:bold">Replica</span>를 여러 개 생성해 관리할 목적이였지만 <span style="color:orange; font-weight:bold">WebSocket</span>을 사용하는 내 앱이 <span style="color:orange; font-weight:bold">Replica</span>가 2개 이상이면 <span style="color:orange; font-weight:bold">Lost Connection</span>이 되면서 작동을 하지 않는 것이다. 내 SpringBoot 프로젝트는 첫 로그인 후에 화면이 WebSocket를 사용해 실시간으로 현황을 보여주는 데 거기서부터 막히는 것이다.

<br>

또 이상한 것은 <span style="color:orange; font-weight:bold">pod</span>를 하나만 배포했을 때는 작동을 하는 것이다. 최근 몇일 간 이것 때문에 스트레스를 너무 받았다. 어떻게 해야 할지 몰라서 구글링도 해보면서 여러 가설을 세우고 시도를 했다.

<br>

결론을 말하자면 내가 만든 SpringBoot 프로젝트의 구성에 문제가 있었다.

쿠버네티스에 웹 애플리케이션을 올린다는 것은 <span style="color:orange; font-weight:bold">MicroService Web Application</span> 구조로 올린다는 것과 같지만 내 프로젝트는 그 구조를 따르지 않았다. 한 프로젝트에 <span style="color:orange; font-weight:bold">Compact</span>하게 되어 있어서 각 기능들이 분리가 되어 있지 않다. 그것이 원인이였다.

<br>

<span style="color:orange; font-weight:bold">MicroService</span> 구조로 변환을 해야 했다. 여기서 완벽하게 <span style="color:orange; font-weight:bold">MicroService</span> 구조로 변환을 시키진 않을 것이다. 내가 기존 프로젝트에서 분리할 것은 딱 하나이다. 바로 실시간으로 데이터를 polling하는 부분이다. 이때 WebSocket를 사용하게 되는데 기존 내 SpringBoot 프로젝트의 WebSocket를 사용하는 구조가 매우 이상했다.

<br>

물론 내가 만들었다.. 일단 WebSocket이라는 것을 처음 써보기도 했고 SpringBoot도 처음 접하는 상태에서 만든 프로젝트라 많이 엉성하고 이상하다. (그래도 최대한 짜여진 틀에서 개발하려고 노력했다) 지금 생각해 보면 왜 이렇게 이상하게 코드를 짰는지... 많이 반성하고 돌아보게 된다. 아마 <span style="color:orange; font-weight:bold">replica</span>를 여러 개 만들어서 안 되는 이유는 나 때문일 것이다.

<br>

한번 간단하게 내 프로젝트에서 사용하는 <span style="color:orange; font-weight:bold">WebSocket</span>의 구조를 보자.

<br>

아래 사진에서 나오는 코드는 <span style="color:#85144b; font-weight:bold">facilityStatus.js</span>에서 나오는 코드의 일부분이다. 함수의 제목에 알맞게 해당 엔드포인트 <span style="color:orange; font-weight:bold">/ws</span>로 연결을 하는 것이다.

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-10-07-38.png){: p}

<br>

그리고 연결이 성공적이면 <span style="color:#85144b; font-weight:bold">onConnected</span> 함수를 호출하고 실패하면 <span style="color:#85144b; font-weight:bold">onError</span>를 호출한다.

<br>

아래 사진에서는 연결이 성공해서 호출되는 <span style="color:#85144b; font-weight:bold">onConnected()</span>함수이다. 여기서는 <span style="color:orange; font-weight:bold">/topic/public</span>를 구독을 하게 되고 이 특정 경로로부터 메시지가 올 경우 <span style="color:#85144b; font-weight:bold">onMessageReceived</span> 함수가 호출된다. 무엇보다 여기서 가장 이상한 점은 제일 아래 있는 <span style="color:#85144b; font-weight:bold">sendMessage()</span> 함수일 것이다. 이상한 게 맞다. 왜 이상한지 설명하겠다.

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-10-09-58.png){: p}

<br>

<span style="color:#85144b; font-weight:bold">sendMessage()</span> 함수에서는 해당 경로 <span style="color:orange; font-weight:bold">/app/status.sendMessage</span>로 메시지를 보내게 된다. 여기는 controller 패키지의 <span style="color:orange; font-weight:bold">FacilityController.java</span>에서 찾을 수 있다.

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-10-12-22.png){: p}

<br>

FacilityController.java

```java
(...)
    @MessageMapping("/status.sendMessage")
    @SendTo("/topic/public")
    public RealTimeStatusDTO sendMessage(@Payload RealTimeStatusDTO realTimeStatusDTO) {
        RealTimeStatusDTO dto = statusService.getFacilityStatus();
        return dto;
    }

(...)
```

<br>

위 사진에서 주의 깊게 또 봐야할 것은 <span style="color:orange; font-weight:bold">setTimeout</span> 부분이다. 3초 후에 다시 <span style="color: rgba(131, 24, 67); font-weight:bold">sendMessage()</span> 함수를 호출해서 반복하는 것을 볼 수 있다. 즉 3초마다 폴링하는 작업을 이렇게 구현한 것이다.

FacilityController.java는 해당 페이지에서 필요한 정보를 데이터베이스에서 가져와서 반환한다. 여기서 반환하는 dto는 다시 <span style="color:orange; font-weight:bold">Message</span>를 보내게 되는데 이는 <span style="color:orange; font-weight:bold">/topic/public</span>를 구독한 client에게 보내게 된다. 그럼 client는 아까 위해서 이야기했던 <span style="color: rgba(131, 24, 67); font-weight:bold">onMessageReceive</span> 함수에서 저 리턴된 dto를 메시지로 받게 된다.

<br>

<span style="color: rgba(131, 24, 67); font-weight:bold">onMessageReceived</span> 함수는 아래 사진과 같이 되어 있다. <span style="color:orange; font-weight:bold">FacilityController.java</span>에서 반환한 dto를 받아서 변수에 초기화 해주고 이로써 실시간으로 html에 있는 데이터가 실시간으로 변경되게 한 것이다.

<br>

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-10-19-38.png){: p}

<br>

최근 <span style="color:orange; font-weight:bold">Vue</span>를 공부하고 있는데 진짜 Vue의 양방향 데이터 바인딩이 그리워 지는 순간이다.

<br>

일단 현재 <span style="color:orange; font-weight:bold">WebSocket</span>를 사용해서 실시간으로 데이터를 페이지에 표시하는 방식이 매우 비효율적이다. 이를 바꿀 예정이다. 이 구조를 요약하면, js에서 더미 message를 보내고 그 message를 받은 백엔드에서 특정 함수를 호출하고 그 호출된 함수에서 데이터베이스에서 데이터를 조회한다음 다시 메세지를 보내는 방식이다. 다시 3초 후에 더미 message를 js 단에서 보내고 백엔드에서 받는 과정을 계속 반복한다. 나는 첫 과정을 생략하고 아예 백엔드 단에서 몇 초마다 함수를 호출되게 만들고 구독하는 client에게 데이터를 message로 보낼 것이다.

<br>

위의 구조로 쿠버네티스 클러스터에서 <span style="color:orange; font-weight:bold">replica</span>를 여러 개 생성한 다음 외부에서 접근할 수 있게 expose하고 접근하게 되면 아래 사진과 같은 에러가 발생한다.

<br>

![](/images/Kubernetes/Kubernetes-Frames/2021-08-29-10-30-02.png){: p}

<br>

위 사진은 파드가 2개 이상 <span style="color:orange; font-weight:bold">replica</span>가 있을 때 발생한다. 신기한 것은 이 에러가 발생할 수도 있고 발생하지 않을 수도 있다.

<br>

이게 무슨 말이냐면 웹소켓이 특정 <span style="color:orange; font-weight:bold">pod</span>에만 연결되는 것 같다. 왜 이런 생각을 하냐면 새로 고침을 계속하다면 웹 소켓이 작동할 때가 있는데 잘 작동하다가 다시 에러가 발생한다. 쿠버네티스는 요청을 부하분산하는 기능이 있는데 아마 <span style="color:orange; font-weight:bold">WebSocket</span>이 연결된 파드에 처음 내가 접근을 정상적으로 하다가 3초마다 메시지를 보내는 작업이 다른 파드로 연결되서 그런 것은 아닌가 생각된다. 그래서 메시지가 잘 보내지다가 중간에 <span style="color:orange; font-weight:bold">WebSocket</span>이 끊겨진다.

<br>

이를 고치기 위해 <span style="color:orange; font-weight:bold">WebSocket</span> 기능을 다른 프로젝트로 분리하고 이를 구독하는 Client에게 일정 간격으로 <span style="color:orange; font-weight:bold">BroadCasting</span> 하는 방식으로 바꾼다.

글이 너무 길어지는 것 같으니 다음 게시물에서 이어간다.
