---
layout: post
title: 디자인 패턴-Factory Method
date: 2021-12-14 10:00:00 0000
tags: [Design Pattern, Factory Method]
categories: [Interview]
description: Factory Method에 대해 알아보자
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

# <center>Design Pattern-Factory Method</center>

<br>

이번에는 면접 때 나올 수 있는 디자인 패턴에 관한 포스트를 해볼까 한다. 모든 디자인 패턴을 다 다루진 않는다. 디자인 패턴 중에 자주 쓰이거나 질문으로 나올 법한 것을 추려봤다. 해당 내용은 내가 좋아하는 유투버 **Pope**님의 **개체지향** 강의에서 나온 부분을 기록해 보려한다.

# Factory Method

<br>

- 사용할 클래스를 정확히 몰라도 개체 생성을 가능하게 해주는 패턴
- 정확히 어떤 클래스를 사용해서 개체를 생성해야 되는지 몰라도 됨
- 부모 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴
- 개체의 생성 코드를 별도의 클래스/메서드로 분리함으로써 개체 생성의 변화에 대비하는 데 유용

<br>

코드를 보며 이해해보자 아래 코드는 버거 자동 주문 기계이다. 거기서 음료 주문을 할 때 컵 크기를 고른다. 고객은 스몰, 미디엄, 라지를 선택할 뿐 실제 컵 용량(ml)을 모른다

<br>

**Cup Class**

```java
public final class Cup{
  private int sizeMl;
  private Cup(int sizeMl){
    this.sizeMl=sizeMl;
  }
  public static Cup createOrNull(CupSize size){
    switch(size){
      case SMALL:
        return new Cup(355);
      case MEDIUM:
        return new Cup(473);
      case LARGE:
        return new Cup(651);
      default:
        assert (false) : "Unhandled CupSize:" + size;
        return null;
    }
  }
}
```

<br>

**CupSize Enum**

```java
public enum CupSize{
  SMALL,
  MEDIUM,
  LARGE
}
```

<br>

Cup 클래스의 생성자는 private이다. 즉 Cup 클래스의 개체를 직접 생성할 수 없다. createOrNull() 정적 메서드에서 switch 문을 통해 Cup 개체를 생성해주는 것을 볼 수 있다.

<br>

**생성자 대신 정적 메서드를 사용하는 것의 장점**

- null을 반환 가능
- 생성자는 생성이 불가능한 경우 예외를 던질 수밖에 없음
  - 반환형이 없기 때문

<br>

아직 팩토리 메서드가 완성된 것은 아니다. 여기서 만약 모든 나라에서 사용할 수 있는 기계를 만든다면 어떻게 해야 할까? 즉 나라마다 small, medium, large의 크기가 다르다. 같은 large여도 나라마다 다르기 때문에 이를 구현하고 싶은 것이다. 두가지 방법으로 이를 해결할 수 있다.

<br>

1. createOrNull()의 매개변수에 나라도 넣어준다.
2. createOrNull()을 다형적으로 만든다.

<br>

여기서 2번 방법으로 해본다. 그러나 static 메서드를 다형적으로 만들 수 없다 그래서 자식 클래스를 만들어야 한다. 구조는 아래 사진과 같이 된다.

<br>

![](/images/Interview/post2/2021-12-14-22-53-10.png?style=centerme)

<br>

위 사진을 보면 Cup 클래스의 생성자가 private에서 패키지 접근제어자로 바뀌었다. 즉 같은 패키지에 있는 누군가가 new를 해준다는 것이다. 즉 KoreanMenu와 AmericanMenu 클래스만 Cup 개체를 생성하게끔 해준다.(같은 패키지에 있으므로) 다시 Cup 클래스를 구성해보자.

<br>

**Cup Class**

```java
public final class Cup{
  private int sizeMl;

  Cup(int sizeMl){
    this.sizeMl=sizeMl;
  }

  public int getSize(){
    return this.sizeMl;
  }
}
```

<br>

위에서 createCupOrNull() 메서드가 빠진다.

<br>

**Menu Class**

```java
public abstract class Menu{
  //다른 메서드는 생략
  public abstract Cup createCupOrNull(CupSize size);
}
```

<br>

위의 Menu Class를 인터페이스 대신 추상 클래스로 만든 것은 Menu라는 특성상 멤버 데이터가 들어갈 가능성이 많아서이다.

<br>

