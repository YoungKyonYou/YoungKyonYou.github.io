---
layout: post
title: 디자인 패턴-Wrapper Pattern
date: 2021-12-15 11:00:00 0000
tags: [Design Pattern, Wrapper Pattern]
categories: [Interview]
description: Wrapper Pattern에 대해 알아보자
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

### Wrapper Pattern

- 주로 업계에서는 래퍼(wrapper) 패턴이라 함
- GoF 책에서는 어댑터(adapter) 패턴이란 이름을 사용
- 어떤 클래스의 메서드 시그내처가 맘에 안 들 때 다른 걸로 바꾸는 방법
- 단, 그 클래스의 메서드 시그내처를 직접 변경하지 않음
  - 그 클래스의 소스코드가 없을 수도 있음
  - 그 클래스에 의존하는 다른 코드가 있을 수도 있음
- 그 대신 새로운 클래스를 만들어 기존 클래스를 감쌈

<br>

![](/images/Interview/post3/2021-12-15-22-25-40.png?style=centerme)

<br>

Wrapper란 포장지를 의미한다. A 클래스의 어떤 getA()라는 메서드 시그니처가 있는데 마음에 안들어서 바꾼다고 해보자. 그러면 클래스 B를 만들고 클래스 B안에 클래스 A를 포함하는 것이다. 정확히 말하면 클래스 A로부터 만든 개체를 포함하는 것이다. 그리고 앞으로 클래스 B에 있는 getB() 메서드를 호출할 건데 이게 알아서 A의 getA()를 호출해주는 것이다. 즉 내가 호출할 때는 B만 사용하고 내부적으로는 getA()를 어떻게서든 사용하는 것이다. 그래서 기존의 클래스를 감싼다고 해서 **Wrapper Pattern** 이라고 부른다.

<br>

![](/images/Interview/post3/2021-12-15-22-29-37.png?style=centerme)

<br>

위의 사진과 같이 어댑터와 같이 이해할 수도 있다. 원래 A의 getA()라는 메서드가 있었으면 A를 그대로 사용하지 않고 앞에 B라는 어댑터를 꽂는 거이다. 그럼 A에 있는 뭔가에 어댑터를 꽂았으니까 바로 접근할 수 있는 방법이 없다. 그래서 B에서 어떻게든 접속을 해서 사용을 하라는 것이다.

<br>

#### 메서드 시그니처를 바꾸려는 다양한 이유

- 추후 외부 라이브러리를 바꿀 때 클라이언트 코드를 변경하지 않기 위해
- 그냥 사용 중인 메서드가 코딩 표준에 맞지 않아서
- 기존 클래스에 없는 기능을 추가하기 위해
- 확장된 용도: 내부 개체를 클라이언트에게 노출시키지 않기 위해
  - DTO(data transfer object) 만들기

<br>

코드로 예를 보자. 윈도우에서 사용 가능한 3D 그래픽 API는 대표적으로 두 개가 있다.

- **Microsoft DirectX**
- **OpenGL**

<br>

두 API 모두 컴퓨터에 설치된 그래픽 카드를 사용한다. 따라서 두 API에서 지원하는 기능이 매우 비슷하다. 아래와 같은 두 클래스가 있다고 하자.

<br>

![](/images/Interview/post3/2021-12-15-22-46-27.png?style=centerme)

<br>

clear()와 clearScreen() 메서드는 둘 다 화면을 어떤 색상으로 지우는 메서드이다. 다른 점은 메서드 이름과 r, g, b, a 매개변수의 형과 유효한 범위이다. **float**은 **[0.0. 1.0]**이고 **int**는 **[0, 255]**이다.

<br>

원래 프로그램에서 OpenGL을 사용했다면(즉, 내가 클라이언트) 내 소스파일 곳곳에 이런 코드가 있을 것이다.

<br>

```java
this.graphics.clearScreen(1.f, 0.f, 0.f, 0.f);
```

<br>

