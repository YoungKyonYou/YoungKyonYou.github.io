---
layout: post
title: 디자인 패턴-Proxy Pattern
date: 2021-12-16 10:00:00 0000
tags: [Design Pattern, Proxy Pattern]
categories: [Interview]
description: Proxy Pattern에 대해 알아보자
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

### Proxy Pattern

<br>

웹 브라우저 설정 등을 뒤자다 보면 프록시 서버라는 걸 볼 수 있다. **Proxy Server**는 실제 웹사이트와 사용자 사이에 위치하는 중간 서버이다. 인터넷상의 캐시 메모리처럼 작동한다. 사용자가 프록시 서버를 통해 원하는 문서를 읽으려 할 때 프록시 서버에 이미 그 문서가 저장되어 있다면 그걸 반환한다. 없다면 실제 웹서버에서 문서를 읽어와 프록시 서버에 저장한다.

<br>

프록시 패턴이 이루려는 목적도 비슷하다. 클래스 안에서 어떤 상태를 유지하는 게 여의치 않은 경우가 있다. 데이터가 너무 커서 미리 읽어 두면 메모리가 부족하고 개체 생성 시 데이터를 로딩하면 시간이 꽤 걸린다. 그리고 개체는 만들었으나 그 속의 데이터를 사용하지 않을 수도 있다. 이럴 경우 다음과 같은 방법을 통해 불필요한 데이터 로딩을 방지한다.

- 개체 생성 시에는 데이터 로딩에 필요한 정보만(예: 파일 위치) 기억해 둠
- 클라이언트가 실제로 데이터를 요청할 때 메모리에 로딩함

<br>

예를 들어보자. 이미지는 프록시 패턴을 적용하기 적합한 데이터이다. 용량이 크고 저장장치에서 읽어와야 하기 때문이다. 

프록시 패턴을 적용하기 전 코드를 살펴보자

<br>

**Image Class**

```java
public final class Image{
  private ImageData image;

  public Image(String filePath){
    this.image=ImageLoader.getInstance().load(filePath);
  }

  public void draw(Canvas canvas, float x, float y){
    canvas.draw(this.image, x, y);
  }
}
```

<br>

위 코드에서 문제점

- 생성자에서 무조건 이미지를 읽어 옴
- 메모리를 많이 사용
- 이미지를 읽어오는 데 시간도 걸림(디스크 읽는 속도는 좀 느리니까)
- 모든 image에 대해 draw()가 호출될지도 의심스러움

<br>

이제 프록시 패턴을 적용한 결과를 보자.

<br>

<br>

**Image Class**

```java
public final class Image{
  private String filePath;
  private ImageData image;

  public Image(String filePath){
    this.filePath=filePath;
  }

  public void draw(Canvas canvas, float x, float y){
    if(this.image==null){
      this.image=ImageLoader.getInstance().load(this.filePath);
    }

    canvas.draw(this.image, x, y);
  }
}
```

<br>

위 코드를 보면 생성자에서 개체 생성 시에 아무 데이터도 읽지 않는다. 처음 사용할 때 draw() 메소드를 통해 이미지를 로딩한다. draw() 메서드를 보면 이미 메모리에 로딩을 해 놨다면 그대로 가져다 쓴다. 이렇게 늦게 읽어오는 방식을 지연 로딩(lazy loading)이라고 하고 반대 방식은 즉시 로딩(eager loading)이라고 한다. 

<br>

언제 지연 로딩을 사용하고 언제 즉시 로딩을 사용해야 할까? 각각의 장단점을 살펴보자.

<br>

![](/images/Interview/post4/2021-12-16-10-35-20.png?style=centerme)

<br>

요즘 컴퓨터에는 메모리를 많이 장착한다. 미리 다 로딩해놔도 큰 문제가 아닌 경우가 많다. 한 번에 그리는 이미지 수가 많지 않다면 필요할 때마다 디스크에서 읽을 수 있다.(SSD면 더 빠르다) 하지만 인터넷에서 그 이미지들을 로딩한다면 디스크에서 읽을 때보다 시간이 더 오래 걸린다. 그 동안에 프로그램이 멈춰 있다면 사용자에게 나쁜 경험을 줄 수 있다. 

<br>

요즘은 클라이언트가 내부 동작방법을 분명히 알고 그에 적합한 UI를 보여주는 방법이 더 사랑받는다. 따라서 요즘 세상에는 클래스가 남몰래 프록시 패턴을 사용하는 것보다 클라이언트에게 조작 권한을 주는 게 좋을 수 있다. 어떻게 하는 지 살펴보자.

<br>

**Image Class**

```java
public final class Image{
  private String filePath;
  private ImageData image;

  public Image(String filePath){
    this.filePath=filePath;
  }

  public boolean isLoaded(){
    return this.image!=null;
  }

  public void load(){
    if(this.image==null){
      this.image=ImageLoader.getInstance().load(this.filePath);
    }
  }
  public void unload(){
    this.image=null;
  }
  public void draw(Canvas canvas, float x, float y){
    canvas.draw(this.image, x, y);
  }
}
```

<br>

위의 코드에서 isLoaded() / load() / unload() 는 이미지의 로딩 상태를 클라이언트가 명확히 알 수 있게 해준다. 클라이언트가 로딩과 언로딩 시점을 직접 제어할 수 있게 해준다. 이를 이용해 게임이나 앱에서 봤던 로딩 스크린을 보여줄 수 있다.(모든 이미지를 다 읽어올 때까지)