---
layout: post
title: 당근페이 면접 후기 및 질문과 답-1
date: 2021-12-21 13:00:00 0000
tags: [Https]
categories: [Interview]
description: 당근페이 면접 질문에 대한 답
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

# <center>당근페이 면접 후기</center>

<br>

사실 당근페이에 서류를 합격했을 때 조금 놀랐다. 왜냐면 기대를 애초에 안했다. 그냥 자기소개서와 코딩테스트 없이 서류만 내면 되서 매우 간단했고 이렇게 생각한 사람이 매우 많아서 지원자가 많을 거라고 생각했다. 그리고 그 수많은 지원자 중에 내가 붙을까라는 의문이 있었기 때문이다. 그래도 어떻게 서류 합격이 되었고 면접 시간을 약속 잡았다.

<br>

![](/images/Interview/post7/2021-12-21-15-31-24.png?style=centerme)

<br>

면접을 진행한 결과 **불합격**을 했다. 물론 내가 CS 지식이 부족한 탓이다. 나름 짧은 기간에 여러 당근마켓 면접 후기들을 보며 준비를 했지만 어려웠다. 그래도 당근페이 면접에서 물어봤던 질문들은 다른 회사 면접에서 충분히 물어볼만한 주제이기 때문에 여기에 정리를 하려고 한다. 다 기억이 나진 않지만 기억나는 것만 적어보도록 하자.

<br>

그전에 HTTP의 정의를 먼저 알고 가자.

**인터넷에서 데이터를 주고 받을 수 있는 프로토콜**

<br>

### **Q: HTTPS의 작동 방식에 대해 설명해주세요**

<br>

![](/images/Interview/post7/2021-12-21-15-43-33.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">HTTP의 보안처리가 된 버전이 HTTPS</span>이다. 요즘은 HTTPS는 웹의 기본 스펙이다라고 봐도 문제가 없다. <span style="background: rgb(251,243,219)">API를 사용</span>하려고 하여도 HTTPS가 안되어 있으면 API를 신청, 사용할 수 없다.

<br>

![](/images/Interview/post7/2021-12-21-15-46-43.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">HTTPS</span>는 <span style="background: rgb(251,243,219)">TCP 위에 SSL/TLS 층을 추가</span>하여 암호화, 인증 그리고 무결성 보장을 통해 더 안전하게 만들어주는 프로토콜이다. 이제 HTTPS의 동작 방식을 알아보기 전에 3가지 개념을 집고 넘어가자.

<br>

- **대칭키**: 암호화에 쓰이는 키와 복호화에 쓰이는 키가 동일한 기법
  <br>

![](/images/Interview/post7/2021-12-21-15-48-44.png?style=centerme)

<br>

만약 클라이언트와 서버가 <span style="background: rgb(251,243,219)">대칭키 방식</span>으로 통신을 한다면 클라이언트도 키를 가지고 있어야 한다. 클라이언트에게 키를 전달하기도 위함하며 소스코드는 누구든지 열어볼 수 있으므로 가지고 있기도 <span style="background: rgb(251,243,219)">굉장히 위험</span>하다.

<br>

**_즉, 원거리에서 대칭키를 안전하게 전달하는 것이 매우 어렵다_**

<br>

- **공개키**: 공개키와 개인키(비밀키)라는 2가지 키를 사용하는 기법이다.

<br>

<span style="background: rgb(251,243,219)">공개키</span>는 말 그대로 누구나 획득할 수 있는 공개된 키를 뜻한다. <span style="background: rgb(251,243,219)">정보를 보내는 쪽(클라이언트)</span>은 이 키를 가지고 <span style="background: rgb(251,243,219)">데이터를 암호화</span>해서 전송한다. <span style="background: rgb(251,243,219)">개인키(비밀키)</span>는 <span style="background: rgb(251,243,219)">공개키</span>로 암호화된 데이터를 <span style="background: rgb(251,243,219)">복호화</span>할 수 있는 키로써 자신(서버)만이 가지고 있는 키이다.

<br>

![](/images/Interview/post7/2021-12-21-15-53-42.png?style=centerme)

<br>

**_이 방법은 안전하게 데이터를 주고 받을 수 있게 만들어주지만 속도가 느리다_**

<br>

- **인증서와 CA(Certificate authority)**: SSL을 적용하기 위해서는 인증서라는 것이 필요하다.

<br>

### HTTPS의 동작 원리

<br>

![](/images/Interview/post7/2021-12-21-16-56-47.png?style=centerme)

<br>

**1)** 네이버의 로그인 창에서 아이디와 비밀번호를 입력하고 <span style="background: rgb(251,243,219)">로그인</span>을 한다.

<br>

**2)** 로그인 버튼을 누르면 이 두 정보(아이디와 비밀번호)는 인터넷을 타고 네이버의 <span style="background: rgb(251,243,219)">서버로 전송</span>이된다