```java
this.graphics.clearScreen(1.f, 0.f, 0.f, 1.f);
```

<br>

그리고 추후 DirectX로 바꾸기로 결정하면 도늑 소을 찾아 고쳐야 한다.

<br>

```java
this.graphics.clear(0,0,0,255);
```

<br>

```java
this.graphics.clear(255,0,0,255);
```

<br>

즉 수정할 코드가 많을수록 실수할 가능성이 높아진다. 

<span style="color:orange; font-weight:bold">이럴 때 래퍼 클래스를 만들어 사용하면 한 곳에서만 바꾸면 된다.</span>

<br>

**Graphics Wrapper Class**

```java
public final class Graphics{
  private OpenGL gl;

  ...

  public void clear(float r, float g, float b, float a){
    this.gl.clearScreen(a, r, g, b);
  }
}
```

<br>

내부에 OpenGL 개체를 들고 있고 Graphics 메서드는 OpenGL의 메서드를 호출한다. 

<br>

**Main Class**

```java
Graphics graphics;
this.graphics.clear(0.f, 0.f, 0.f, 1.f);
```

<br>

Graphics 개체만 만들고 속에 OpenGL 개체가 들어있다. Graphics 개체의 메서드만 호출한다. 이제 여기서 OpenGL 대신 DirectX를 사용하려면 어떻게 해야 할까? **Graphics** 클래스 안에서 OpenGL 개체를 DirectX 개체로 변경하면 된다. 

**Graphics Class**

```java
public final class Graphics{
  private OpenGL gl;

  ...

  public void clear(float r, float g, float b, float a){
    this.gl.clearScreen(a, r, g, b);
  }
}
```

<br>

위 코드를 아래와 같이 바꾼다.

<br>

** Graphics Class**

```java
public final class Graphics{
  private DirectX dx;

  ...

  public void clear(float r, float g, float b, float a){
    this.dx.clear((int)(r*255),(int)(g*255),(int)(b*255), (int)(a*255));
  }
}
```

<br>

즉, **Graphics** 메서드들이 DirectX 메서드를 호출하게 변경한다. 

<br>

그리고 추가적으로 살펴볼 것이 DTO이다. 엄밀히 말하면 어댑터 패턴은 아니지만 궁극적인 목표가 같은 DTO 개념에 대해서 살펴본다. 어댑터 패턴은 타 클래스의 메서드 시그내처를 내 필요에 맞게 바꾸는 것이다. DTO는 타 클래스의 데이터를 내 필요에 맞게 바꾸는 것이다.

<br>

이제 DTO 변환하기의 간단한 예를 살펴보자. 시스템 규모가 크면 종종 이런 문제들을 겪는다. 

<br>

![](/images/Interview/post3/2021-12-15-23-16-12.png?style=centerme)

<br>

Db에 저장된 데이터를 읽어와서 웹페이지에 보여준다고 가정했을 때 PersonEntitiy의 모든 정보를 반환하면 필요 이상의 데이터를 반환하게 되는 것이다. 따라서 정말 클라이언트가 필요로 하는 정보만 반환하는 게 더 좋다 이때 데이터 전송에만 사용하는 개체를 데이터 전공 개체(DTO)라 한다.

<br>

![](/images/Interview/post3/2021-12-15-23-17-56.png?style=centerme)

<br>

**PersonEntity Class**

```java
public final class PersonEntity{
  public UUID id;
  public String fullName;
  public String email;
  public String passwordHash;
  public String phoneNumber;
  public int balance;
  public Date createDateTime;
  public Date modifiedDateTime;

  public PeronDto toDto(){
    return new PersonDto(this.fullName, this.email, this.createdDateTime);
  }
}
```

<br>

위와 같이 구성하게 되면 웹에서 필요한 데이터만 DTO로 변환해 전달해줄 수 있다. 즉 필요없는 정보를 안 보내게 됨으로 메모리를 아끼고 보안성을 갖출 수 있는 것이다. 