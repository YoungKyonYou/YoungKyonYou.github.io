---
layout: post
title: 디자인 패턴-Observer Pattern
date: 2021-12-16 13:00:00 0000
tags: [Design Pattern, Observer Pattern]
categories: [Interview]
description: 책임 연쇄 Pattern에 대해 알아보자
---

<br><br>

_**오늘보다 발전된 내일의 나를 위해...**_

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

# <center>Design Pattern-Wrapper Pattern</center>

<br>

_해당 내용은 POCU 아카데미 COMP_2500에서 배운 내용을 공부하기 위해 작성된 글입니다_

<br>

<span style="background: rgb(251,243,219)">Proxy Pattern</span>

<br>

<span style="background: rgb(251,243,219)">옵저버 패턴</span>은 옛날에 많이 사용했지만 지금은 좀 더 일반적이고 더 다양하게 사용할 수 있는 방식을 사용한다. A라는 개체가 있다고 하자. B가 A를 감시한다.

<br>

![](/images/Interview/post6/2021-12-16-17-59-33.png?style=centerme)

<br>

어느 순간 <span style="background: rgb(251,243,219)">A가 바뀌면 B가 그것을 깨닫고 행동</span>을 하게 되는 것이다 그런데 B가 한명만 있는 게 아니다.

<br>

![](/images/Interview/post6/2021-12-16-18-00-21.png?style=centerme)

<br>

여러 개가 있을 수 있다. B, C, D, E도 감시를 하고 있을 수도 있다 하지만 A는 하나이다.

<br>

![](/images/Interview/post6/2021-12-16-18-01-17.png?style=centerme)

<br>

A를 감시하며 A가 변하면 감시하고 있는 것들도 바뀌는 것이다. 이때 쓰는 패턴이 <span style="background: rgb(251,243,219)">옵저버 패턴</span>이다.

<br>

![](/images/Interview/post6/2021-12-16-18-02-16.png?style=centerme)

<br>

요즘은 옵저버보다 더 자주 사용하는 패턴이 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 발행-구독(pub-sub) 패턴
</h3>

<br>

- **pub**: publisher(발행자)의 줄임말
- **sub**: subscriber(구독자)의 줄임말
- 옵저버와 비슷하지만 엄밀히 말하면 <span style="background: rgb(251,243,219)">다른 패턴</span>
- 그러나 <span style="background: rgb(251,243,219)">이루려는 목적은 비슷</span>하기에 같은 패턴이라고 보는 일도 흔함

<br>

사실 이미 발행-구독 패턴에 대해서 코드를 써본적이 있다. 바로 이전 포스트에서의 **LogManager**이다. (아래 링크 참고)

**[책임 연쇄 패턴](https://youngkyonyou.github.io/interview/2021/12/16/Interview-interview-05.html)**

 <br>

![](/images/Interview/post6/2021-12-16-18-09-01.png?style=centerme)

<br>

즉, 여기서 <span style="background: rgb(251,243,219)">LogManager</span>를 빼면 그게 옵저버 패턴인 것이다.

<br>

<span style="background: rgb(251,243,219)">옵저버 패턴의 예</span>를 하나 들어보자.
<span style="background: rgb(251,243,219)">크라우드펀딩</span> 예를 구성해보겠다.
돈이 들어올 때마다 두 개체를 업데이트

- <span style="background: rgb(251,243,219)">장부를 업데이트</span>(상태는 금액만 필요)
- 모바일 폰에서 <span style="background: rgb(251,243,219)">노티</span>를 받음( 상태는 이름과 금액이 필요)

<br>

**IFundingCallback Interface**

```java
public interface IFundingCallback{
  void onMoneyRaised(String backer, int amount);
}
```

<br>

**BookkeepingApp Class**

```java
public final class BookkeepingApp implements IFundingCallback{

  //멤버 변수와 메서드는 모두 생략

  @Override
  public void onMoneyRaised(String backer, int amount){
    //장부에 새 내역 추가
    //amount만 사용
  }

}
```

<br>

**MobileApp Class**

```java
public final class MobileApp implements IFundingCallback{
  //멤버 변수와 메서드는 모두 생략

  @Override
  public void onMoneyRaised(String backer, int amount){
    //모바일 앱에 알림을 보여준다
    //backer와 amount 모두 사용
  }

}
```

<br>

**CrowdFundingAccount Class**

```java
public final class CrowdFundingAccount{
  private int balance;

  private ArrayList<IFundingCallback> subscribers;

  public CrowdFundingAccount(){
    this.subscribers=new ArrayList<IFundingCallback>();
  }

  public void subscribe(IFundingCallback sub){
    subscribers.add(sub);
  }

  public void support(String backer, int amount){
    this.balance+=amount;

    for(IFundingCallback sub:subscribers){
      sub.onMoneyRaised(backer, amount);
    }
  }
}
```

<br>

위 코드를 통해 <span style="background: rgb(251,243,219)">CrowdFundingAccount</span>라는 <span style="background: rgb(251,243,219)">발행자</span>가 하나이고 ArrayList로 구성된 <span style="background: rgb(251,243,219)">subscribers</span>를 통해 <span style="background: rgb(251,243,219)">구독자</span>는 여럿인 것을 볼 수 있다.

<br>

<span style="color:orange; font-weight:bold">pub-sub 패턴과의 차이는 <span style="background: rgb(251,243,219)">발행자가 하나</span>이다. 즉, pub-sub은 <span style="background: rgb(251,243,219)">다대다 관계(many-to-many)</span>이고 그걸 조율해주는 <span style="background: rgb(251,243,219)">중간 클래스</span>가 있을 뿐인 것이다.</span>

<br>

<span style="background: rgb(251,243,219)">옵저버</span>와 <span style="background: rgb(251,243,219)">pub-sub</span>의 차이는 <span style="background: rgb(251,243,219)">발행자가 하나냐 여럿이냐의 차이</span>다.