<br>

만약 그냥 HTTP로 보내면 이 암호가 입력한 텍스트 그대로, 누구든 알아볼 수 있는 형식으로 보내진다. **만약 누군가가 이 정보를 중간에 들여다본다면** 그 누군가는 우리의 **네이버 아이디와 비밀번호**를 알게될 것이다.

<br>

HTTPS는 이 정보를 네이버만 알아볼 수 있는 뒤죽박죽(Random Data)된 데이터를 싣어서 보내게 된다 (즉 아래 사진에서 **xyaerXzabc**에 해당)

<br>

![](/images/Interview/post7/2021-12-21-17-01-20.png?style=centerme)

<br>

나쁜 사람이 들여다봐도 뭐라고 쓴 건지 알아볼 수 없도록 말이다.

<br>

네이버에 들어가려고 링크를 클릭했는데 알고보니 **'네이놈'**이라는 피싱 사이트인 경우가 있다고 해보자. 거기에 **네이버 아이디랑 비밀번호를** 입력해버리면 이 피싱 사이트가 우리의 네이버 계정을 알게 된다.

<br>

_**HTTPS는 이런 수상한 사이트를 걸러낼 수 있도록 도와준다**_

<br>

<span style="background: rgb(251,243,219)">기관으로부터 검증된 사이트</span>만 주소에 HTTPS 사용이 허가되고 이제 그냥 HTTP를 사용하는 사이트들은 주소창에 아래와 같은 **'안전하지 않다'**는 표시가 뜨게 된다.

<br>

![](/images/Interview/post7/2021-12-21-17-05-23.png?style=centerme)

<br>

#### HTTPS 요약

- **내가 사이트에 보내는 정보들을 제 3자가 못 보게 한다.**
- **접속한 사이트가 믿을 만한 곳인지를 알려준다**

<br>

이제 좀더 들어가보자. 위의 요약이 어떤 원리로 이루어지는 지 알아보자.

<br>

그러기 위해서는 앞서 배웠던 <span style="background: rgb(251,243,219)">대칭키와 비대칭키</span>를 알아야된다. 다시 한번 상기시켜보자.

예를 들어 전쟁에서 아군에게 편지로 메시지를 보낼 때 중간에 적이 편지를 탈취해도 이를 알아볼 수 없도록 하려면 <span style="background: rgb(251,243,219)">메시지를 암호화</span> 해야 한다. 그 암호화된 메시지를 아군만 읽을 수 있어야 된다. 그래서 이런 방식들이 고민되어 왔다. 그동안 널리 사용되어 온 건 <span style="background: rgb(251,243,219)">대칭키 방식</span>이다.

<br>

메시지를 보내는 쪽과 메시지를 받는 쪽이 메시지를 암호화하고 이를 다시 메시지로 바꾸는 즉, 복호화하는 같은 방식을 공유하는 것이다.

<br>

아래 사진과 같이 A는 27에 대응되고 B는 9에 대응되고 C는 51에 대응되는 이런 표를 양측이 똑같이 가지고 있다면 중간에 편지가 가로채여도 본문이 노출될 걱정 없이 얼마든 메시지를 주고받을 수 있을 것이다. (이 표만 노출되지 않는다면)

![](/images/Interview/post7/2021-12-21-17-13-03.png?style=centerme)

<br>

컴퓨터에서 사용하는 **'대칭키'**란 건 이 표와도 같다.

<span style="color:orange; font-weight:bold">문제는 어떻게 이 동일한 키를 양측이 공유하냐 이다! </span>

