---
layout: post
title: Kubernetes와 Mysql Workbench 연동하기-2
date: 2021-08-24 10:00:00 0000
tags: [Kubernetes, Mysql-Workbench]
categories: [Kubernetes]
description: 쿠버네티스와 Mysql Workbench 연동하기(로드밸런서 사용)
---

<br><br>
_**피곤한데 커피 한잔만 마시고 시작해보자..**_
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

# <center>Kubernetes와 Mysql Workbench 연동하기-2(로드 밸런서 사용하기)</center>

<br>

이전에 쿠버네티스 클러스터 내에서 mysql 서비스와 외부에서 접근할 수 있게 nodeport를 만들어서 사용했던 적이 있다. 그것에 관한 내용은 아래 링크에 달아놓겠다. 이 글을 이해하려면 아래 링크를 통해서 먼저 학습을 하기 바란다.

<br>

**[Kubernetes와 Mysql Workbench 연동하기-1](https://youngkyonyou.github.io/kubernetes/2021/07/27/Kubernetes-Mysql.html)**

<br>

위 링크에서 노드포트를 생성하기 전까지 과정은 동일하다. 여기서는 노드포트를 사용하기 보다는 로드밸런서를 사용할 것이다. 보통 클라우드를 사용해서 하는 것이 일반적이나 우리는 온프레미스 환경임으로 추가적인 설정이 필요하다.

<br>

그것은 metallb를 사용하는 것이다. 여기서는 최대한 간단하게 로드밸런서를 사용해서 mysql에 접근하는 방법을 설명하기 때문에 metallb와 관련된 내용도 아래 링크에 달아놓겠다.

<br>

**[온프레미스에서 로드밸런서를 제공하는 MetalLB](https://youngkyonyou.github.io/kubernetes/2021/08/01/Kubernetes-MetalLB-3.3.4.html)**

<br>

위에 달아놓은 링크를 봤다면 아래 사진과 같은 상태일 것이다. 4개의 스피커가 있고 하나의 컨트롤러가 있다.

![](/images/Kubernetes/kubernetes-Mysql/2021-08-24-18-56-51.png){: p}

<br>

그리고 첫 번째로 단 링크를 보고 노드포트를 설정하기 전까지 왔다면 아래 사진과 같이 mysql 파드가 있는 것을 볼 수 있다.

<br>

![](/images/Kubernetes/kubernetes-Mysql/2021-08-24-18-58-22.png){: p}

<br>

먼저 해야 할 일은 mysql service를 삭제 해줘야 한다. expose를 해서 다시 생성해줄 것이기 때문이다.

<br>

```bash
kubectl delete service mysql
```

<br>

위 명령으로 mysql service를 지운다음 다시 만든다.

```bash
kubectl expose deployment mysql --type=LoadBalancer --name=mysql --port=3306
```

<br>

위 명령을 입력하면 mysql 서비스와 함께 External IP가 생성된다.

![](/images/Kubernetes/kubernetes-Mysql/2021-08-24-19-00-27.png){: p}

<br>

External IP가 <span style="color: rgba(131, 24, 67); font-weight:bold">192.168.1.13</span>으로 지정된 것을 볼 수 있다.

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">
<div class="webnots-information webnots-notification-box">여기서 노드포트 때와는 다르게 포트는 의미가 없다.(30286)</div>

<br>

이제 <span style="color:orange; font-weight:bold">Mysql Workbench</span>로 접근해 보자.

<br>

![](/images/Kubernetes/kubernetes-Mysql/2021-08-24-19-02-32.png){: p}

<br>

위 사진과 같이 설정하되 <span style="color:#001f3f; font-weight:bold">Store in Vault</span>를 누르고 password에 우리가 설정했던 <span style="color:orange; font-weight:bold">password</span>를 입력해준다. 그리고 <span style="color:orange; font-weight:bold">Test Connection</span>를 누르면 연결이 된 것을 볼 수 있다.
