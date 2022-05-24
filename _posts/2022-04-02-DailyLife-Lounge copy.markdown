---
layout: post
title: 센트로폴리스 라운지 후기
date: 2022-04-01 13:00:00 0000
tags: [Centropolis, Lounge]
categories: [daily-life]
description: 회사 내 안식처
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

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Centropolis 라운지 후기
</h3>

<br>

어느덧 회사를 입사한지 2달이 되었다. <span style="background: rgb(251,243,219)">취준생</span>이였던 게 엊그제 같은데 시간 정말 빠르다. 

그동안 입사하고 소감을 먼저 적고 싶었으나 수습 교육을 받고 부서에 배치되느라 시간이 없었던 것 같다. 

수습 기간은 종각 본사에서 받았는데 건물 자체가 너무 이쁘다. 아침 출근 시간에 찍은 건물 사진은 빛이 난다.

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-26-56.png?style=centerme)

<br>

사실 이번 포스트를 적게 된 이유는 소감을 적기 위한 것은 아니고 회사 내에 라운지 후기에 관해 적고 싶었다. 아무도 그 후기에 대해 적은 글이 없기에 내가 처음으로 적고 싶었다.

<br>

센트로폴리스 건물 안 3층에는 아주 좋은 휴식 공간이 있다. 일단 3층으로 올라가게 되면 아래와 같은 문이 있다.

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-29-21.png?style=centerme)

<br>

일반인은 들어갈 수 없고 센트로폴리스 건물 내 상주하고 있는 회사 사람만 들어갈 수 있다. 직원카드를 카드기에 되면 문이 열리는 방식이다. 이게 더 라운지의 가치를 높여주는 것 같다.

<br>

다행히 내가 라운지를 갔을 땐 사람이 얼마 없었다. 아마도 열심히 다들 일하느라 그렇지 않을까 싶다. 그리고 내가 애매한 시간에 왔기 때문일 것이다. 

어쨌든 문을 열고 들어가게 되면 쾌적하고 깔끔한 공간을 목격할 수 있다.

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-31-58.png?style=centerme)

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-32-16.png?style=centerme)

<br>

무엇보다 엄청 넓고 자리마다 간격이 넓어 사람들이랑 대화하기 좋았다.

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-32-55.png?style=centerme)

<Br>

![](/images/DailyLife/Lounge/2022-04-02-18-33-11.png?style=centerme)

<Br>

![](/images/DailyLife/Lounge/2022-04-02-18-33-19.png?style=centerme)

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-33-28.png?style=centerme)

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-33-55.png?style=centerme)

<Br>

더 좋았던 것은 안에 커피와 간식을 팔기 때문에 커피를 사서 직장 동기들과 앉아 대화하는 것이 좋았다. 

<br>

가운데 책상에는 다양한 잡지들이 가지런히 놓여있었다. 실제로 보는지는 의문이다.

![](/images/DailyLife/Lounge/2022-04-02-18-34-50.png?style=centerme)

<br>

가끔 회사 일을 하다가 지치면 내려와 커피 한잔을 하면서 쉬기에 너무 좋다. 창밖의 거리도 괜찮고 분위기도 조용하고 해서 혼자만의 시간을 갖기에도 좋은 것 같다.

<br>

![](/images/DailyLife/Lounge/2022-04-02-18-38-38.png?style=centerme)

<br>

단점은 저녁 7시에 닫는 다는 것과 주말에 운영하지 않는 다는 게 아쉬웠다. 그래도 장점은 일반인이 들어올 수 없어 점심 시간이 아니라면 사람이 그리 많지 않다는 점과 동기들과 일종의 수다를 떨거나 한숨 돌릴 수 있다는 점에서 좋았다. 

회사에 유일한 힐링 공간이라고 할 수 있겠다. 

혹시나 친구들이나 아는 사람이 회사 근처에 오게 된다면 여기서 커피 한잔 정도 대접해주고 싶은 그런 공간이다.