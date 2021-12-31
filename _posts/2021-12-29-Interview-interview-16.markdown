---
layout: post
title: Java Garbage Collector와 JVM 구조
date: 2021-12-30 11:00:00 0000
tags: [Garbage Collector, JVM]
categories: [Interview]
description: JVM의 구조 및 GC에 대하여
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

<br>

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Garbage Collector & JVM
</h2>

<br>

GC(Garbage Collector)에 대해서 이야기 하기 전에 먼저 JVM의 구조를 아는 것이 중요하다.

그래서 GC를 설명하기 전에 JVM을 먼저 살펴보자.

![](/images/Interview/post16/2021-12-30-14-20-57.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> JVM의 역할
</h3>

<br>

- 자바 애플리케이션을 Class Loader를 통해 읽어 들여 자바 API와 함께 실행
- JVM은 Java와 OS 사이에서 중개자 역할을 수행
  - JAVA가 <span style="background: rgb(251,243,219)">OS에 독립적</span>으로 실행 및 재사용을 가능하게 함
- <span style="background: rgb(251,243,219)">메모리 관리, GC을 수행</span>
- 스택기반의 가상머신
  - ARM 아키텍쳐 같은 하드웨어는 레지스터 기반으로 동작하는데 비해 JVM은 스택기반으로 동작한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> JVM의 구조
</h3>

<br>

- .class 파일 = 바이트 코드
- byte 코드 → JVM과 같은 가상 머신이 이해할 수 있는 코드 - binary 코드
  - CPU가 이해할 수 있는 코드가

<br>

### **Class Loader**

<br>

바이트 코드를 읽어오며 메모리에 적절히 배치하는 역할

<br>

- **로딩:** .class 파일을 읽어온다.
- **링크:** 코드 내부의 래퍼런스를 연결
- **초기화:** 클래스에 있는 static 값들을 초기화

<br>

### **Runtime Data Area(Memory)**

<br>

JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역이다.

<br>

![](/images/Interview/post16/2021-12-30-14-48-28.png?style=centerme)

<br>

전체 공유 자원

<br>

### **[Method Area, Heap Area]**

- **Method:** 클래스 수준의 정보 저장
  - 클래스 멤버 변수, 클래스 메소드 정보, Type(Class or interface)정보, Constant Pool, static, final 변수 등이 생성된다.
  - Class의 메타 정보를 저장.(Field 이름, Field 타입, Class 이름 등등)
- **Heap:** 객체(인스턴스) 수준의 정보 저장
  - <span style="background: rgb(251,243,219)">GC의 주요 대상</span>
  - 흔히 코드에서 'new' 명령어를 통해 생성된 인스턴스 변수가 놓인다.
  - 스택영역에 저장되는 로컬 변수, 매개변수와 달리 힙영역에서 보관되는 메모리는 메소드 호출이 끝나도 사라지지 않고 유지된다.
    - (언제까지?) 주소를 읽어버려 가비지가 되어 GC에 의해 지워질 때까지 아니면 JVM이 종료될 때까지

<br>

### **[Stack Area, PC register, Native Method Stack]**

쓰레드 단위로 하나씩 생성된다.

- **Stack:** 인스턴스 및 지역 변수의 <span style="background: rgb(251,243,219)">참조 주소</span>들을 저장

  - JVM 시작 시 생성되고 프로그램 종료될 때까지 유지된다.
  - 로컬변수와 매개변수의 특징은 선언된 블록 안에서만 유효한 변수들이고 이것이 스택영역에 저장되는 것이다.

  <br>

  <link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
  <div style="background: #eee;
    box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

  클래스 Person p=new Person(); 이라는 소스를 작성했다면 Person p는 스택 영역에 생성되고 new로 생성된 Person 클래스의 인스턴스는 힙 영역에 생성된다.<br> 스택영역에 생성된 p의 값으로 힙 영역의 주소값을 가지고 있다.<br>→ 즉, 스택 영역에 생성된 p가 힙 영역에 생성된 객체를 가리키고(참조하고) 있는 것</div>

<br>

- **PC register:** 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역
  - 네이티브 메소드는 java가 아닌 low-level로 구현된 메소드<br>
  - Thread 마다 하나씩 존재하고 **Native Pointer**와 **Return Address**를 가지고 있음
  - 즉, PC register는 Thread가 어떠한 명령을 실행하게 될지에 대한 부분을 기록
    ex. Thread.currentThread()

<br>

### **Execution Engine**

<br>

- **인터프리터**
  - 바이트 코드를 한줄 한줄 읽어서 네이티브 코드로 변환
- **JIT(Just In Time) 컴파일러**
  - 바이트 코드에서 반복되는 코드 부분은 JIT 컴파일러가 미리 네이티브 코드로 변환시켜 놓음
  - 반복되는 코드가 읽힐 순서가 왔을 때, 인터프리터로 읽지 않고 바로 네이티브 코드를 바로 사용한다.
  - 인터프리터 읽을 때의 속도 효율성을 JIT 컴파일러가 보완하는 형태
- **GC(Garbage Collector)**
  - 더 이상 참조되지 않는 객체를 모아서 메모리 정리를 한다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Gargabe Collector
</h3>

<br>

Java에서의 GC는 기본적으로 <span style="background: rgb(251,243,219)">Mark And Sweep</span> 방식으로 돌아간다.

<span style="background: rgb(251,243,219)">Mark And Sweep</span> 방식으로 GC를 실행할 경우 2가지 특징이 있다.

<br>

1. 의도적으로 GC를 실행시켜야 한다.
2. 애플리케이션 실행과 GC 실행이 병행된다.

<br>

**가바지는 사용되지 않는 객체를 말한다.**

<br>

### **JVM에서 Root set이 어딜까?**

<br>

![](/images/Interview/post16/2021-12-30-16-03-00.png?style=centerme)

<br>

Mark And Sweep 알고리즘은 **Root Space**로부터 동적 메모리 영역의 객체 접근이 가능한지를 해제의 기준으로 둔다.

Root Space에서부터 해당 객체에 접근이 가능하다면 메모리에 유지시키고, 접근이 불가능하다면 메모리에서 지워버리는 방식인 것이다.

<br>

**그렇다면 JVM의 Root Space는 어디일까?**

<br>

Heap 영역 메모리에 대한 참조를 들고 있을 수 있는 영역일 것이다.

JVM Memory 영역 중에서는 다음과 같다.

<br>

1. _Stack의 로컬 변수_
2. _Method Area의 Static 변수_
3. _Native Method Stack의 JNI 참조_

<br>

아래 그림을 참고하자.

<br>

![](/images/Interview/post16/2021-12-30-16-04-49.png?style=centerme)

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Mark and Sweep
</h3>

<br>

Root가 참조하는 모든 객체, 또 그 객체들이 참조하는 객체들을 탐색해 내려가며 할당받은 각 메모리 영역에 1비트씩 남겨서 사용 중을 표시(Mark) 한다. 이게 바로 GC의 첫 번째 단계인 **Mark** 단계이다.

<br>

![](/images/Interview/post16/2021-12-31-20-35-01.png?style=centerme)

<br>

Mark가 끝나면 GC는 힙 내부 전체를 돌면서 Mark 되지 않은 메모리들을 해제한다. 이 과정을 **Sweep**라고 부른다.

<br>

![](/images/Interview/post16/2021-12-31-20-35-44.png?style=centerme)

<br>

**Mark and Sweep Algorithm**의 단점은 GC를 수행하는 동안 **Stop the World**가 발생한다는 것이다.

- **Stop The World:** Stop The World는 가비지 컬렉션을 실행하기 위해 JBM이 애플리케이션의 실행을 멈추는 작업이다. GC가 실행될 때는 GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업이 중단되고 GC가 완료되면 작업이 재개된다. 당연히 모든 쓰르데들의 작업이 중단되면 애플리케이션이 멈추기 때문에, GC의 성능 개선을 위해 튜닝을 한다고 하면 보통 stop-the-world의 시간을 줄이는 작업을 하는 것이다. 

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 힙(Heap) 영역의 구조와 가비지 컬렉션 프로세스
</h3>

<br>

힙 영역은 **Old, Eden, S0, S1** 총 네 개 영역으로 나눌 수 있다.

인스턴스의 메모리 할당 측면에서 성능을 높이려고 용도를 구분해둔 것이다.

<br>

![](/images/Interview/post16/2021-12-31-20-45-12.png?style=centerme)

<br>

- **Metaspace:** 클래스 메타 데이터를 native 메모리에 저장하고 메모리가 부족할 경우 이를 자동으로 늘려주는 공간을 말한다.

<br>

힙은 Young, Generation, Old Generation으로 크게 두 개의 영역으로 나누어 지고, Young Generation은 또다시 Eden, Survivor Space 0, 1로 세분화 되어진다. S0, S1 으로 표시되는 영역이 Survivor Space 0, 1이다. 각 영역의 역할은 가비지 컬렉션 프로세스를 알면 알 수 있다.

<br>

**(1)** 새로운 객체는 **Eden** 영역에 할당된다. 두 개의 **Survivor Space**는 비워진 상태로 시작한다.

<br>

![](/images/Interview/post16/2021-12-31-20-53-18.png?style=centerme)

<br>

**(2)** Eden 영역이 가득 차면, **MinorGC(Young Generation을 대상으로 하는 GC)가 발생한다.

<br>

**(3)** MinorGC가 발생하면, Reachable 객체들은 S0으로 옮겨진다. Unreachable 객체들은 Eden 영역이 클리어 될 때 함께 메모리에서 사라진다.

<br>

![](/images/Interview/post16/2021-12-31-20-55-05.png?style=centerme)

<br>

**(4)** 다음 MinorGC 가 발생할 때, Eden 영역에는 3번과 같은 과정이 발생한다. Unreachable 객체들은 지워지고, Reachable 객체들은 Survivor Space로 이동한다. 기존에 S0에 있었던 Reachable 객체들은 S1으로 옮겨지는데, 이때, age 값이 증가되어 옮겨진다. 살아남은 모든 객체들이 S1 으로 모두 옮겨지면, S0와 Eden 은 클리어 된다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Survivor Spae 간의 이동마다 age 값이 증가한다. JVM 중 가장 일반적인 HotSpot JVM의 경우 이 age의 기본 임계값은 31이다. 객체 헤더에 age를 기록하는 부분이 6 bit로 되어 있기 때문이다. 아래 그림은 S0(From)에서 age가 1이었던 객체들이 S1(To)로 이동하면서 2로 증가한 예시이다.</div>

<br>

![](/images/Interview/post16/2021-12-31-20-56-55.png?style=centerme)

<br>

**(5)** 다음 MinorGC가 발생하면, 4번 과정이 반복되는데 S1이 가득 차 있었으므로 S1에서 살아남은 객체들은 S0으로 옮겨지면서 Eden과 S1은 클리어 된다. 이때도 age값이 증가되어 옮겨진다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Survivor 영역 중 하나는 반드시 비어 있는 상태로 남아 있어야 한다. 만약 두 Survivor 영역에 모두 데이터가 존재하거나, 두 영역 모두 사용량이 0이라면 여러분의 시스템은 정상적인 상황이 아니라고 생각하면 된다.</div>

<br>

![](/images/Interview/post16/2021-12-31-20-58-28.png?style=centerme)

<br>

**(6)** Young Generation에서 계속해서 살아남으며 age 값이 증가하는 객체들은 age 값이 특정값 이상이 되면 Old Generation(Java 8까지는 Tenured Generation라 부름)으로 옮겨지는데 이 단계를 **Promotion**이라고 한다.

<br>

![](/images/Interview/post16/2021-12-31-20-59-18.png?style=centerme)

<br>

그렇기 때문에 MinorGC가 계속해서 반복된다면 Promotion 작업도 꾸준히 발생하게 된다.

<br>

![](/images/Interview/post16/2021-12-31-21-00-15.png?style=centerme)

<br>

**(7)** Promotion 작업이 계속해서 반복되면서 **Old Generation**이 가득 차게 되면 **MajorGC**(Old Generation을 대상으로 하는 GC)가 발생하게 된다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Young 영역은 일반적으로 Old 영역보다 크키가 작기 때문에 GC가 보통 0.5초에서 1초 사이에 끝난다. 그렇기 때문에 Minor GC는 애플리케이션에 크게 영향을 주지 않는다. 하지만 Old 영역은 Young 영역보다 크며 Young 영역을 참조할 수도 있다. 그렇기 때문에 Major GC는 일반적으로 Minor GC보다 시간이 오래걸리며, 10배 이상의 시간을 사용한다.

</div>

<br>

![](/images/Interview/post16/2021-12-31-21-01-20.png?style=centerme)

<br>

![](/images/Interview/post16/2021-12-31-21-03-31.png?style=centerme)

<br>

---

<br>

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Garbage Collection의 종류
</h2>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Serial GC
</h3>

<br>

- Mark-Sweep-Compact 알고리즘 사용
- 적은 메모리와 CPU 코어 갯수가 적을 때 적합

<br>

Old 영역에 살아있는 객체를 Mark하고 Heap의 앞부분부터 살아있는 객체를 Sweep한 뒤 힙의 앞부분부터 객체를 쌓는다.(Compact) 메모리와 CPU 코어수가 적을 때 좋다.

<br>

1. mark 단계에서는 old 영역에서 살아있는 객체를 확인한다.
2. sweep 단계에서는 heap 영역의 앞부분부터 확인하여 표시된 객체를 제거한다.
3. compact 단계에서는 메모리 단편화를 방지하기 위해 힙의 앞부분부터 객체를 채워 넣는다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Parallel GC
</h3>

<br>

- Serial GC와 알고리즘은 같지만 GC를 처리하는 Thread가 여러 개이다.
- 메모리와 코어가 충분할 때 적합하다.

<br>

Serial GC와 기본적인 알고리즘은 같지만, GC를 처리하는 Thread의 개수가 여러 개다. 메모리와 CPU 코어 수가 많을수록 좋다. Java 8 버전에서 default로 사용되는 gc이다.

<br>

![](/images/Interview/post16/2021-12-31-21-29-52.png?style=centerme)

<br>

이는 Parallel GC 에서의 GC 프로세스가 더 빠르게 동작할 수 있게 해주며 이러한 차이는 GC를 처리하는 동안 Java의 프로세스가 모두 멈춰버리는 Stop-The-World 현상이 나타나는 시간에도 영향을 주게된다. 즉, STW(Stop-The-World) 시간이 좀 더 적게 걸리는 Parallel GC에서의 Java 애플리케이션이 좀 더 매끄럽게 동작한다는 의미이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Paraelle Old GC
</h3> 

<br>

- Parallel GC에서 Old GC 알고리즘을 개선한 버전이다.
- Mark-Summary-Compact 알고리즘을 사용하며 좀 더 복잡하다.

<br>

Mark-Sweep-Compact 방식은 단일 쓰레드가 old 영역을 검사하는 방식이라면 mark-summary-compact 방식은 여러 쓰르데를 사용해서 old 영역을 탐색한다.

<br>

1. mark 단계에서는 old 영역을 region 별로 나누고 region 별로 살아있는 객체를 식별한다.
2. summary 단계에서는 region 별 통계정보로 살아있는 객체의 밀도가 높은 부분이 어디까지 인지 dense prefix를 정한다. 오랜 기간 참조된 객체는 앞으로 사용할 확률이 높다는 가정하에 dense prefix를 기준으로 compact 영역을 줄인다.
3. compact 단계에서는 compact 영역을 destination과 source로 나누며 살아있는 개체는 destination으로 이동시키고 참조되지 않는 객체는 제거한다.

