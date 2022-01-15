---
layout: post
title: 싱글턴 패턴
date: 2022-01-15 13:20:00 0000
tags: [Singleton Pattern]
categories: [Interview]
description: 싱글턴 패턴에 대해
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Sigleton Pattern
</h2>

<br>

**싱글턴 패턴**: 어떤 클래스에서 만들 수 있는 <span style="background: rgb(251,243,219)">인스턴스 수를 하나로 제한</span>하는 패턴이다.

<br>

다음과 같은 조건을 충족하는 개체에 적합하다.

1. 프로그램 실행 중에 <span style="background: rgb(251,243,219)">최대 하나만</span> 있어야 할 경우
2. <span style="background: rgb(251,243,219)">전역적으로 접근</span>이 가능한 개체여야 할 경우

<br>

딱 하나(single)만 존재해야만 해서 이름이 **싱글턴**인 것이다.

<br>

일부 사람들은 <span style="background: rgb(251,243,219)">static</span>를 싫어한다. 그 이유는 <span style="background: rgb(251,243,219)">전역 변수</span> 같아 보이고 개체가 아니기 때문이다. 하지만 <span style="background: rgb(251,243,219)">싱글턴</span>은 이러한 비판을 해결하는 패턴이다. 그러면서도 OO(개체지향)에서 <span style="background: rgb(251,243,219)">전역 변수 및 전역 함수</span>를 만드는 법이다.

<br>

싱글턴 패턴은 기본적으로 <span style="background: rgb(251,243,219)">private 생성자</span>를 사용한다. 그럼으로 <span style="background: rgb(251,243,219)">static</span> 메서드를 통해서만 개체를 얻어올 수 있는데 바로 <span style="background: rgb(251,243,219)">getInstance()</span>메서드이다. 개체가 없는 경우 <span style="background: rgb(251,243,219)">개체를 생성 후 static 변수에 저장</span>하고 <span style="background: rgb(251,243,219)">static 변수에 저장된 개체를 반환</span>하게 된다. 

이미 개체가 있는 경우 <span style="background: rgb(251,243,219)">static 변수</span>에 저장되어 있는 개체를 반환한다. 아래 코드를 보자

<br>

```java
public class Singleton{
  private static Singleton instance;
  private Singleton(){

  }
  public static Singleton getInstance(){
    if(instance==null){
      instance=new Singleton();
    }
    return instance;
  }
}
```

<br>

**Main**

```java
Singleton instance0=Singleton.getInstance();
Singleton instance1=Singleton.getInstance();

System.out.println("same Object? "+(instance0==instance1));
```

<br>

위는 싱글턴 패턴의 간단한 예이다. 밑에 코드는 <span style="background: rgb(251,243,219)">Math</span> 클래스를 사용한 <span style="background: rgb(251,243,219)">싱글턴 패턴</span>의 예이다.

<br>

**Math Class**

```java
public class Math{
  private static Math instance;
  
  private Math(){

  }
  
  public static Math getInstance(){
    if(instance==null){
      instance=new Math();
    }
    return instance;
  }

  public int abs(int n){
    return n<0?-n:n;
  }
  (...)
}
```

<br>

**Main**

```java
int absValue=Math.abs(-2); //컴파일 오류가 발생 

Math math=Math.getInstance();
int minValue=math.min(-2,1);
int maxValue=Math.getInstance().max(3,100);
```

<br>

여기서 중요하게 봐야할 점은 싱글턴을 만다는데 사용한 <span style="background: rgb(251,243,219)">static</span>이다. Math Class에서 변수를 만들때도 <span style="background: rgb(251,243,219)">static</span>를 사용했고 <span style="background: rgb(251,243,219)">getInstance()</span> 메서드를 만드는데도 <span style="background: rgb(251,243,219)">static</span>를 사용했다. 그리고 나머지는 <span style="background: rgb(251,243,219)">static이 아니라 일반 메서드이다.</span>

위 클래스는 메서드만 있어 별로 좋은 예는 아니다. 이번에는 상태도 가지는 다른 싱글턴을 보자.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 프로그램 설정 읽기 - Configuration 싱글턴
</h3>

<br>

![](/images/Interview/post16/2022-01-15-15-02-40.png?style=centerme)

<br>

- 설정은 프로그램 실행 중 하나만 존재한다.
- 프로그램 창의 위치와 크기를 기억한다.
- 파일에 저장하거나 파일로부터 로딩이 가능하다.

<br>

위 클래스 다이어그램을 보면 밑줄 친 것은 static 선언을 했다는 것을 알 수 있다. 그리고 멤버 변수들은 <span style="background: rgb(251,243,219)">static</span>이 아니다.

<br>

**Configuration Class**

```java
public class Configuration{
  private static Configuration instance;
  private int x;
  private int y;
  private int width;
  private int height;

  private Configuration(){

  }
  
  public static Configuration getInstance(){
    if(instance==null){
      instance=new Configuration();
    }

    return instance;
  }

  public int getX(){
    return this.x;
  }

  public void setX(int x){
    this.x=x;
  }

  public int getY(){
    return this.y;
  }

  public void setY(int y){
    this.y=y;
  }

  public int getWidth(){
    return this.width;
  }
  (... 생략)
  
  public void save(String filename){
    //설정을 파일로 저장
  }

  public void load(String filename){
    //파일로부터 설정 읽기
  }
}
```

