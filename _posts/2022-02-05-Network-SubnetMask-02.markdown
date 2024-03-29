---
layout: post
title: Subnet Mask란?
date: 2022-02-05 13:00:00 0000
tags: [Subnet Mask, Broadcast, Network]
categories: [Network]
description: Subnet Mask의 정의와 연습문제
---

<br><br>

_**오늘의 나보다 성장한 내일의 나를 위해....**_

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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> 서브넷 마스크(Subnet Mask)란?
</h2>

<br>

<span style="background: rgb(251,243,219)">서브넷 마스크</span>의 개념에 앞서 <span style="background: rgb(251,243,219)">서브네팅(Sub-netting)</span>의 개념에 대해 먼저 알아야 한다.

서브넷팅은 하나의 주 네트워크(Major Network)를 필요한 만큼 <span style="background: rgb(251,243,219)">분할</span>하여 상호 연결 망을 구축할 수 있게 해주는 것이다. IP 주소의 고갈 문제를 해결하기 위해 설계된 개념이고 반대로 <span style="background: rgb(251,243,219)">축약</span>하는 개념은 <span style="background: rgb(251,243,219)">수퍼넷팅(Super-netting)</span>이라고 한다.

예를 들어, 회사에 영업부(50명), 회계부(50명), 관리부(50명) 등이 존재하는데 이를 하나의 네트워크로 묶을 수도 있지만 이를 분할해서 네트워크를 구분 지어준다. 이 구분된 네트워크를 <span style="background: rgb(251,243,219)">브로드캐스트 도메인(Broadcast Domain)</span>이라고 하고 너무 큰 브로드캐스트 도메인은 자원을 효율적으로 분배하기 어려워서 속도가 느려진다.

따라서, 서브넷팅으로 네트워크를 분할하게 되면 필요한 네트워크 주소만 호스트 IP로 할당해서 쓸모없이 버려지는 잉여 IP를 최소화할 수 있으며 <span style="background: rgb(251,243,219)">Broadcast Domain Size</span>를 줄여주므로 LAN의 Traffic을 줄일 수 있다. 또한 여러 <span style="background: rgb(251,243,219)">네트워크로 분할</span>되므로 분할된 각 network(서로 다른 부서) 업무 간에 <span style="background: rgb(251,243,219)">보안</span>을 유지할 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 서브넷 마스크란?
</h3>

<br>

<span style="background: rgb(251,243,219)">서브넷 마스크</span>란 IP Address에서 첫비트부터 <span style="background: rgb(251,243,219)">어디까지가 네트워크 부분</span>인가 알려주는 역할이다. 쉽게 생각하면 IP 주소에 마스크를 씌워서 어디까지가 네트워크 부분인가를 표시하는 것이다. IP Address처럼 32비트로 구성되며, <span style="background: rgb(251,243,219)">네트워크 부분</span>을 표시하는 비트는 <span style="color:#001f3f; font-weight:bold">1</span>, 호스트 부분은 </span>을 표시하는 비트는 <span style="color:#001f3f; font-weight:bold">0</span>이다. 또한,연속성이 존재해서 네트워크 부분 중간에 0이 들어갈 수 없다.

예를 들어, IP 주소 <span style="background: rgb(251,243,219)">192.168.1.1</span>에 서브넷 마스크가 <span style="background: rgb(251,243,219)">255.255.255.0</span>라면 <span style="background: rgb(251,243,219)">255</span>로 표시된 부분인 <span style="background: rgb(251,243,219)">192.168.1.</span>까지는 네트워크 부분이고 <span style="background: rgb(251,243,219)">0</span>으로 표시된 부분인 <span style="background: rgb(251,243,219)">.1</span>은 호스트 부분이다. 다시 말해, <span style="background: rgb(251,243,219)">255는 이진법</span>으로 표시하면 <span style="background: rgb(251,243,219)">1111111</span>이기 때문에 <span style="background: rgb(251,243,219)">네트워크 부분</span>인 것이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 네트워크 부분과 호스트 부분을 구하는 TIP!
</h4>

서브네팅한 네트워크 부분을 확인할 때는 IP주소와 Subnet mask를 <span style="background: rgb(251,243,219)">AND 연산</span>해서 구한다. <span style="background: rgb(251,243,219)">AND 연산</span>은 각 비트를 비교해서 모두 1인 경우에만 1 값을 반환한다.

<br>

