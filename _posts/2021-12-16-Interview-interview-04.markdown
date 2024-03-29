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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Proxy Pattern
</h2>

<br>

웹 브라우저 설정 등을 뒤자다 보면 <span style="background: rgb(251,243,219)">프록시 서버</span>라는 걸 볼 수 있다. **Proxy Server**는 실제 웹사이트와 사용자 사이에 위치하는 <span style="background: rgb(251,243,219)">중간 서버</span>이다. 인터넷상의 <span style="background: rgb(251,243,219)">캐시 메모리</span>처럼 작동한다. 사용자가 프록시 서버를 통해 원하는 문서를 읽으려 할 때 <span style="background: rgb(251,243,219)">프록시 서버</span>에 이미 그 문서가 저장되어 있다면 그걸 반환한다. 없다면 실제 웹서버에서 문서를 읽어와 프록시 서버에 저장한다.

<br>

프록시 패턴이 이루려는 목적도 비슷하다. 클래스 안에서 <span style="background: rgb(251,243,219)">어떤 상태를 유지</span><span style="background: rgb(251,243,219)">하는 게 여의치 않은 경우</span>가 있다. 데이터가 너무 커서 미리 읽어 두면 메모리가 부족하고 개체 생성 시 데이터를 로딩하면 시간이 꽤 걸린다. 그리고 개체는 만들었으나 그 속의 데이터를 사용하지 않을 수도 있다. 이럴 경우 다음과 같은 방법을 통해 <span style="background: rgb(251,243,219)">불필요한 데이터 로딩을 방지</span>한다.

- 개체 생성 시에는 <span style="background: rgb(251,243,219)">데이터 로딩에 필요한 정보만(예: 파일 위치)</span> 기억해 둠
- <span style="background: rgb(251,243,219)">클라이언트가 실제로 데이터를 요청</span>할 때 메모리에 로딩함

<br>

예를 들어보자. 이미지는 <span style="background: rgb(251,243,219)">프록시 패턴</span>을 적용하기 적합한 데이터이다. 용량이 크고 저장장치에서 읽어와야 하기 때문이다.

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

- 생성자에서 <span style="background: rgb(251,243,219)">무조건 이미지를 읽어 옴</span>
- <span style="background: rgb(251,243,219)">메모리</span>를 많이 사용
- 이미지를 읽어오는 데 <span style="background: rgb(251,243,219)">시간도 걸림</span>(디스크 읽는 속도는 좀 느리니까)
- <span style="background: rgb(251,243,219)">모든 image에 대해 draw()가 호출</span>될지도 의심스러움

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

위 코드를 보면 생성자에서 <span style="background: rgb(251,243,219)">개체 생성 시에 아무 데이터도 읽지 않는다.</span> 처음 사용할 때 <span style="background: rgb(251,243,219)">draw() 메소드</span>를 통해 이미지를 로딩한다. draw() 메서드를 보면 <span style="background: rgb(251,243,219)">이미 메모리에 로딩</span>을 해 놨다면 그대로 가져다 쓴다. 이렇게 늦게 읽어오는 방식을 <span style="background: rgb(251,243,219)">지연 로딩(lazy loading)</span>이라고 하고 반대 방식은 <span style="background: rgb(251,243,219)">즉시 로딩(eager loading)</span>이라고 한다.

<br>

언제 <span style="background: rgb(251,243,219)">지연 로딩</span>을 사용하고 언제 <span style="background: rgb(251,243,219)">즉시 로딩</span>을 사용해야 할까? 각각의 장단점을 살펴보자.

<br>

![](/images/Interview/post4/2021-12-16-10-35-20.png?style=centerme)

<br>

요즘 컴퓨터에는 메모리를 많이 장착한다. 미리 다 로딩해놔도 큰 문제가 아닌 경우가 많다. 한 번에 그리는 이미지 수가 많지 않다면 필요할 때마다 디스크에서 읽을 수 있다.(SSD면 더 빠르다) 하지만 인터넷에서 그 <span style="background: rgb(251,243,219)">이미지들을 로딩한다면 디스크에서 읽을 때보다 시간이 더 오래 걸린다.</span> 그 동안에 프로그램이 멈춰 있다면 사용자에게 <span style="background: rgb(251,243,219)">나쁜 경험</span>을 줄 수 있다.

<br>

요즘은 클라이언트가 내부 동작방법을 분명히 알고 그에 <span style="background: rgb(251,243,219)">적합한 UI</span>를 보여주는 방법이 더 사랑받는다. 따라서 요즘 세상에는 클래스가 남몰래 프록시 패턴을 사용하는 것보다 <span style="background: rgb(251,243,219)">클라이언트에게 조작 권한</span>을 주는 게 좋을 수 있다. 어떻게 하는 지 살펴보자.

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

