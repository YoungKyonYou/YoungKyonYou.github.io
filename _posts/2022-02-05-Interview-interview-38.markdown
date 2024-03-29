---
layout: post
title: CIDR에 대해 알아보자
date: 2022-02-05 11:00:00 0000
tags: [CIDR]
categories: [Interview]
description: CIDR이란
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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> CIDR
</h2>

<br>

<span style="background: rgb(251,243,219)">CIDR</span>의 full name은 <span style="background: rgb(251,243,219)">Classless Inter-Domain Routing</span>으로 클래스 없는 도메인간 라우팅 기법이라는 뜻이다.

<span style="background: rgb(251,243,219)">CIDR</span>가 나오면서 <span style="background: rgb(251,243,219)">Class 체계</span>보다 더 유연하게 IP 주소를 여러 네트워크 영역으로 나눌 수 있게 되었다.

참고 하자면 클래스 구분은 아래 그림과 같다.

<br>

![](/images/Interview/post16/2022-02-05-12-08-04.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">도메인간 라우팅</span>이라는 뜻은 아래 그림에서 <span style="background: rgb(251,243,219)">Inter-Domain</span>과 같은 형태를 말한다.

<br>

![](/images/Interview/post16/2022-02-05-12-10-14.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">CIDR</span>는 위 <span style="background: rgb(251,243,219)">Intra-Domain</span>과 같이 각 네트워크 대역을 구분 짓고 <span style="background: rgb(251,243,219)">Inter-Domain</span>과 같이 구분된 네트워크간 통신을 위한 주소 체계라고 이해하면 쉽다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 표기법
</h3>

<br>

IP 뒤에 <span style="background: rgb(251,243,219)">192.168.10.0/24</span> 이런 식으로 <span style="background: rgb(251,243,219)">"/24"</span>를 본 적이 있을 것이다.

이것이 <span style="background: rgb(251,243,219)">CIDR</span> 표기법이다.

이 숫자는 <span style="background: rgb(251,243,219)">비트 단위</span>이며 <span style="background: rgb(251,243,219)">0~32</span>까지 표현이 가능하다. 이 숫자를 이해하기 위해서 IP에 대해 간략히 설명해보겠다. 아래 그림과 같이 하나의 옥텟은 8비트로 이루어져 있으며 일반적으로 사용하는 IPv4 주소는 4개의 옥텟으로 이루어져 있습니다.

따라서 <span style="background: rgb(251,243,219)">CIDR</span>는 <span style="background: rgb(251,243,219)">0~32</span>까지 총 <span style="background: rgb(251,243,219)">32비트</span>까지 사용 가능합니다.

<br>

![](/images/Interview/post16/2022-02-05-12-14-02.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">CIRDR</span>이 <span style="background: rgb(251,243,219)">"/24"</span>라면 아래 그림과 같이 앞에서부터 <span style="background: rgb(251,243,219)">24비트</span> 이후에 오는 4번 째 옥텟(파란색 부분)을 전부 사용할 수 있다는 표현이다.

<br>

![](/images/Interview/post16/2022-02-05-12-21-33.png?style=centerme)

<br>

하나의 옥텟은 <span style="background: rgb(251,243,219)">8비트</span>로 2의8승인 256개 이기 때문에, <span style="background: rgb(251,243,219)">143.7.65.0 ~ 143.7.65.255</span>까지 사용이 가능한 것이다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

이렇게 CIDR 값이 각 자리의 옥텟을 전체를 포함하는 /8, /16, /24, /32 일 경우는 계산하기 쉽다. 0부터 그 자리에 해당하는 255까지라고 보면되기 때문이다.</div>

<br>

만약 <span style="background: rgb(251,243,219)">143.7.65.203/23</span> 일때, 4번째 옥텟(파란색 부분) 전체와 3번째 옥텟(노란색 부분)영역의 1비트가 포함된다.

<br>

![](/images/Interview/post16/2022-02-05-13-58-33.png?style=centerme)

<br>

애매하게 걸친 3번째 옥텟을 2진수로 표현해보자.

<span style="background: rgb(251,243,219)">65로 01000001</span>이다.

CIDR에 의해 마지막 자리 1비트를 0 또는 1을 사용할 수 있게 되면 01000000, 01000001 이기 때문에 64, 65가 된다. 여기서 <span style="background: rgb(251,243,219)">64</span>가 3번째 옥텟에서 사용할 수 있는 <span style="background: rgb(251,243,219)">최소값</span>이 되며 <span style="background: rgb(251,243,219)">최대값</span>은 <span style="background: rgb(251,243,219)">65</span>가 된다.

나머지 4번째 옥텟(파란색 부분)은 전체를 사용할 수 있기 때문에 <span style="background: rgb(251,243,219)">최소값 0, 최대값 255</span>가 된다. 따라서 <span style="background: rgb(251,243,219)">143.7.65.203/23</span>는 <span style="background: rgb(251,243,219)">143.7.64.0 ~ 143.7.65.255</span>대역을 사용할 수 있는 것이다.

<br>

**다른 예**

<br>

<span style="background: rgb(251,243,219)">143.7.65.203/22</span>를 계산해보자.

<br>

![](/images/Interview/post16/2022-02-05-14-03-06.png?style=centerme)

<br>

일단 파란색 옥텟은 8개를 다 사용할 수 있으므로 사용할 수 있는 주소는 <span style="background: rgb(251,243,219)">0~255</span>일 것이다. 하지만 노란색 옥텟은 <span style="background: rgb(251,243,219)">아래 두개만</span> 사용할 수 있는데 최대값을 구하는 가장 쉬운 방법은 가용 비트인 제일 아래 2개를 <span style="background: rgb(251,243,219)">1로</span> 바꾼다

<span style="background: rgb(251,243,219)">01000011</span>이 되는데 이것은 <span style="background: rgb(251,243,219)">67</span>이다. 즉 최대값이 <span style="background: rgb(251,243,219)">67</span>이 되는 것이다. 

최소 값은 아래 2개 비트를 다 0으로 바꾼다. <span style="background: rgb(251,243,219)">01000000</span>즉 <span style="background: rgb(251,243,219)">64</span>가 된다 즉, 최소값이 <span style="background: rgb(251,243,219)">64</span>가 되는 것이다.