<br>

**Main**

```java
//프로그램 실행 후 파일로부터 설정을 읽어 옴
Configuration config=Configuration.getInstance();

config.load("settings.csv");
```

```java
//창 위치 바뀔 때, x와  y를 설정함
Configuration config=Configuration.getInstance();

config.setX(windowX);
config.setY(windowY);

//프로그램 종료 시, save()를 이용해서 변경 사항을 파일에 저장
config.save();
```

<br>

그런데 결과적으로 <span style="background: rgb(251,243,219)">static</span>으로 만드는 것과 같지 않나? 물론 <span style="background: rgb(251,243,219)">Configuration 예</span>에서는 그렇다. 그런데 두 방법(static vs 싱글턴) 간에 다른 점은 분명히 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> static으로는 못하는 일
</h3>

<br>

- 다형성을 사용할 수 없다.
- 시그내처를 그대로 둔 채 멀티턴(multiton) 패턴으로 바꿀 수 없다.
- 개체의 생성 시점을 제어할 수 없다
  - Java의 static은 프로그램 실행 시에 초기화됨
  - 단, 싱글턴을 사용해도 제어에 어려움이 있음

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 싱글턴 생성 시 인자가 필요한 경우
</h3>

<br>

```java
public class GraphicsResourceManager{
  (...)
  public static GraphicsResourceManager getInstance(FileLoader loader, GraphicsDevice gfxDevice){
    if(instance==null){
      instance=new GraphicsResourceManager(loader, gfxDevice);
    }
    return instance;
  }
}
```

<br>

```java
// 프로그램 시작 시
GraphicsResourceManager.getInstance(loader, gfxDevice);

//다른 클래스에서
GraphicsResourceManager.getInstance(???,???);
```

<br>

한 예로 GraphicsResource는 화면에 이미지, 3차원 모델등을 보여주는 것이라고 해보자. 그러면 실제 화면에 그림을 그릴 장치(GraphicsDevice gfxDevice)가 필요하고 파일을 로딩해야 하니까 파일 로딩에 관한 개체(FileLoader loader)도 필요할 것이다. 

그럼 위와 같이 매개변수를 전달해서 만들어줘야 한다. 물론 loader, gfxDevice를 먼저 초기화하고 매개변수로 넣어줄 수 있겠지만 주석에서 명시한 것과 같이 다른 클래스에서 getInstance()로 가져온다고 해보자. 그럼 사용하지도 않을 매개변수를 넣어줘야 하는데 다른 클래스에 loader와 gfxDevice가 들어가 있지 않을 가능성이 높다.

그럼 다른 클래스 안에 저 매개변수가 없다면 어떻게 할 것인가? 그것을 해결하기 어렵다. 

<br>

**싱글턴의 변형**

- 현재의 구현으로는 표현이 어렵다.
- 따라서 실무에서는 다른 변형을 사용하기도 한다.
- 디자인 패턴은 그저 가이드 라인일뿐
- 필요에 따라 변형해서 사용하는 것도 괜찮다.

<br>

위 예제를 조금 변형해보자.

<br>

![](/images/Interview/post16/2022-01-15-15-24-46.png?style=centerme)

<br>

```java
public class GraphicsResourceManager{
  private static GraphicsResourceManager instance;

  private GraphicsResourceManager(FileLoader loader, GraphicsDevice gfxDevice){
    (...)
  }

  public static void createInstance(FileLoader loader, GraphicDevice gfxDevice){
    assert (instance==null) : "do not create instance twice";

    instance = new GraphicsResourceManager(loader, gfxDevice);
  }

  public static void deleteInstance(){
    assert (instance != null) : "no instance to delete";

    instance = nulll;
  }

  public static GraphicsResourceManager getInstance(){
    assert (instance != null) : "no instance was created before get()";

    return instance;
  }
}
```

<br>

위는 createInstance와 getInstance가 분리된 형태다. 

프로그램 실행 시 getInstance()가 아니라 createInstance()를 호출하는 형태다.

```java
GraphicsResourceManager.createInstance(loader, gfxDevice);
```

<br>

인스턴스가 필요할 때는 매개변수가 없는 getInstance()를 호출해준다.

```java
GraphicsResourceManager gfxManager=GraphicsResourceManager.getInstance();
```

<br>

더 이상 사용하지 않는 싱글턴 인스턴스를 삭제한다.

```java
GraphicsResourceManager.deleteInstance();
```

<br>

바뀐 getInstance() 함수는 싱글턴 인스턴스가 null일 경우를 대비해서 어서트(assert)를 추가했다. 그리고 createInstance()가 먼저 호출됐다는 가정으로 돈다.

```java
public static GraphicsResourceManager getinstance(){
  asswert (instance != null) : "no instance was created before get()";

  return instance;
}
```


