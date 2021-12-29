---
layout: post
title: 디자인 패턴-Builder Pattern
date: 2021-12-14 11:00:00 0000
tags: [Design Pattern, Builder Pattern]
categories: [Interview]
description: Builder Pattern에 대해 알아보자
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

# <center>Design Pattern-Builder Pattern</center>

<br>

_해당 내용은 POCU 아카데미 COMP_2500에서 배운 내용을 공부하기 위해 작성된 글입니다_

<br>

### Builder Pattern

- 개체의 생성과정을 그 개체의 클래스로부터 분리하는 방법
- 개체의 부분부분을 만들어 나가다 준비되면 그제서야 개체를 생성
  - 비유: 벽돌을 하나씩 쌓아 담장을 만드는 과정
- 다형성이 없는 빌더는 StringBuilder에서도 볼 수 있다.

<br>

다형성이 없는 빌더인 StringBuilder를 한번 살펴보자. 처음에 자바 언어를 하며 문자열을 접하게 되면 String을 사용하게 될 것이다. 하지만 복잡한 문서는 String으로 만들기가 힘들다. 즉 복잡한 문서를 String으로 한 방에 만들려면 꽤 까다롭다. '+' 연산을 통해 String을 더해가는 것은 많은 비용이 들어 속도에 느리다. 하지만, String.format()를 사용하면 어느 정도 비용을 감소할 수 있지만 서식 문자열이 매우 복잡해지고 가독성이 안 좋다. 이는 StringBuilder를 사용하면 어느 정도 편하다.

<br>

오버로딩된 append() 덕분에 String 외에 다른 것도 추가하기 쉽고 내부에서 알아서 효율적으로 문자열을 합쳐준다. 단 내부가 어떻게 작동하는지 알면 좋은 점이 있다. **StringBuilder** 생성 시 어떤 매개변수를 전달해야 유리할까? 이것은 내부를 알면 알 수 있을 것이다. StringBuilder는 append를 다 하고 나서 **toString()** 메서드를 호출해주면 String을 반환한다.

<br>

```java
builder.append(heading);
builder.append(newLine);
builder.append(newLine);
```

<br>

코드가 깔끔하게 읽히나 작성자의 의도가 명확하지 않다. 예를 들어 작성자가 제목(heading)을 넣고 줄을 바꾸고(newLine) 싶다고 해보자. 위 코드에서 그 의도가 명확히 보이지 않는다. 오히려 서로 다른 3개를 추가하는 느낌이다.

<br>

이를 위해 **플루언트 인터페이스(fluent interface)**가 해결 방안이 될 수 있다. 요즘은 빌더 패턴을 구현시 종종 플루언트 인터페이스도 지원한다. 예를 한번 보자.

<br>

```java
StringBuilder builder=new StringBuilder(1024*1024);
builder.append(heading)
       .append(newLine)
       .append(newLine);

builder.append(leadingParagraph)
       .append(newLine);

for(KeyValue kv : data){
  builder.append(" * ")
         .append(kv.getKey())
         .append(": ")
         .append(kv.getValue())
         .append(newLine));

...

String document=builder.toString();

```

<br>

이렇게 **.append()**를 이어서 쓸 수 있는 이유는 this 즉, builder 자기자신을 반환하기 때문이다.
자기 스스로를 반환하는 건 함수 시그내처 측면에서는 이상할 수도 있으나 플루언트 인터페이스는 이제 프로그래머의 상식이 되었다. 다시 빌더 이야기로 돌아가 보자.

<br>

또다른 예를 보자.

<br>

**Employee Class**

```java
public final class Employee{
  private String firstName;
  private String lastName;
  private int id;
  private int yearStarted;
  private int age;

  public Employee(String firstName, String lastName, int id, int yearStarted, int age){
    this.firstName=firstName;
    this.lastName=lastName;
    this.id=id;
    this.yearStarted=yearStarted;
    this.age=age;
  }
}
```

<br>

**Main Class**

```java
Employee pope=new Employee("Pope", "Kim", 30,2020,30);
Employee robert=new Employee("Lee", "Robert", 31,2020,1);
```

<br>

컴파일과 실행이 되지만 위의 코드엔 버그가 있다. 두 번째 Robert 개체를 한번 살펴보자. 자세히 보면 firstName과 lastName의 위치가 바뀌었다. 나이와 ID도 바뀌었다. <span style="color:orange; font-weight:bold">이것은 컴파일러가 잡아줄 수 있는 문제가 아니다. 컴파일러는 자료형이 안 맞는 정도이지 형이 같은 매개변수가 있는 것은 잡아주지 못한다.</span>

<br>

이 문제를 빌더 클래스로 해결해 보자.

<br>

```java
Employee robert=new EmployeeBuilder(1)
         .withAge(31)
         .withStartingYear(2020)
         .withName("Robert", "Lee")
         .build();
```

<br>

위 코드는 메서드 이름이 명확하기 때문에 잘못된 값을 전달할 확률이 적다. 그러나 여기서도 문제가 발생한다. <span style="color:orange; font-weight:bold">호출자가 실수하면 이런 문제가 발생한다</span>

<br>

```java
Employee robert=new EmployeeBuilder(1)
         .withAge(31)
         .withName("Robert", "Lee")
         .build();
```

<br>

즉 서기 0년부터 일하기 시작한 초고인물 직원이 등장하게 된다. 개체는 생성부터 유효한 상태여야 한다는 원칙이 어긋나게 된다. 디자인 패턴을 잘못 사용하는 경우가 많은데 이게 바로 그 예 중에 하나이다. 근데 이런 식으로 만든 SDK들이 정말 많아졌다. Goo\*\*\* 사의 SDK 조차도 이런 식의 빌더 패턴을 사용한다.

