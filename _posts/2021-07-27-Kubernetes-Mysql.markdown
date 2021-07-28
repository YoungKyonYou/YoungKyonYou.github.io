---
layout: post
title: Kubernetes와 Mysql Workbench 연동하기
date: 2021-07-27 10:00:00 0000
tags: [Kubernetes, Mysql-Workbench]
categories: [Kubernetes]
description: 쿠버네티스와 Mysql Workbench 연동하기
---

<br><br>
_**피곤한데 커피 한잔만 마시고 시작해보자..**_

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

# <center>Kubernetes와 Mysql Workbench 연동하기</center>

<br>

여기서는 교육용 및 소규모 환경에서 사용하기 좋은 베이그런트(Vagrant)를 사용하고 베이그런트와 호환성이 좋은 버추얼박스(VirtualBox)를 사용해서 진행한다.

![](/images/Kubernetes/kubernetes-Mysql/2021-07-27-23-54-14.png)

<br>

<style lang="scss">
 p{
    text-align:center;
 }
</style>

![](/images/Kubernetes/kubernetes-Mysql/2021-07-27-23-54-32.png){: p}

<br>

Vagrantfile 설정은 밑에 링크 달아놓은 이전 게시물을 참고<br>

**[Vagranfile 설정](https://youngkyonyou.github.io/kubernetes/2021/07/20/Kubernetes-3.1.3.html)**

<br>

위 링크에 들어가면 나오는 Vagrantfile과 스크립트들을 한 디렉토리에 넣고 **vagrant up**를 하게 되면 아래 사진과 같이 virtual box에 4개의 가상 머신이 생기는 것을 확인할 수 있다.

<br>

![](../images/Kubernetes/kubernetes-Mysql/2021-07-28-09-56-23.png){: p}

<br>

이제 **Superputty**로 m-k8s를 접속한다.

<br>

![](/images/Kubernetes/kubernetes-Mysql/2021-07-28-09-57-40.png){: p}

<br>

그리고 우리는 쿠버네티스 공식 문서에서 mysql를 배포하는 방법에 대해서 따라한다.

<br>

**[쿠버네티스 공식 문서](https://kubernetes.io/ko/docs/tasks/run-application/run-single-instance-stateful-application/)**

<br>

이 사이트에서는 쿠버네티스 클러스터에서 퍼시스턴트볼륨(PersistentVolume)과 디폴로이먼트(Deployment)를 사용하여, 단일 이스턴스 스테이트풀 애플리케이션을 실행하는 방법을 보인다. 해당 애플리케이션은 MYSQL이다.

<br>

이전에 <span style="color:red; font-weight:bold">PV</span>(PersistentVolume)과 <span style="color:red; font-weight:bold">PVC</span>(PersistentVolumeClaim)에 대해서 좀 알아보자.

파드에서 생성한 내용을 기록하고 보관하거나 모든 파드가 동일한 설정 값을 유지하고 관리하기 위해 공유된 볼륨으로부터 공통된 설정을 가지고 올 수 있도록 설계해야하는데 이때 원격으로 지원하는 것이 PVC이다. 쿠버네티스는 필요할 때 <span style="color:red; font-weight:bold">PVC</span>를 요청해 사용한다. <span style="color:red; font-weight:bold">PVC</span>를 사용하려면 <span style="color:red; font-weight:bold">PV</span>로 볼륨을 선언해야 한다. 간단하게 <span style="color:red; font-weight:bold">PV</span>는 볼륨을 사용할 수 있게 준비하는 단계이고 <span style="color:red; font-weight:bold">PVC</span>는 준비된 볼륨에서 일정 공간을 할당받는 것이다. 비유하면 <span style="color:red; font-weight:bold">PV</span>는 요리사(관리자)가 피자를 굽는 것이고, <span style="color:red; font-weight:bold">PVC</span>는 손님(사용자)가 원하는 만큼의 피자를 접시에 담아 가져오는 것이다.

<br>