위의 코드에서 <span style="background: rgb(251,243,219)">isLoaded() / load() / unload()</span> 는 <span style="background: rgb(251,243,219)">이미지의 로딩 상태</span>를 클라이언트가 명확히 알 수 있게 해준다. 클라이언트가 <span style="background: rgb(251,243,219)">로딩과 언로딩 시점</span>을 직접 제어할 수 있게 해준다. 이를 이용해 게임이나 앱에서 봤던 <span style="background: rgb(251,243,219)">로딩 스크린</span>을 보여줄 수 있다.(모든 이미지를 다 읽어올 때까지)

---

**_프록시 패턴의 흔한 다른 예시 살펴보기_**

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 
프록시 패턴이란?</h3>

<br>
 
<span style="background: rgb(251,243,219)">프록시</span>는 <span style="background: rgb(251,243,219)">대리인</span>이라는 뜻으로 무엇인가를 대신 처리하는 의미이다.

<span style="background: rgb(251,243,219)">일종의 비서</span>라고 생각하면 된다.

어떤 객체를 사용하고자 할때, 객체를 **직접적으로 참조** 하는 것이 아니라, <span style="background: rgb(251,243,219)">해당 객체를 대행(대리, proxy)하는 객체</span>를 통해 대상객체에 접근하는 방식을 사용하면 해당 객체가 메모리에 존재하지 않아도 기본적인 정보를 참조하거나 설정할 수 있고 또한 실제 객체의 기능이 반드시 필요한 시점까지 객체의 생성을 미룰 수 있다.

<br>

![](/images/Interview/post16/2022-01-01-12-15-29.png?style=centerme)

<br>

예를 들어 <span style="background: rgb(251,243,219)">용량이 큰 이미지와 글</span>이 같이 있는 문서를 모니터 화면에 띄운다고 가정하였을 때 이미지 파일은 용량이 크고 텍스트는 용량이 작아서 텍스트는 빠르게 나타나지만 그림은 조금 <span style="background: rgb(251,243,219)">느리게 로딩</span>되는 것을 본 적이 있다.

만약 이렇게 처리가 안되고 <span style="background: rgb(251,243,219)">이미지와 텍스트가 모두 로딩</span>이 된 후에야 화면이 나온다면 사용자는 페이지가 로딩될 때까지 의미없이 기다려야 한다. 그러므로 먼저 로딩이 되는 텍스트라도 먼저 나오는게 좋다.

이런 방식을 취하려면 텍스트 처리용 프로세서, 그림 처리용 프로세스를 별도로 운영하면 된다.

이런 구조를 갖도록 설계하는 것이 바로 **프록시 패턴**이다.

일반적으로 다른 무언가와 이어지는 인터페이스의 역할을 하는 클래스를 의미한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프록시 패턴 장점
</h3>

<br>

- 사이즈가 큰 객체(ex: 이미지)가 로딩되기 전에도 <span style="background: rgb(251,243,219)">프록시를 통해 참조</span>를 할 수 있다.
- 실제 객체의 public, protected 메소드들을 숨기고 인터페이스를 통해 노출시킬 수 있다.
- 로컬에 있지 않고 떨어져 객체를 사용할 수 있다.
- 원래 <span style="background: rgb(251,243,219)">객체의 접근에 대해서 사전처리</span>를 할 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프록시 패턴 단점
</h3>

<br>

- 객체를 생성할 때 한 단계를 거치게 되므로, 빈번한 객체 생성이 필요한 경우 <span style="background: rgb(251,243,219)">성능이 저하</span>될 수 있다.
- 프록시 내부에서 객체 생성을 위해 <span style="background: rgb(251,243,219)">스레드가 생성, 동기화가 구현되야 하는 경우</span> 성능이 저하될 수 있다.
- 로직이 난해해져 <span style="background: rgb(251,243,219)">가독성</span>이 떨어질 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프록시 패턴 예제
</h3>

<br>

**Image Interface**

```java
public interface Image {
   void displayImage();
}
```

<br>

**RealImage.java**

```java
public class RealImage implements Image {

    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(fileName);
    }

    private void loadFromDisk(String fileName) {
        System.out.println("Loading " + fileName);
    }

    @Override
    public void displayImage() {
        System.out.println("Displaying " + fileName);
    }
}
```

<br>

**ProxyImage.java**

```java
public class ProxyImage implements Image {
    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void displayImage() {
        if (realImage == null) {
            realImage = new Real_Image(fileName);
        }
        realImage.displayImage();
    }
}
```

<br>

**Main**

```java
public class Main {
    public static void main(String[] args) {
        Image image1 = new Proxy_Image("test1.png");
        Image image2 = new Proxy_Image("test2.png");

        image1.displayImage();
        System.out.println();
        image2.displayImage();
    }
}
```

<br>

![](/images/Interview/post16/2022-01-01-12-23-24.png?style=centerme)
