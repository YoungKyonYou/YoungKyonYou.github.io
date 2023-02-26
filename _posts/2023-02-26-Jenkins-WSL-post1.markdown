---
layout: post
title: WSL Ubuntu 22.04.2LTS 에서 Jenkins 실행하는 방법
date: 2023-02-26 10:00:00 0000
tags: [반성]
categories: [jenkins-wsl]
description: 다시 돌아보는 내 자신
---

<br><br>

_**오늘의 나보다 성장한 내일의 나를 위해....**_

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

<br><br><br><br>

<h2 style="color:#107896;  font-weight:bold">

<br>

<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> WSL Ubuntu 22.04.2LTS 에서 Jenkins 실행하는 방법
</h2>

<br>

인프런에서 **Jenkin를 이용한 CI/CD Pipeline 구축** 강의를 시작했다.

이 강의는 **MAC** 위주로 진행이 됐고 나는 MAC이 없어서 Windows로 따라해보려고 하다가 WSL를 사용해서 강의를 듣는 것으로 결정을 했다. 

해당 강의는 Docker를 사용해 Jenkins 컨테이너를 실행함으로 일단 **Ubuntu**를 사용해서 docker desktop를 사용하는 방법은 아래 링크를 참고한다.

[docker desktop 설치하기(WSL2 Ubuntu 활용)](https://goddaehee.tistory.com/313)

<br>

다 깔고 나서 Ubuntu terminal에서 docker version이 제대로 나오는지 확인하자

```shell
docker --version
```


![](/images/Jenkins/2023-02-26-19-41-38.png?style=centerme)

<br>

Jenkins 도커 이미지를 배포하기 위해서 아래 명령어를 입력한다.

<br>

```shell
docker run -d -p 8088:8080 -p 50000:50000 --name jenkins-server\--restart=on-failure \jenkins/jenkins:lts-jdk11
```

- run : 도커를 실행할 때 사용하는 명령어
- -p : 컨테이너 내부에 있는 포트를 컨테이너 외부에서 어떻게 접속해서 사용할지 설정하는 옵션
  - -p 8080:9090는 컨테이너 바깥 쪽에서 8080 포트를 사용한다면 컨테이너 내부로는 9090 포트로 접속이 된다는 것이다.
- --restart=on-failure : fail이 될 경우 restart 한다
- jenkins/jenkins : 앞 jenkins는 계정 이름 뒤 jenkins는 리포지토리 이름
- : 뒤는 우리가 사용하려고 하는 tag의 이름이다. 
- -d : 데몬으로 실행(백그라운드 실행)

---

컨테이너가 제대로 작동이 되었다면 **docker ps**라는 명령어로 확인이 가능하다.

<br>

![](/images/Jenkins/2023-02-26-19-53-35.png?style=centerme)

<br>

자 이제 실행한 컨테이너에 크롬을 통해 접근해 보자.

우리는 외부에서 8088로 접근한다고 이전에 -p 옵션을 통해 설정했으므로 

**http://localhost:8088/** 로 접근한다
<br>

![](/images/Jenkins/2023-02-26-19-54-37.png?style=centerme)

<br>

사진에서 **Adminstrator Password**를 입력하라고 나오는데 사실 강의에서는 해당 비밀번호가 **콘솔 로그**에 찍힌다고 되어 있지만 WSL Ubuntu를 사용하게 되면 콘솔 로그에 컨테이너를 실행할 때 딱히 찍히는 로그가 없다.

<br>

그리고 해당 사진에서는 **/var/jenkins_home/secrets/initialAdminPassword** 로 접속하면 비밀번호가 나와있다고 되어 있지만 Ubuntu 콘솔에 /var 디렉토리에 가게되면 아래 사진과 같이 jenkins_home 폴더를 찾아볼 수가 없다.

<br>

![](/images/Jenkins/2023-02-26-19-57-45.png?style=centerme)

<br>

강사님은 Mac 환경에서 강의를 진행함으로 이러한 부분을 알려주지 않는다. 그래서 따로 알아본 결과 컨테이너 내부로 진입을 하면 찾을 수 있었다.

<br>

컨테이너 내부로 진입하기 위해서는 컨테이너 ID를 알아야 하는데 이는 **docker ps**로 확인한다.

<br>

![](/images/Jenkins/2023-02-26-20-00-15.png?style=centerme)

<br>

사진에서 보다시피 컨테이너 ID는 e3eeb021b795 이다.

이를 복사하고 아래와 같이 입력한다.

<br>

```shell
docker exec -it e3eeb021b795 bash
```

<br>

![](/images/Jenkins/2023-02-26-20-01-27.png?style=centerme)

<br>

이렇게 하면 컨테이너 안으로 진입할 수 있는데 여기서 우리가 찾고자 하는 것을 찾을 수 있다.

<br>

![](/images/Jenkins/2023-02-26-20-02-45.png?style=centerme)

**/var/jenkins_home/secrets**

<br>

여기서 비밀번호를 확인한다.

<br>

![](/images/Jenkins/2023-02-26-20-03-40.png?style=centerme)

<br>

위 비밀번호를 복사해서 웹에 입력칸에 넣는다

<br>

![](/images/Jenkins/2023-02-26-20-04-12.png?style=centerme)

<br>

넣고 나면 위와 같이 화면이 전환되는데 이는 

모든 플러그인을 설치할 것인지 설치할 플러그인을 고를 것인지 고르는데 여기서는 모든 플러그인을 다 설치하기 위해서 왼쪽을 선택한다.

<br>

![](/images/Jenkins/2023-02-26-20-06-30.png?style=centerme)

<br>

플러그인을 다 다운받고 나면 아래와 같이 계정을 만들 수 있는 화면이 나온다.

<br>

![](/images/Jenkins/2023-02-26-20-12-12.png?style=centerme)

<br>

다 만들고 난 후

![](/images/Jenkins/2023-02-26-20-12-40.png?style=centerme)

<br>

**Save and Finish**.를 누르면 이렇게 완성된다.

<br>

![](/images/Jenkins/2023-02-26-20-13-09.png?style=centerme)

<br>

다시 localhost:8088 로 접속하게 되면 아래와 같이 나온다.

![](/images/Jenkins/2023-02-26-20-13-53.png?style=centerme)