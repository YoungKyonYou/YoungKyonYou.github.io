---
layout: post
title: 동기 vs 비동기 Blocking vs Non-Blocking
date: 2021-12-23 15:00:00 0000
tags: [Blocking, Non-Blocking, Synchronous, Asynchronous]
categories: [Interview]
description: 동기와 비동기 그리고 블로킹과 논 블로킹의 차이
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

면접 질문으로 단골로 나오는 것들이 몇가지 있다. 지금까지 면접을 보면서 계속 나왔던 질문이나 제대로 답해본 적이 없다. 꼭 관련되서 게시글을 써야겠다는 마음이 있었는데 앞에 질문들에 대해 포스팅하느라 이제야 글을 써본다.

<br>

처음 동기, 비동기, 블로킹, 논블로킹을 듣게되면 헷갈린다.

<br>

마치 동기와 블로킹이 같은 말 같고 비동기와 논블로킹이 같은 말 같아 보이기 때문이다. 하지만 둘은 <span style="color: rgba(131, 24, 67); font-weight:bold">다르다!</span>

<br>

먼저 **Blocking과 Non-Blocking**의 차이를 살펴보자.

<br>

그러기 앞서 여기서 기준점이 있어야 된다. Blocking과 Non-Blocking를 구별해주는 기준점을 여기서는 **제어권**이라고 하겠다. 제어권이란 함수를 실행할 권리라고 생각을 하자. **블로킹**에 대해서 먼저 살펴보자.

<br>

#### 블로킹

<br>
- 호출된 함수가 제어권을 넘겨주지 않아 호출한 함수측에서는 다른 작업을 수행할 수 없고 제어권이 돌아오기만을 기다리는 것을 말한다.

<br>

> 상황으로 이해하자. [신발가게 안에서]

![](/images/Interview/post11/2021-12-23-16-15-13.png?style=centerme)

<br>

![](/images/Interview/post11/2021-12-23-15-30-50.png?style=centerme)

<br>

위 그림을 보면 **제어권**을 가지고 있는 A함수가 진행하다가 B함수를 호출하게 된다. 그리고 **제어권**을 B 함수에 넘긴다. 이때 A 함수는 **제어권**이 없기 때문에 함수 실행이 멈추게 된다. 그리고 **제어권**을 넘겨받은 B 함수는 함수를 완료시키고 나서 **제어권**을 다시 자신을 호출한 함수 A에게 **제어권**을 넘겨준다.

<br>

<br>

이제 **Non-Blocking**에 대해 살펴보자.

<br>

#### 논블로킹

<br>

- 어떤 함수를 호출한 함수가 제어권을 넘겨주지 않고 그대로 자신이 가지고 있는 것을 말한다.

<br>

> 상황으로 이해하자. [신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-14-40.png?style=centerme)

<br>

![](/images/Interview/post11/2021-12-23-15-35-22.png?style=centerme)

<br>

A 함수가 B함수를 호출하면 B 함수는 실행되지만 제어권은 A 함수가 그대로 가지고 있는다. A 함수는 계속 제어권을 가지고 있기 때문에 B 함수를 호출한 이후에도 자신의 코드를 계속 실행한다.

<br>

동기화 비동기를 살펴보자. 살펴보기 전에 여기서도 기준점을 가지고 있어야 한다. 여기서 기준은 **작업 완료**를 **누가 신경** 쓰는가 이다.

<br>

#### 동기

<br>

- **'호출한 함수'**가 스스로 신경을 쓴다. 즉, 호출된 함수의 수행 결과 및 종료를 호출한 함수가 신경 쓰면 동기이다.

<br>

![](/images/Interview/post11/2021-12-23-15-57-41.png?style=centerme)

<br>

Thread1, Thread2가 존재할때 Thread1에서 처리하려고 했던 일을 Thread2에게 보낸 경우, Thread2가 해당 작업을 수행하는 동안 Thread1은 Thread2가 끝날 때까지 대기상태다.

<br>

> 상황으로 이해하자.[신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-01-17.png?style=centerme)

<br>

#### 비동기

<br>