![](/images/Network/2022-02-06-16-37-58.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">255.255.255.0</span> 서브넷 마스크의 경우 <span style="background: rgb(251,243,219)">24 bit</span>가 네트워크 부분이며, <span style="background: rgb(251,243,219)">prefix</span> 표기법으로 <span style="background: rgb(251,243,219)">/24</span>이다.

<span style="background: rgb(251,243,219)">AND 연산</span>을 통해서 네트워크 부분을 구하게 될 경우 Network Address를 구할 수 있으며, 이때 <span style="background: rgb(251,243,219)">호스트 부분을 모두 1</span>로 바꿀 경우 <span style="background: rgb(251,243,219)">Broadcast Address</span>를 구할 수 있다. 이 두가지 주소의 경우 호스트에 할당할 수 없으며 이를 제외한 나머지 IP주소가 호스트에 할당 가능한 <span style="background: rgb(251,243,219)">주소(Assigned Address)</span>이다.

따라서 위의 네트워크를 보면, <span style="background: rgb(251,243,219)">192.168.1.1/24</span>는 <span style="background: rgb(251,243,219)">Network Address</span>가 <span style="background: rgb(251,243,219)">192.168.1.0</span>이고 <span style="background: rgb(251,243,219)">Broadcast Address</span>가 <span style="background: rgb(251,243,219)">192.168.1.255</span>이며 할당 가능한 호스트는 <span style="background: rgb(251,243,219)">192.168.1.1~192.168.1.254</span>까지이다. 호스트 수는 <span style="background: rgb(251,243,219)">254</span>개 이며 이를 구하는 공식은 2의 호스트 비트수 제곱에서 2를 뺀 값이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 문제를 통한 이해
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IP: 10.0.24.100 Subnet Mask: 255.0.0.0 (= 10.0.25.100/8)
</h4>

- **Network Address**: 10.0.0.0
- **Broadcast Address**: 10.255.255.255
- **할당 가능한 호스트 주소**: 10.0.0.1 ~ 10.255.255.254
- **호스트 개수**: 2^24-2 = 16777216-2 = 16777214

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IP: 192.100.2.31/16
</h4>

- **Network Address**: 192.100.0.0
- **Broadcast Address**: 192.100.255.255
- **할당 가능한 호스트 주소**: 192.100.0.1 ~ 192.100.255.254
- **호스트 개수**: 2^16-2 = 65536-2 = 65534

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IP: 151.3.192.17 Subnet Mask: 255.255.240.0 (= 151.3.192.17/20)
</h4>

- **Network Address**: 151.3.192.0
- **Broadcast Address**: 151.3.207.255
- **할당 가능한 호스트 주소**: 151.3.192.1 ~ 151.3.207.254
- **호스트 개수**: 2^12-2=4096-2 = 4094

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> IP: 192.168.4.100/26
</h4>

- **Network Address**: 192.168.4.64
- **Broadcast Address**: 192.168.4.127
- **할당 가능한 호스트 주소**: 192.168.4.65 ~ 192.168.4.126
- **호스트 개수**: 2^6-2 = 64-2 = 66

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 마지막 문제
</h3>

<br>

<span style="background: rgb(251,243,219)">192.168.4.100/26</span>를 비트화 시켜보면

<br>

**11000000 10101000 00000100 01100100**

<span style="color:#3D9970; font-weight:bold">11111111 11111111 11111111 11</span>00000

<span style="color:#3D9970; font-weight:bold">11000000 10101000 00000100 01</span> 까지 <span style="background: rgb(251,243,219)">네트워크 부분</span>이고 나머지 6비트는 <span style="background: rgb(251,243,219)">호스트</span>이다.

<br>

그래서 호스트 비트를 0으로 채운 192.168.4.64가 네트워크 주소(Network Address)이고 1로 채운

11000000 10101000 00000100 01<span style="color:#093145; font-weight:bold">111111</span> (192.168.4.127)는 <span style="background: rgb(251,243,219)">브로드캐스트 주소(Broadcast Address)</span>이다.

따라서 <span style="background: rgb(251,243,219)">네트워크 주소와 브로드캐스트 주소</span> 사이에 있는 IP 주소들이 <span style="background: rgb(251,243,219)">호스트</span>에게 할당가능한 주소(192.168.4.65 ~ 192.168.4.126)이다. 또한, 호스트 개수는 호스트 비트가 6bit 이기 때문에 2의 6제곱 빼기 2 = 64 - 2 = 62개이다.

<br>

마지막으로 한가지만 더 짚어보자

<span style="background: rgb(251,243,219)">192.168.4.100</span>은 <span style="background: rgb(251,243,219)">192</span>로 시작하기 때문에 <span style="background: rgb(251,243,219)">C 클래스</span>이다. 그러면 <span style="background: rgb(251,243,219)">네트워크 부분</span>이 <span style="background: rgb(251,243,219)">192.168.4.0/24</span> 이렇게 된다. 그러면 해당 네트워크에는 호스트 수가 <span style="background: rgb(251,243,219)">.4.1</span>부터 <span style="background: rgb(251,243,219)">.4.254</span>까지 <span style="background: rgb(251,243,219)">254</span>개가 된다.

<span style="color:#107896; font-weight:bold">그.런.데</span> 위의 문제는 네트워크 부분이 2비트가 늘어났다. 자 이렇게 서브네팅을 하게되면

**192.168.4.0 ~ 192.168.4.255**

이렇게 하나였던 네트워크를

**192.168.4.0 ~ 192.168.4.63**

**192.168.4.64 ~ 192.168.4.127**

**192.168.4.128 ~ 192.168.4.191**

**192.168.4.192 ~ 192.168.4.254**

<br>

이렇게 4개 네트워크로 분할하게 된다.

위 문제에 있던 .100 이라는 호스트는 <span style="background: rgb(251,243,219)">두 번째 네트워크</span>에 해당된다.

하나의 네트워크 일때는 호스트가 254개인데 4개의 <span style="background: rgb(251,243,219)">네트워크</span>로 분할하면 각 <span style="background: rgb(251,243,219)">네트워크</span>당 62개씩으로 할당된다. 더 <span style="background: rgb(251,243,219)">효율적</span>으로 활용이 가능하게 된 것이다. 이처럼 서브넷팅은 분할에 사용하며 반대로 네트워크를 합칠 때는 <span style="background: rgb(251,243,219)">축약</span>이라고 하며 <span style="background: rgb(251,243,219)">수퍼넷팅</span>이라고 한다.