<br>

StringBuilder는 유효한 개체만 반환했다. 어느 상황에서 toString()을 호출해도 유효한 String 개체가 나온다. 따라서 이건 올바르게 빌더 패턴을 구현한 경우라고 할 수 있다. 자 그러면 위의 방법보다 어떤 방법을 쓰는 것이 나은가? 바로 **매개변수 클래스**를 이용하는 것이다.

<br>

**Employee Class**

```java
public final class Employee{
  private String firstName;
  private String lastName;
  private int id;
  private int yearStarted;
  private int age;

  public Employee(CreateEmployeeParams params){
    this.firstName=params.firstName;
    this.lastName=params.lastName;
    this.id=params.id;
    this.yearStarted=params.yearStarted;
    this.age=params.age;
  }
}
```

<br>

**CreateEmployeeParams Class**

```java
public final class CreateEmployeeParams{
  public String firstName;
  public String lastName;
  public int id;
  public int yearStarted;
  public int age;
}
```

<br>

위의 CreateEmployeeParams 이라는 구조체 역할을 하는 클래스를 만든다.

<br>

**Main Class**

```java
CreateEmployeeParams params=new CreateEmployeeParams();
params.firstName="Robert";
params.lastName="Lee";
params.id=1;
params.age=31;
params.yearStarted=2020;

Employee robert=new Employee(params);
```

<br>

이런 식으로 하면 생성자에 인자 순서를 잘못 넣는 경우를 해결할 수 있다. 하지만 여전히 실수로 age를 안 넣는 등의 문제는 있을 수 있다. 하지만 빌더 패턴의 방식으로 개체를 생성하는 것보다 훨씬 낳은 방법이다.

<br>

이제 빌더 패턴을 다형적으로 확장해보자. 지금까지 본 빌더 패턴은 언제나 동일한 클래스의 개체를 반환한다. 하지만 다형적인 빌더 패턴을 사용할 경우 다른 개체를 반환한다. 

<br>

이번 예에서는 .csv 파일이 있다고 가정한다. 이 .csv 파일은 표로 쉽게 표현 가능하다 .csv 파일을 다음 둘 중 하나로 변화하고 싶은 것이다.

- HTML 표
- markdown 포맷 표

<br>

아래 사진을 통해 클래스 다이어그램을 보자.


<br>

![](/images/Interview/post2/2021-12-15-00-25-38.png?style=centerme)

<br>

**HTML 혹은 markdown 표로 변환하기**

```java
CsvReader reader=new CsvReader(csvText);
HtmlTableBuilder buider=new HtmlTableBuilder();

reader.writeTo(builder);

HtmlDocument html=builder.toHtmlDocument();
```

<br>

```java
CsvReader reader=new CsvReader(csvText);
MarkdownTableBuilder builder=new MarkdownTableBuilder();

reader.writeTo(builder);

String mdText=builder.toMarkDownText();
```

<br>

위 두 코드의 차이점은 하나는 HtmlTableBuilder 클래스와 MarkdownTableBuilder 클래스 밖에 없다. 즉 원하는 포맷에 맞는 구체 빌더 클래스의 개체를 생성한다. 

csvText는 csv 파일의 문자열을 넣어준다고 보면 된다. **CsvReader** 클래스의 **writeTo** 메서드는 파라미터로 TableBuilder 클래스 타입으로 가지고 있다. 이는 즉 **TableBuilder**의 자식 클래스 타입을 받을 수 있게 되는 것이다. 

**reader.writeTo(builder)** 부분에서 builder를 호출해주면 자체적으로 "한 줄 더하거나" "한 column 를 더하거나" 하는 작업을 할 것이다. 즉 builder가 자기 포맷에 맞게 알아서 build해 나아갈 것이다.

<br>

**writeTo() 메서드 의사 코드**

- 첫 줄을 읽음
- 빌더의 addHeadingRow() 메서드를 호출
- 읽은 줄을 쉼표에 따라 토큰화
- 토큰 배열을 foreach 문으로 돌면서 빌더의 addColumn(token)을 호출
- 나머지 줄을 한 줄씩 읽으면서 다음의 과정을 반복
  - 빌더의 addRow() 메서드를 호출
  - 각 토큰마다 빌더의 addColumn(token)을 호출

<br>

위 코드에서 **reader.writeTo(builder)**가 호출되고 끝나는 순간 **builder 안에는** 모든 필요한 구성요소가 만들어졌다는 것이다. 그러면 그것을 최종 문서로 뽑아내기만 하면 된다. 그리고 마지막에 **builder.toHtmlDocument**과 **builder.toMarkDownText**으로 최종 문서로 뽑아낸다. 

```java
HtmlDocument html=builder.toHtmlDocument();
```
과
```java
String mdText=builder.toMarkDownText();
```

부분은 **다형적 함수 호출이 아니다!**

**실제 빌더 개체의 레퍼런스를 들고 있기에 가능한 것이다**


<br>

### **빌더 패턴 장점**

<br>

- 필요한 데이터만 설정할 수 있음
  - 예를 들어 User 객체를 생성해야 하는데 age라는 파라미터가 필요 없는 상황
    - 생성자나 정적 메서드였으면 age에 더미 값을 넣어주거나 age가 없는 생성자 필요
- 유연성을 확보할 수 있음
  - 클래스에 새로운 변수가 추가되야 하는 상황에 직면해도 기존 코드에 영향을 주지 않음
- 가독성을 높일 수 있음