- **호출되는 함수**에게 callback을 전달해서 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 callback을 실행하고 호출하는 함수는 작업 완료 여부를 신경쓰지 않으면 비동기이다.

<br>

![](/images/Interview/post11/2021-12-23-16-11-44.png?style=centerme)

<br>

Thread1, Thread2가 존재할때 Thread1에서 처리하려고 했던 일을 Thread2에게 보낸 경우, Thread2가 해당 작업을 수행하는 동안 Thread1은 대기 없이 나머지 Task2, Task3를 실행한다.

<br>

> 상황으로 이해하자. [시발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-12-45.png?style=centerme)

<br>

---

## 조합

<br>

### 동기 / 블로킹

<br>

- 동기: 호출한 함수가 작업 완료 여부를 확인한다.
- 블로킹: 호출된 함수가 제어권을 가진다.

<br>

![](/images/Interview/post11/2021-12-23-16-17-17.png?style=centerme)

<br>

> 상황으로 이해하자. [신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-17-53.png?style=centerme)

<br>

**Example**

```java
import java.util.Scanner;

/**
 * 동기 + 블로킹
 */
public class BlockingAndSync {
    public static void main(String[] args) {
        System.out.println("메시지를 입력하세요 : ");

        Scanner scanner = new Scanner(System.in);

        /* 제어권이 넘어갔다. 입력이 되기 전까지 그 다음 로직이 실행되지 않는다. */
        String message = scanner.nextLine();

        /* 입력이 된 후, 결과를 받아서 그때 처리된다. */
        System.out.println(message);
    }
}
```

<br>

### 동기 / 논블로킹

<br>

- 동기: 호출한 함수가 작업 완료 여부를 확인한다.
- 논블로킹: 호출한 함수가 제어권을 가진다.

<br>

![](/images/Interview/post11/2021-12-23-16-21-20.png?style=centerme)

<br>

Thread1은 task1의 완료 여부에 상관 없이 다른 작업을 진행할 수 있다. 하지만 task1의 완료 여부를 지속적으로 확인한다.

<br>

> 상황으로 이해하자. [신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-22-20.png?style=centerme)

<br>

**Example**

<br>

![](/images/Interview/post11/2021-12-23-16-22-43.png?style=centerme)

<br>

흔한 게임 업데이트 진행중인 화면이다. 오른쪽 하단에 게임 업데이트가 계속 진행되고 있다. 남은 시간 및 현재까지 업데이트된 정도를 보여주고 있다. 완료여부를 계속해서 확인하고 있는 상태로 보인다.

<br>

### 비동기 / 블로킹

<br>

- 비동기 (Asynchronous) : Callback 함수가 작업 완료 여부를 확인한다.

- 블로킹 (Blocking) : 호출된 함수 (task1)이 제어권을 가진다.

<br>

![](/images/Interview/post11/2021-12-23-16-23-44.png?style=centerme)

<br>

Thread1이 task1의 작업 완료 여부를 신경쓰지 않으나, 작업이 완료될때 까지 아무것도 하지 못하는 대기 상태다. 해당 경우는 비동기인데 굳이 블로킹인 경우인데, 이는 보통 비동기 (Asynchronous) + 논블로킹 (Non-Blocking) 로 작업을 시도했을때 잘못된 경우 발생한다.

<br>

> 상황으로 이해하자. [신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-25-08.png?style=centerme)

<br>

### 비동기 / 논블로킹을

<br>

- 비동기 (Asynchronous) : Callback 함수가 작업 완료 여부를 확인한다.
- 논블로킹 (Non-Blocking) : 호출한 함수가 제어권을 가진다.

<br>

![](/images/Interview/post11/2021-12-23-16-26-14.png?style=centerme)

<br>

Thread1이 task1의 완료 여부를 신경쓰지 않고 다른 자신의 작업을 진행한다. 성능과 자원 효율면에서 가장 우수하다.

<br>

> 상황으로 이해하자. [신발가게 매장 안에서]

![](/images/Interview/post11/2021-12-23-16-27-02.png?style=centerme)

<br>

**Example**

