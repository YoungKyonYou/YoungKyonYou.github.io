---
layout: post
title: IP 주소 0.0.0.0의 의미
date: 2022-02-05 15:00:00 0000
tags: [Network]
categories: [Network]
description: 0.0.0.0의 의미
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> 0.0.0.0의 의미
</h2>

<br>

책으로 웹 개발을 하다보면 아주 가끔 <span style="background: rgb(251,243,219)">0.0.0.0</span>이라는 IP를 사용할 때가 있다.

해당 IP를 그저 <span style="background: rgb(251,243,219)">모든 IP에 접근하기 위해 사용</span>한다 정도로만 알고 있었다. 하지만 왜 서버 측에서 <span style="background: rgb(251,243,219)">0.0.0.0</span>으로 접근하는데 <span style="background: rgb(251,243,219)">local</span>의 웹 서버로 접근이 되는지 이해가 되지 않았다.

이에 대한 좋은 영문 글이 있다 **[What is the Difference Between 127.0.0.1 and 0.0.0.0?](https://www.howtogeek.com/225487/what-is-the-difference-between-127.0.0.1-and-0.0.0.0/)**

<br>

해당 글을 보면 다음과 같은 문구가 나온다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

In the context of servers, 0.0.0.0 means all IPv4 addresses on the local machine. If a host has two IP addresses, 192.168.1.1 and 10.1.2.1, and a server running on the host listens on 0.0.0.0, it will be reachable at both of those IPs</div>

<br>

이 문구를 보면, <span style="background: rgb(251,243,219)">0.0.0.0</span>은 <span style="background: rgb(251,243,219)">local machine</span>의 모든 <span style="background: rgb(251,243,219)">IPv4 address</span>를 의미하기 때문에 0.0.0.0로 접근하면 로컬 호스트의 모든 <span style="background: rgb(251,243,219)">IPv4</span>로 되어있는 호스트에 접근이 가능하다는 의미이다.

조금 더 설명을 붙이자면, 정확한 address가 할당되어 있지 않다면, 각각의 host는 그 address를 자신이라고 주장하게 되고 이에 따라 웹 서비스에서 0.0.0.0을 지정하면 자신의 IP를 그 address로 지정하게 되어 local로 접근이 되는 것이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 간단한 예시
</h3>

<br>

간단한 flask 서버로 예시를 들어보자.

<br>

```python
from flask import Flask

app=Flask(__name__)

@app.rout("/")
def index():
  return "Hello, world!"

if __name__ == "__main__":
  app.run(host="127.0.0.1")
```

<br>

![](/images/Network/2022-02-06-17-52-30.png?style=centerme)

<br>

위는 127.0.0.1:5000 으로 접근하게 되면 단순하게 Hello, world! 문구를 웹으로 띄워준다.

<br>

![](/images/Network/2022-02-06-17-53-17.png?style=centerme)

<br>

이제 cmd에 들어가 ipconfig를 통해 자신의 IP 주소를 확인해 보자.

<br>

![](/images/Network/2022-02-06-17-54-13.png?style=centerme)

<br>

위 사진을 통해 현재 내 IP가 <span style="background: rgb(251,243,219)">192.168.1.16</span>인 것을 확인할 수 있다. 그렇다면 아까 서버를 킨 채로 다시 이 IP와 5000번 포트로 접근해보자.

<br>

![](/images/Network/2022-02-06-17-55-34.png?style=centerme)

<br>

보시다시피 접근이 안된다. 코드를 조금 수정해 보자.

<br>

```python
from flask import Flask

app=Flask(__name__)

@app.rout("/")
def index():
  return "Hello, world!"

if __name__ == "__main__":
  app.run(host="192.168.1.16")
```

<br>

![](/images/Network/2022-02-06-17-56-30.png?style=centerme)

<br>

서버를 재가동하게 되면 위의 사진처럼 192.168.1.16:5000으로 <span style="background: rgb(251,243,219)">Running</span>되고 있다는 표시가 뜰 것이다.

<br>

![](/images/Network/2022-02-06-17-57-05.png?style=centerme)

<br>

기대했던 되로 제대로 접근이 된다. 하지만 <span style="background: rgb(251,243,219)">127.0.0.1:5000</span>으로 접근하게 되면 또 다시 찾을 수 없다는 표시가 뜰 것이다.

<br>

![](/images/Network/2022-02-06-17-57-36.png?style=centerme)

<br>

코드를 다시 수정해보자.

<br>

```python
from flask import Flask

app=Flask(__name__)

@app.rout("/")
def index():
  return "Hello, world!"

if __name__ == "__main__":
  app.run(host="0.0.0.0")
```

<br>

![](/images/Network/2022-02-06-17-58-27.png?style=centerme)

<br>

위와 같이 수정하고 서버를 재가동한다.

<br>

이제는 <span style="background: rgb(251,243,219)">192.168.1.16:5000, 127.0.0.1:5000, 0.0.0.0:5000</span> 세개 다 접근이 가능한 것을 볼 수 있다.

<br>

![](/images/Network/2022-02-06-17-59-14.png?style=centerme)

![](/images/Network/2022-02-06-17-59-37.png?style=centerme)

![](/images/Network/2022-02-06-17-59-23.png?style=centerme)

<br>
