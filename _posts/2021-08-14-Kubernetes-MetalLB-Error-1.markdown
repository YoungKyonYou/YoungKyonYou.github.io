---
layout: post
title: MetalLB-Failed to allocate IP for ... address also in use by ... 문제 해결하기
date: 2021-08-11 10:00:00 0000
tags: [Kubernetes, MetalLB, Prometheus]
categories: [Kubernetes]
description: AllocationFailed
---

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

# <center>프로메테우스로 모니터링 데이터 수집과 통합하기</center>

<br>

쿠버네티스 프로메테우스를 helm으로 설치하고 grafana를 사용하던 중 원래 사용하던 프로메테우스의 External IP를 브라우저로 접속하려고 해도 작동하지 않았다.

<br>

원인을 찾기위해서 프로메테우스 서비스의 <span style="color:orange; font-weight:bold">External IP</span>를 확인해 봤다.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-25-25.png){: p}

<br>

원래 <span style="color:orange; font-weight:bold">External IP</span>가 존재했는데 어느 순간 <span style="color:#85144b; font-weight:bold">pending</span>이 되어 있었다.

원인을 찾기 위해서 **describe** 명령으로 살펴봤다.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-26-36.png){: p}

<br>

애레를 보니 <span style="color:orange; font-weight:bold">AllocationFailed</span>라고 나오면서 **metallb-controller**가 IP 할당을 실패한 것을 볼 수 있었다.

<br>

에러 문구를 읽어보자 이해가 됐다. 내가 프로메테우스 단독으로 사용할 때는 괜찮았는데 grafana를 연동시키면서 IP가 <span style="color:orange; font-weight:bold">Overwrite</span>된 것 같다. grafana로 접속할 땐 내가 원래 프로메테우스를 접속할 때 사용했던 External IP가 할당되어 있었고 프로메테우스로 접속하려고 했던 External IP가 막혀서 <span style="color:orange; font-weight:bold">pending</span> 상태였던 것이다.

<br>

이를 해결하기 위해 여러 가지 검색을 했다. 일단 내가 찾은 <span style="color:#3D9970; font-weight:bold">stackoverflow</span> 게시물을 참고해보자. (아래 링크 첨부)

**[stackoverflow](https://stackoverflow.com/questions/44519980/assign-external-ip-to-a-kubernetes-service)**

<br>

질문자가 나와 동일한 문제는 아니지만 도움이 될 것 같아서 답변해준대로 따라해봤다.

<br>

해결 방안은 External IP를 수동으로 설정해 주는 것이였다.

<br>

그래서 시도한 명령어는 아래와 같다.

<br>

```bash
kubectl patch svc prometheus-server -p '{"spec":{"externalIPs":["192.168.1.11"]}}'
```

<br>

현재 grafana가 **192.168.12**를 사용하고 있으므로 프로메테우스를 **192.168.11**로 설정해 준 것이었다.

<br>

이렇게 설정하면 **prometheus-server**의 **External-IP**가 **192.168.11**로 바꿔지긴 한다.

<br>

<span style="color: rgba(131, 24, 67);">그러나..</span> 브라우저로 접속이 되지 않는다.

<br>

이는 서비스가 제공하는 Service가 제공하는 External-IP가 **192.168.11**이기 때문이다. 내가 처음 프로메테우스를 설치할 때 **MetalLB**와 연동해서 설치해줬었다. 즉 MetalLB의 metallb-controller가 제공하는 **External IP**를 바꿔줘야 한다.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-38-30.png){: p}

<br>

해결책은 생각보다 간단했다. 바로 <span style="color:orange; font-weight:bold">edit</span> 명령을 사용하는 것이다.

<br>

```bash
kubectl edit service prometheus-server
```

<br>

위의 명령을 치면 아래 사진과 같이 나온다.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-40-08.png){: p}

<br>

yaml 파일을 수정할 수 있는 편집기가 나오는데 밑으로 내리다 보면 <span style="color:orange; font-weight:bold">status</span>이라고 써져 있는 부분이 있다. 거기서 **.status.loadBalancer.ingress.ip**를 192.168.1.15로 바꾼다.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-41-39.png){: p}

<br>

그리고 **Esc+':'+wq**를 누르고 저장하고 나온다.

<br>

External IP를 확인해 보자.

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-42-46.png){: p}

<br>

External IP가 두개가 할당되어 있는데 **192.168.1.11**은 처음에 우리가 stackoverflow에서 본 해결책으로 할당한 것이고 **192.168.1.15**로 우리가 방금 할당한 것이다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-information 
<div class="webnots-success webnots-notification-box">192.168.1.11가 거슬리면 edit 명령으로 해당 부분을 지워주면 된다.</div>

<br>

이제 브라우저로 **192.168.1.15**를 접속해보자.

<br>

![](/images/Kubernetes/Kubernetes-Error-1/2021-08-14-13-44-45.png){: p}

<br>

접속이 정상적으로 된다~!!