```javascript
function getData() {
  let data;

  $.ajax({
    type: "post",
    url: "https://recordboy.github.io/",
    data: {
      // 전송 데이터
    },
    success: function (result) {
      // 통신 성공시 결과값 할당
      data = result;
    },
  });

  return data;
}

console.log(getData()); // undefined
```

---

### 장단점

<br>

- **블로킹**
  - 장점
    - 작업이 순차적으로 이루어지기에 작업 흐름을 쉽게 이해할 수 있음
  - 단점
    - 블로킹이 이루어지는 동안으 하드웨어 리소스를 효율적으로 이용하지 못함

<br>

- **논 블로킹**
  - 장점
    - 리소스가 낭비되는 시간이 없기에 하드웨어 리소스를 균일하고 효율적으로 이용가능
  - 단점
    - 업무 흐름이 매우 복잡해지는 단점 존재

<br>

- **동기**
  - 장점
    - 요청한 작업의 완료여부와 결과를 바로 알 수 있다는 장점이 있음
  - 단점
    - 요청한 작업의 완료여부와 작업 결과를 반환받는 데 필요한 시간이 긴 경우 문제가 발생

<br>

- **비동기**
  - 장점
    - 이미 요청한 작업의 결과를 기다리고 있을 필요 없이 바로 다음 작업을 요청할 수 있기에 작업 효율이 높아짐(자원의 효율적 사용)
  - 단점
    - 특정 작업의 경우 선행 작업의 결과값을 이어받아 순차적으로 작업을 진행해야 할 수 있다. 이런 작업을 비동기 작업으로 구현할 경우 프로그램이 복잡해짐

---

## 비동기는 언제 써야 할까?

<br>

웹서버로 예를 들어보겠다.

웹서버에서 받는 요청을 처리해주는 쓰레드가 100개가 있다고 해보자.

<br>

만약 웹서버로 100개의 requests가 들어오는 경우에는 **동기**를 쓰든 **비동기**를 쓰든 속도가 비슷하다.

<br>

request가 100개가 넘어가는 순간 비동기를 쓴다고 해보자. 200개의 requests가 들어오면 그냥 무작정 기다리는 게 아니라 100개를(request 200개 중에 100개) 실행하다가 잠깐 멈추고 나머지 100개(나머지 request 200개 중에 100개)를 실행하고 왔다갔다 한다.

<br>

결과적으로 하나하나의 job은 빨리 안 끝날 수 있지만 모든 사람에게 너무 느리게 끝나지 않게, 그러니까 웹에 접속할 때 이미지를 보여주는 것과 같은 경우 이미지가 쫙 보이기 시작하면 사람들은 로딩되고 있구나 라고 느낄 것이다. 반면에 이미지가 몇 분동안 아예 안 보인다면 짜증이 난다. 그것과 같다.

<br>

이것만이 문제가 아니다 만약 비동기를 안 할 경우 뒤에 있는 task는 앞의 task가 끝날 때까지 기다린다. request의 200개 중 100개가 모두 동일한 시간에 끝난다면 그냥 smooth하게 흘러가면 된다.(기다리는 시간만 길어짐) 그런데 재밌는 건 이렇게 하다가 이 중 하나, 즉, 중간에 있는 게 다른 거에 비해 100배의 시간이 걸린다 하면 이 뒤에 있는 딜레이는 엄청날 것이다.

<br>

그래서 자기가 가지고 있는 쓰레드 풀에 있는 테스크 수보다 request가 많지가 않다면 동기로하나 비동기로하나 성능상에 별 차이가 없다

<br>

이때는 코드 가독성이라던가 오버헤드를 줄이는 측면에서 비동기를 안 쓰는 게 낫다.

<br>

나중에 스케일이 커져서 로드가 몰리게 되면 갑자기 평탄하던 그래프가 치솟는다. 이때 비동기를 쓰면 완만하게 그래프가 올라간다. 즉 어느 정도 유지가 된다.

<br>

**_로드가 몰리면 모든 사람이 어느 정도는 느려질 수 있어도 한명이 엄청나게 오래 기다리다가 타임아웃되는 것을 방지하기 위해서는 비동기가 낫다._**