<br>

결국 한 번은 한쪽에서 다른 한 쪽으로 이 키를 전송해야 하는데 중간에 이걸 누군가 훔쳐보다면 말짱 꽝이 되는 것이다.

<br>

**문제가 원점으로 돌아와버렸다. 이게 대칭키의 한계다**

<br>

이를 보완한 방식이 1970년대에 수학자들에 의해 개발된다.

<br>

즉 그게 **비대칭키 또는 공개키**라고 불리는 시스템이다. 여기에는 두 개의 키가 사용된다.

<br>

![](/images/Interview/post7/2021-12-21-17-18-08.png?style=centerme)

<br>

각각 A키와 B키라고 부른다. 이 둘은 한쌍이다. 서로 다르기 때문에 **'비대칭키'**라고 불린다. 이 암호화 방식을 개발자들은 보통 **'공개키'**라고 많이 부르는데 여기서는 헷갈리지 않도록 **대칭키**와 상반되는 개념으로 **비대칭키** 방식이라고 부를 것이다.

<br>

<span style="background: rgb(251,243,219)">대칭키 시스템</span>에서는 어떤 키로 암호화를 하면 같은 키로 복호화를 할 수 있었지만 여기서는 <span style="background: rgb(251,243,219)">A키로 암호화를 하면 B키로만 복호화</span>할 수 있다. 반대로 <span style="background: rgb(251,243,219)">B키로 암호화를 하면 A키</span>로만 풀 수가 있다.

<br>

네이버 서버는 이 두 키들 중 하나는 비밀로 보관한다.(**이걸 개인키**라고 한다) 다른 하나를 그냥 대중에게 공개한다. 누구나 볼 수 있도록 말이다.(**이게 공개키**이다)

<br>

이제 사용자는 이 **공개키**로 비밀번호를 암호화해서 네이버에 보낸다. 누가 가로채도 같은 공개키로는 이 암호문을 풀어낼 수가 없다.

**이걸 볼 수 있는 건 이 개인키를 가진 네이버 뿐인 것이다!**

<br>

이 원리로 우리는 개인 정보들을 안심하고 네이버에 보낼 수 있는 것이다.

그럼 여기서 문제가 발생한다.

**_이 사이트가 네이버인 걸 어떻게 증명하는가?_**

<br>

네이버에서 우리에게 보내는 정보들은 그 일부가 이 <span style="background: rgb(251,243,219)">네이버의 개인키로 암호화</span>가 돼있다. 우리가 네이버의 공개키로 풀어서 알아볼 수 있는 건 <span style="background: rgb(251,243,219)">네이버의 개인키로 암호화된 정보</span>들 뿐이다.

<br>

만약 **'네이놈'**에서 온 정보들은 네이버의 공개키로 풀리지 않기 때문에 <span style="background: rgb(251,243,219)"> 네이버의 공개키</span>로 열어보려 하면 오류가 난다. 신뢰할 수 있는 기관에서 우리에게 네이버의 공개키만 검증해준다면 우린 이걸 기준으로 안전하게 네이버를 이용할 수 있을 것이다.

<br>

더 디테일하게 알아보자

<br>

일단 네이버가 우리에게 뿌린 공개키가 <span style="background: rgb(251,243,219)">정품</span>인지를 확인할 수 있어야 한다.

_**네이버가 아니라 네이놈의 공개키일수도 있으니까 말이다**_

<br>

이걸 인증해주는 공인된 민간기업들이 있다. 그것이 바로 **Certificate Authority** 줄여서 **CA**라고 불린다.

<br>

아무나 차려서 될 수 있는 게 아니라 엄격한 인증과정을 거쳐야 CA를 할 수 있다.

우리들의 브라우저, 즉 크롬이나 사파리, 파이어폭스, 엣지, 익스플로러 등에 프로그램에는 이 <span style="background: rgb(251,243,219)">CA들의 목록이 내장</span>돼 있다. 이 브라우저에서 네이버에 접속할 때 어떤 과정들을 거치게 되는지 살펴보자.

![](/images/Interview/post7/2021-12-21-17-28-24.png?style=centerme)

<br>

