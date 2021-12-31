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

- **로딩:** .class 파일을 익어온다.
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

그렇다면 JVM의 Root Space는 어디일까?

<br>

Heap 영역 메모리에 대한 참조를 들고 있을 수 있는 영역일 것이다.

JBM Memory 영역 중에서는 다음과 같다.

<br>

1. _Stack의 로컬 변수_
2. _Method Area의 Static 변수_
3. _Native Method Stack의 JNI 참조_

<br>

아래 그림을 참고하자.

<br>

![](/images/Interview/post16/2021-12-30-16-04-49.png?style=centerme)

<br>