이제 createCupOrNull() 메서드는 가상 생성자가 된 꼴! 다른 나라를 지원하려면 자식 클래스를 추가하면 된다.

<br>

**AmericanMenu Class**

```java
public final class AmericanMenu extends Menu{
  @Override
  public Cup createCupOrNull(CupSize size){
    switch(size){
      case SMALL:
        return new Cup(473);
      case MEDIUM:
        return new Cup(621);
      case LARGE:
        return new Cup(887);
      default:
        assert (false) : "Unhandled CupSize:"+size;
        return null;
    }
  }
}
```

<br>

**KoreanMenu Class**

```java
public final class KoreanMenu extends Menu{
  @Override
  public Cup createCupOrNull(CupSize size){
    switch(size){
      case SMALL:
        return new Cup(355);
      case MEDIUM:
        return new Cup(473);
      case LARGE:
        return new Cup(651);
      default:
        assert (false) : "Unhandled CupSize:"+size;
        return null;
    }
  }
}
```

<br>

이제 컵을 생성해보자!

<br>

**Main Class**

```java
Menu menu=new KoreanMenu();
Cup cup=menu.createCupOrNull(CupSize.LARGE);

System.out.println(cup.getSize());
```

<br>

651이 찍힌다.

<br>

```java
Menu menu=new AmericanMenu();
Cup cup=menu.createCupOrNull(CupSize.LARGE);

System.out.println(cup.getSize());
```

<br>

887이 찍힌다.

<br>

반환하는 Cup도 추상적으로 만들 수 있다. 예를 들어 각 나라의 법규에 따라 사용하는 컵 종류가 다르다고 해보자 어떤 나라는 1회용 종이컵을 사용하고 어떤 나라는 반드시 유리컵을 사용해본다고 해보자. 그러면 Cup 클래스를 아래와 같이 수정할 수 있다.

<br>

![](/images/Interview/post2/2021-12-14-23-13-27.png?style=centerme)

<br>

**Cup Class**

```java
public abstract class Cup{
  private int sizeMl;

  protected Cup(int sizeMl){
    this.sizeMl=sizeMl;
  }

  public int getSize(){
    return this.sizeMl;
  }
}
```

<br>

**GlassCup Class**

```java
public final class GlassCup extends Cup{
  GlassCup(int sizeMl){
    super(sizeMl);
  }
}
```

<br>

**PaperCup Class**

```java
public final class PaperCup extends Cup{
  private Lid lid;
  PaperCup(int sizeMl, Lid lid){
    super(sizeMl);
    this.lid=lid;
  }
}
```

<br>

**AmericanMenu Class**

```java
public final class AmericanMenu extends Menu{
  @Override
  public Cup createCupOrNull(CupSize size){
    Lid lid= new Lid(size);
    switch(size){
      case SMALL:
        return new PaperCup(473, lid);
      case MEDIUM:
        return new PaperCup(621, lid);
      case LARGE:
        return new PaperCup(887, lid);
      default:
        assert (false) : "Unhandled CupSize:"+size;
        return null;
    }
  }
}
```

<br>

**KoreanMenu Class**

```java
public final class KoreanMenu extends Menu{
  @Override
  public Cup createCupOrNull(CupSize size){
    switch(size){
      case SMALL:
        return new GlassCup(355);
      case MEDIUM:
        return new GlassCup(473);
      case LARGE:
        return new GlassCup(651);
      default:
        assert (false) : "Unhandled CupSize:"+size;
        return null;
    }
  }
}
```

<br>

**Main Class**

```java
Menu menu=new KoreanMenu();
Cup cup=menu.createCupOrNull(CupSize.LARGE);

System.out.println(cup.getClass().getName());
System.out.println(cup.getSize());
```

<br>

academy.pocu.GlassCup
651
이 찍힌다.

<br>

```java
Menu menu=new AmericanMenu();
Cup cup=menu.createCupOrNull(CupSize.LARGE);

System.out.println(cup.getClass().getName());
System.out.println(cup.getSize());
```

<br>

academy.pocu.PaperCup
887
이 찍힌다.

<br>

### Factory Method 장점

- 다형적으로 개체 생성 가능 따라서 이 패턴을 가상 생성자 패턴이라고도 함
- 생성자에서 오류 상황 감지 시 null 반환 가능
- 클라이언트는 본인에게 익숙한 인자를 통해 개체 생성 가능