우리들의 컴퓨터, 정확히는 이 브라우저 측을 이 서버와 상대되는 개념, 즉 **클라이언트**라고 부른다. **사용자**라고 이해하면 된다. **클라이언트**는 아직 이 **서버**를 신뢰하지 못한다. 그래서 이 둘은 먼저 일종의 탐색과정을 거치게 된다. 이것을 **handshake**라고 한다.

<br>

먼저 클라이언트는 어떤 랜덤 데이터를 생성하고 그 랜덤 데이터와 브라우저에서 제공하는 암호화 기법을 서버에 보낸다.

![](/images/Interview/post7/2021-12-21-17-32-08.png?style=centerme)

<br>

이것을 받은 서버는 답변으로 역시 서버측에서 생성한 무작위의 데이터, Server가 결정한 암호화 기법 그리고 해당 서버의 인증서를 실어 보낸다.

![](/images/Interview/post7/2021-12-21-17-33-02.png?style=centerme)

<br>

이것으로 둘은 악수(handshake)를 한 것이다.

<br>

자 그럼 이제 이 클라이언트는 이 인증서가 진짜인지 브라우저에 내장된 CA들의 정보를 통해 확인하게 된다. **(비대칭키 시스템을 사용해서)**

![](/images/Interview/post7/2021-12-21-17-35-28.png?style=centerme)

<br>

CA의 인증을 받은 인증서들은 해당 CA의 개인키로 암호화가 돼있다. 이게 진짜라면 브라우저에 저장된 그 CA의 공개키로 복화할 수 있는 것이다.

![](/images/Interview/post7/2021-12-21-17-36-43.png?style=centerme)

<br>

이 공개키로 복호화될 수 있는 인증서를 발급할 수 있는건 <span style="background: rgb(251,243,219)">그에 대응하는 개인키</span>를 가진 이 <span style="background: rgb(251,243,219)">CA</span> 뿐이다.

<span style="background: rgb(251,243,219)">만약 이 CA 리스트 중에 이 인증서가 해당하는 것이 없다면</span> 브라우저 주소창에 아래와 같은 사진이 뜨게 되는 것이다.

![](/images/Interview/post7/2021-12-21-17-37-46.png?style=centerme)

<br>

**그렇게 성공적으로 복호화된 인증서에는 이 서버의 공개키가 포함돼있다.**

<br>

**_자 이제 이 공개키로 메시지들을 암호화해서 비대칭키 방식으로 주고받으면 되는 것이다!!!_**

## 아니다!!

<br>

지금부터 주고받아지는 데이터들은 대칭키 방식과 비대칭키 방식이 함께 <span style="background: rgb(251,243,219)">혼합</span>되어서 사용된다. 그 좋은 비대칭키 방식이 있는데 왜 대칭키를 쓰는지 의문이 들 것이다.

<br>

**비대칭키 방식으로 메시지를 암호화 및 복호화하는 건 대칭키로 할 때보다 컴퓨터에 훨씬 큰 부담을 주기 때문이다!**

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

기본적으로 비대칭키는 대칭키보다 느리다<br>
그 이유는 대칭키는 비대칭키에 비해 키 길이가 짧고 알고리즘이 비교적 단순하기 때문에 암호화 및 복호화가 빠르다. 그리고 대칭키는 128~256 bit의 길이인 반면 비대칭키는 1024~2048 bit로 키 길이가 짧다.</div>

<br>

사이트를 이용할 때 주고받을 그 <span style="background: rgb(251,243,219)">다량의 데이터</span>를 비대칭키로 일일이 <span style="background: rgb(251,243,219)">암호화, 복호화</span>하는 것은 무리다. 그래서 이 데이터는 <span style="background: rgb(251,243,219)">대칭키로 암호화</span>를 한다.

<br>

**_대칭키는 탈취당할 수 있어서 위험한거 아닌가?_**

<br>

**그 대칭키를 공유할 때 비대칭키를 사용하는 것이다.**

<br>

