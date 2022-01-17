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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Wrapper Pattern
</h2>

<br>

- 주로 업계에서는 <span style="background: rgb(251,243,219)">래퍼(wrapper) 패턴</span>이라 함
- GoF 책에서는 <span style="background: rgb(251,243,219)">어댑터(adapter) 패턴</span>이란 이름을 사용
- 어떤 클래스의 <span style="background: rgb(251,243,219)">메서드 시그내처</span>가 맘에 안 들 때 다른 걸로 바꾸는 방법
- 단, 그 클래스의 메서드 시그내처를 <span style="background: rgb(251,243,219)">직접 변경하지 않음</span>
  - 그 클래스의 <span style="background: rgb(251,243,219)">소스코드가 없을 수도 있음</span>
  - 그 클래스에 의존하는 <span style="background: rgb(251,243,219)">다른 코드</span>가 있을 수도 있음
- 그 대신 새로운 클래스를 만들어 <span style="background: rgb(251,243,219)">기존 클래스를 감쌈</span>

<br>

![](/images/Interview/post3/2021-12-15-22-25-40.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">Wrapper</span>란 포장지를 의미한다. <span style="background: rgb(251,243,219)">A 클래스</span>의 어떤 <span style="background: rgb(251,243,219)">getA()</span>라는 <span style="background: rgb(251,243,219)">메서드 시그니처</span>가 있는데 마음에 안들어서 바꾼다고 해보자. 그러면 <span style="background: rgb(251,243,219)">클래스 B</span>를 만들고 <span style="background: rgb(251,243,219)">클래스 B</span>안에 <span style="background: rgb(251,243,219)">클래스 A</span>를 포함하는 것이다. 정확히 말하면 <span style="background: rgb(251,243,219)">클래스 A</span>로부터 만든 개체를 포함하는 것이다. 그리고 앞으로 <span style="background: rgb(251,243,219)">클래스 B</span>에 있는 <span style="background: rgb(251,243,219)">getB()</span> 메서드를 호출할 건데 이게 알아서 <span style="background: rgb(251,243,219)">A의 getA()</span>를 호출해주는 것이다. 즉 내가 호출할 때는 <span style="background: rgb(251,243,219)">B</span>만 사용하고 내부적으로는 <span style="background: rgb(251,243,219)">getA()</span>를 어떻게서든 사용하는 것이다. 그래서 기존의 클래스를 감싼다고 해서 **Wrapper Pattern** 이라고 부른다.

<br>

![](/images/Interview/post3/2021-12-15-22-29-37.png?style=centerme)

<br>

위의 사진과 같이 <span style="background: rgb(251,243,219)">어댑터</span>와 같이 이해할 수도 있다. 원래 <span style="background: rgb(251,243,219)">A의 getA()</span>라는 메서드가 있었으면 <span style="background: rgb(251,243,219)">A</span>를 그대로 사용하지 않고 앞에 <span style="background: rgb(251,243,219)">B</span>라는 어댑터를 꽂는 거이다. 그럼 <span style="background: rgb(251,243,219)">A</span>에 있는 뭔가에 어댑터를 꽂았으니까 바로 접근할 수 있는 방법이 없다. 그래서 <span style="background: rgb(251,243,219)">B</span>에서 어떻게든 접속을 해서 사용을 하라는 것이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 메서드 시그니처를 바꾸려는 다양한 이유
</h3>

<br>

- 추후 외부 라이브러리를 바꿀 때 <span style="background: rgb(251,243,219)">클라이언트 코드를 변경</span>하지 않기 위해
- 그냥 사용 중인 메서드가 <span style="background: rgb(251,243,219)">코딩 표준</span>에 맞지 않아서
- 기존 클래스에 없는 <span style="background: rgb(251,243,219)">기능을 추가</span>하기 위해
- 확장된 용도: <span style="background: rgb(251,243,219)">내부 개체를 클라이언트에게 노출</span>시키지 않기 위해
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

원래 프로그램에서 <span style="background: rgb(251,243,219)">OpenGL</span>을 사용했다면(즉, 내가 클라이언트) 내 소스파일 곳곳에 이런 코드가 있을 것이다.

<br>

```java
this.graphics.clearScreen(1.f, 0.f, 0.f, 0.f);
```

<br>

그리고 추후 <span style="background: rgb(251,243,219)">DirectX</span>로 바꾸기로 결정하면 위의 코드를 찾아 고쳐야 한다.

<br>

```java
this.graphics.clear(0,0,0,255);
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

<span style="background: rgb(251,243,219)">Graphics</span> 개체만 만들고 속에 <span style="background: rgb(251,243,219)">OpenGL</span> 개체가 들어있다. <span style="background: rgb(251,243,219)">Graphics</span> 개체의 메서드만 호출한다. 이제 여기서 <span style="background: rgb(251,243,219)">OpenGL</span> 대신 <span style="background: rgb(251,243,219)">DirectX</span>를 사용하려면 어떻게 해야 할까? **Graphics** 클래스 안에서 OpenGL 개체를 <span style="background: rgb(251,243,219)">DirectX</span> 개체로 변경하면 된다.

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

**Graphics Class**

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

즉, **Graphics** 메서드들이 <span style="background: rgb(251,243,219)">DirectX</span> 메서드를 호출하게 변경한다.

<br>

그리고 추가적으로 살펴볼 것이 <span style="background: rgb(251,243,219)">DTO</span>이다. 엄밀히 말하면 <span style="background: rgb(251,243,219)">어댑터 패턴</span>은 아니지만 궁극적인 목표가 같은 <span style="background: rgb(251,243,219)">DTO</span> 개념에 대해서 살펴본다. <span style="background: rgb(251,243,219)">어댑터 패턴</span>은 타 클래스의 메서드 시그내처를 내 필요에 맞게 바꾸는 것이다. <span style="background: rgb(251,243,219)">DTO</span>는 타 클래스의 데이터를 내 필요에 맞게 바꾸는 것이다.

<br>

이제 <span style="background: rgb(251,243,219)">DTO 변환</span>하기의 간단한 예를 살펴보자. 시스템 규모가 크면 종종 이런 문제들을 겪는다.

<br>

![](/images/Interview/post3/2021-12-15-23-16-12.png?style=centerme)

<br>

DB에 저장된 데이터를 읽어와서 웹페이지에 보여준다고 가정했을 때 <span style="background: rgb(251,243,219)">PersonEntitiy의</span> <span style="background: rgb(251,243,219)">모든 정보를 반환</span>하면 필요 이상의 데이터를 반환하게 되는 것이다. 따라서 정말 클라이언트가 <span style="background: rgb(251,243,219)">필요로 하는 정보만 반환</span>하는 게 더 좋다 이때 데이터 전송에만 사용하는 개체를 <span style="background: rgb(251,243,219)">데이터 전공 개체(DTO)</span>라 한다.

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

위와 같이 구성하게 되면 웹에서 필요한 데이터만 <span style="background: rgb(251,243,219)">DTO로 변환</span>해 전달해줄 수 있다. 즉 필요없는 정보를 안 보내게 됨으로 <span style="background: rgb(251,243,219)">메모리</span>를 아끼고 <span style="background: rgb(251,243,219)">보안성</span>을 갖출 수 있는 것이다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 적응자(Adapter) 패턴
</h3>

<br>

<span style="background: rgb(251,243,219)">적응자 패턴</span>은 다른 이름으로 <span style="background: rgb(251,243,219)">래퍼(Wrapper)</span>라고 불리우는 패턴이다.

**클래스의 인터페이스를 사용자가 원하는 형태로 변환(적응) 시킨다.**

이렇게 <span style="background: rgb(251,243,219)">변환(적응)</span>을 통해서 일치하지 않는 인터페이스를 갖는 클래스들이 함께 동작할 수 있도록 한다.

<br>

### <span style="color:#2ECC40; font-weight:bold">시나리오</span>

<br>

그림 편집기가 있다.

그림판의 주요한 <span style="background: rgb(251,243,219)">추상적 개념은 그래픽 객체들</span>이다.

이런 <span style="background: rgb(251,243,219)">공통 그래픽 요소</span>에 대한 인터페이스는 <span style="background: rgb(251,243,219)">추상 클래스인 Shape</span>에 정의되어 있다.

그리고 각 그래픽 요소인 <span style="background: rgb(251,243,219)">선</span>과 <span style="background: rgb(251,243,219)">다각형</span>은 각각 **LineShape, PolygonShape**과 같은 클래스로 개발해야 한다.

<br>

위와 같이 간단한 도형도 있겠지만 **TextShape**는 텍스트 처리시 **버퍼 관리**와 같이 다른 그래픽 요소에 비해 **특별하게 고려해야할 점**이 있을 수 있다.

<br>

이때 재사용할 수 있는 라이브러리나 자원이 없을까 조사를 하게 된다.

다행히 **사용자 인터페이스 툴킷**에서 복잡한 **TextView**를 처리하는 클래스를 제공하고 있다고 **가정**하자.

당연히 재사용하는 것이 바람직하긴 하지만 **TextView**는 **Shape**를 고려해서 설계한 것이 아니라서 곧바로 **TextShape** 클래스로 대체하여 사용할 수 없다.

<br>

### <span style="color:#2ECC40; font-weight:bold">적응자 패턴의 구조</span>

<br>

<span style="background: rgb(251,243,219)">적응자 패턴</span>에는 2 가지 구현 방식이 있다.

- <span style="background: rgb(251,243,219)">TextShape(Adapter)</span>가 <span style="background: rgb(251,243,219)">Shape의 인터페이스</span>와 <span style="background: rgb(251,243,219)">TextView</span>의 구현을 모두 상속
- <span style="background: rgb(251,243,219)">TextShape(Adapter)</span> 가 <span style="background: rgb(251,243,219)">TextView의 인스턴스</span>를 포함하고, <span style="background: rgb(251,243,219)">TextView</span>의 인터페이스를 사용

<br>

아래 다이어그램은 위의 방법 중 **인스턴스를 포함한 방식**으로 적응자 패턴을 구현한 다이어그램이다.

<br>

![](/images/Interview/post16/2021-12-29-23-27-50.png?style=centerme)

<br>

위에서 <span style="background: rgb(251,243,219)">TextShape</span>은 <span style="background: rgb(251,243,219)">TextView 클래스</span>에 정의된 인터페이스를 바꾸어 <span style="background: rgb(251,243,219)">Shape 클래스</span>에 정의된 인터페이스와 잘 부합되게 한다.

이로써 <span style="background: rgb(251,243,219)">TextView</span> 클래스를 <span style="background: rgb(251,243,219)">TextShape</span> 적응자를 통해 <span style="background: rgb(251,243,219)">재사용</span>할 수 있게 되었다.

<br>

<span style="background: rgb(251,243,219)">적응자 패턴</span>의 <span style="background: rgb(251,243,219)">참여자</span>는 아래와 같다.

<br>

<span style="color:#3D9970; font-weight:bold">Client(DrawingEditor):</span> **Target** 인터페이스를 만족하는 객체와 동작할 대상

<span style="color:#3D9970; font-weight:bold">Target(Shape):</span> 사용자(Client)가 사용하는데 필요한 인터페이스를 정의한 클래스가

<span style="color:#3D9970; font-weight:bold">Adaptee(TextView):</span> 인터페이스에 적응이 필요한 기존 인터페이스, 적응 대상자

<span style="color:#3D9970; font-weight:bold">Adapter(TextShape):</span> **Target** 인터페이스에 **Adaptee**의 인터페이스를 적응 시키는 클래스

<br>

### <span style="color:#2ECC40; font-weight:bold">Java Example</span>

<br>

**DrawingEditor.java(Client)**

```java
public class DrawingEditor {

	public void useShape(Shape shape) {

		shape.boundingBox();
		shape.createManipulator();
	}
}
```

<br>

**Shape Interface(Target)**

```java
public interface Shape {

	void boundingBox();

	void createManipulator();
}
```

<br>

**Line.java(평범한 클래스)**

```java
public class Line implements Shape {

	@Override
	public void boundingBox() {
		System.out.println("Line bounding box");
	}

	@Override
	public void createManipulator() {
		System.out.println("Line create manipulator");
	}
}
```

<br>

**TextView Interface(Adaptee)**

```java
public interface TextView {

	void getExtent();
}
```

<br>

**TextShape.java(Adapter)**

```java
public class TextShape implements Shape{

	private TextView text;

	public TextShape(TextView text) {
		super();
		this.text = text;
	}

	@Override
	public void boundingBox() {

		text.getExtent();
		System.out.println("TextShape bounding box.");
	}

	@Override
	public void createManipulator() {
		System.out.println("TextShape create manipulator.");
	}
}
```

<br>

**TextShape** 클래스는 **Adaptee**인 **TextView**를 생성자의 인자를 통해 받아서 속성에 설정하였다.

**boundingBox()** 메서드에서 **Adaptee**인 **TextView**의 메서드를 이용하여 기능을 구현하고 있다.

이 패턴의 참여자들을 이용하여 작성한 Main 코드는 아래와 같다.

<br>

**Main**

```java
public static void main(String[] args) {

		DrawingEditor drawingEitor = new DrawingEditor();

		Shape lineShape = new Line();

		TextView text = () -> {
			System.out.println("getExtent called in Text View");
		};
		Shape textShape = new TextShape(text);

		System.out.println("====DrawingEditor use line shape.====");
		drawingEitor.useShape(lineShape);
		System.out.println();

		System.out.println("====DrawingEditor use text shape.====");
		drawingEitor.useShape(textShape);
	}
```

<br>

<span style="background: rgb(251,243,219)">lineShape</span>는 특별한 것이 없다.

우리가 작성한 코드에서 <span style="background: rgb(251,243,219)">adaptee</span>인 <span style="background: rgb(251,243,219)">TextView</span>는 <span style="background: rgb(251,243,219)">인터페이스만 정의</span>하였고, 구현체는 없었다.

<span style="background: rgb(251,243,219)">TextView</span>는 추상 method가 1개인 <span style="background: rgb(251,243,219)">FunctionalInterface</span> 이기 때문에 <span style="background: rgb(251,243,219)">익명함수</span>를 이용하여 <span style="background: rgb(251,243,219)">구현체 text</span>를 생성하였다.

그리고 <span style="background: rgb(251,243,219)">adapter</span>인 <span style="background: rgb(251,243,219)">TextShape</span>에서 <span style="background: rgb(251,243,219)">TextView</span> 를 생성자 인자로 받으므로, text를 인자로 넘겨주었다.

<br>

```
====DrawingEditor use line shape.====
Line bounding box
Line create manipulator

====DrawingEditor use text shape.====
getExtent called in Text View
TextShape bounding box.
TextShape create manipulator.
```