아까 악수할 때 생성된 <span style="background: rgb(251,243,219)">두 무작위 데이터</span>를 기억하는가?(클라이언트에서 서버로 무작위 데이터 보냄, 서버에서 무작위 데이터를 클라이언트로 보냄) 클라이언트는 <span style="background: rgb(251,243,219)">이 둘을 혼합해서 어떤 임시 키</span>를 만든다. 이 임시 키는 <span style="background: rgb(251,243,219)">서버의 공개키로 암호화</span>돼서 서버로 보내진 다음 양쪽에서 <span style="background: rgb(251,243,219)">일련의 과정을 거쳐서 동일한 대칭키</span>가 만들어지는 것이다.

<br>

이제 이 대칭키는 서버와 이 클라이언트 둘만 갖고 있으니까 이후 서로 주고받아지는 메시지들을 제3자가 알아볼 걱정은 없는 것이다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> SSL HandShaking
</h3>

<br>

![](/images/Interview/post16/2021-12-31-19-38-10.png?style=centerme)

<br>

**(1)** **클라이언트가 먼저 서버에 접속해서 말을 건넨다.** <span style="color:#107896; font-weight:bold">Client Hello</span>

- 내가 브라우처 주소창에서 **blog.naver.com**를 치면 내 브라우저는 네이버 블로그 웹 서버에 접속 시도를 한다.
- HTTPS는 TCP의 일종이니, TCP 연결을 위한 3-Way Handshake를 수행한 브라우저는 네이버 블로그가 HTTPS를 사용하는 것을 알게 되자 <span style="background: rgb(251,243,219)">다음 정보를</span> <span style="color:#107896; font-weight:bold">Client Hello</span>단계에서 보낸다.
  - 브라우저가 사용하는 **SSL 혹은 TLS 버전 정보**
  - 브라우저가 지원하는 **암호화 방식 모음(cipher suite)**
  - 브라우저가 순간적으로 생성한 **임의의 난수(숫자)**
  - 만약 이전에 SSL 핸드 쉐이크가 완료된 상태라면, 그때 생성된 **세션 아이디(Session ID)**
  - 기타 확장 정보(extension)

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

cipher suite: 보안의 궁극적 목표를 달성하기 위해 사용하는 방식을 패키지의 형태로 묶어놓은 것을 의미한다. 여기서 보안의 목표란 다음과 같다.
<br><br>

- 안전한 키 교환<br>
- 전달 대상 인증<br>
- 암호화 알고리즘<br>
- 메시지 무결성 확인 알고리즘<br>
</div>

<br>

**(2)** **서버 또한 위의 인사에 응답하면서,** <span style="background: rgb(251,243,219)">다음 정보</span>**를 클라이언트에 제공한다.** <span style="color:#107896; font-weight:bold">Sever Hello</span>

- 브라우저의 암호화 방식 정보 중에서, 서버가 지원하고 **선택한 암호화 방식(cipher suite)**
- 서버의 **공개키가 담긴 SSL 인증서**. 인증서는 CA의 비밀키로 암호화되어 발급된 상태이다.
- 서버가 순간적으로 생성한 **임의의 난수(숫자)**
- 클라이언트 인증서 요청(선택 사항)

<br>

**(3)** **브라우저는 서버의 SSL 인증서가 믿을만한지 확인한다.**

<span style="background: rgb(251,243,219)">클라이언트</span>는 서버의 인증서가 <span style="background: rgb(251,243,219)">CA에 의해서 발급된 것인지를 확인</span>하기 위해서 클라이언트에 내장된 <span style="background: rgb(251,243,219)">CA 리스트를 확인</span>한다. CA 리스트에 인증서가 없다면 사용자에게 <span style="background: rgb(251,243,219)">경고 메시지</span>를 출력한다. <span style="background: rgb(251,243,219)">인증서가 CA에 의해서 발급된 것인지를 확인</span>하기 위해서 <span style="background: rgb(251,243,219)">클라이언트에 내장된 CA의 공개키를 이용해서 인증서를 복호화</span>한다. 복호화에 성공했다면 인증서는 CA의 개인키로 암호화된 문서임이 <span style="background: rgb(251,243,219)">암시적으로 보증</span>된 것이다. 인증서를 전송한 서버를 믿을 수 있게 된 것이다. (이때 믿을 수 없는 인증서일 경우 브라우저 경고를 보냄)

<br>

**(4)** **브라우저는 자신이 생성한 난수와 서버에서 보내준 난수를 사용하여** <span style="background: rgb(251,243,219)">premaster secret</span>**을 만든다.**

클라이언트는 <span style="background: rgb(251,243,219)">자신이 만든 무작위 데이터(random data)</span>와 <span style="background: rgb(251,243,219)">서버쪽에서 전송된 무작위 데이터(random data)를 조합</span>하여 <span style="background: rgb(251,243,219)">premaster secret 키</span>를 생성한다. 이 키를 서버로 전송할 때 인증서에서 받았던 키를 이용하여 <span style="background: rgb(251,243,219)">공개키 방식 암호화</span>를 하게 된다. 그리고 서버로 전송한다. (서버 인증서에 공개키가 같이 딸려옴)

<br>

**(5)** **서버는 사이트의 개인키로, 브라우저가 보낸** <span style="background: rgb(251,243,219)">premaster secret</span> **값을 복호화 한다.**

<br>

서버에서는 수신한 <span style="background: rgb(251,243,219)">premaster secret 키를 개인키를 이용하여 복호화</span>하여 얻게된다.

이제 서버와 클라이언트 모두 일련의 과정을 거쳐서 <span style="background: rgb(251,243,219)">premaster secret 값</span>을 <span style="background: rgb(251,243,219)">master secret 값</span>으로 만든다.

<span style="background: rgb(251,243,219)">master secret는 session key를 생성</span>하는데 이 <span style="background: rgb(251,243,219)">session key가 대칭키 암호화에 사용할 키</span>가 된다. 이것으로 브라우저와 서버 사이에 주고받는 데이터를 <span style="background: rgb(251,243,219)">암호화하고 복호화</span>한다.

<br>

**(6)** **서버/클라이언트는 SSL handshake를 종료하고 HTTPS 통신을 시작한다.**

브라우저와 서버는 <span style="background: rgb(251,243,219)">SSL handshake가 정상적으로 완료</span>되었고 이제는 웹상에서 데이터를 세션 키를 사용하여 암호화/복호화하며 HTTPS 프로토콜을 통해 주고받을 수 있다. <span style="background: rgb(251,243,219)">HTTPS 통신이 완료되는 시점에서 서로에게 공유된 세션 키를 폐기</span>한다. 만약 세션이 여전히 유지되고 있다면 브라우저는 SSL handshake 요청이 아닌 세션 ID만 서버에게 알려주면 된다.

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 비대칭키를 활용한 통신이 대칭키 활용 통신보다 느린 이유
</h3>

<br>

비대칭키의 대표적인 알고리즘으로는 RSA, 디피-헬만, 타원곡선암호 등이 있다. 가장 대표적인 RSA는 기본적인 정수론, 소수를 이용하는데 정보를 두 개의 소수로 표현한 후, 두 소수의 곱을 힌트와 함께 암호로 사용한다. c=a*b(a,b는 소수)라 할 때, a,b를 가지고 c를 구하는 것은 비교적 쉽게 구할 수 있지만 c를 먼저 제시하고 곱해진 두 소수 a,b를 구하는 문제는 풀기가 쉽지 않다. c를 공개해도 a 또는 b를 구하는 것이 대단히 어려우므로 c는 공개키로, a는 개인키로 사용한다.

그러나 수학적인 난제를 기반으로 설계된 비대칭키는 암호화나 복호화를 수행하기 위한 연산이 복잡한 수학 연산을 기반으로 구성되어 있기 때문에 효율성이 대칭키 암호(AES, SEED)에 비해 약 1000배에 달한다. 비대칭키는 길이가 긴 키의 소인수 분해가 어렵다는 특성을 활용한 알고리즘인 만큼 대칭키에 비해 키 사이즈가 상대적으로 크고 연산이 복잡하다. 대칭키의 대표적인 알고리즘인 AES는 128, 192, 256 비트 크기의 키를 사용한다. 반면 비대칭키의 공개키의 경우 512, 1024, 2048 비트의 키를 사용한다. 따라서 비대칭키를 사용한 암호화, 복호화는 대칭키의 사용보다 부하가 크고, 사용에 제약이 따를 수밖에 없다.

<br>

**[소인수분해](https://mathbang.net/200)**