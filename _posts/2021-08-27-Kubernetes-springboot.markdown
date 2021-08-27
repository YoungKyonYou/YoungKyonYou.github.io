---
layout: post
title: SpringBoot 앱을 도커 이미지로 변환 후 Deployment로 배포하고 접근하는 방법
date: 2021-08-27 17:00:00 0000
tags: [Kubernetes, Docker, SpringBoot, Docker Hub]
categories: [Kubernetes]
description: 도커 이미지를 도커 허브에 저장하고 Deployment로 배포하고 접근하기
---

<br><br>
_**믹스 컴피 중독자가 되가는 중..**_
<br>
(Press the Button)

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

# <center>Kubernetes와 Mysql Workbench 연동하기-2(로드 밸런서 사용하기)</center>

<br>

이번 포스팅을 읽기 전에 자신만의 SpringBoot 앱이 있는 것이 좋다. 물론 내가 도커 허브에 저장한 이미지를 써도 무방하다.

<br>

일단 도커 메인 홈페이지에 가입이 되어 있어야 한다. 그리고 repository를 생성한다.

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-17-21-01.png){: p}

<br>

클러스터에 접속하고 target 디렉터리를 만든다음 그 안에 .jar 파일을 넣고 이전 디렉터리로 이동한 다음 <span style="color:orange; font-weight:bold">Dockerfile</span>를 생성하자.

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-08-03.png){: p}

<br>

**Dockerfile**

```Dockerfile
FROM openjdk:11
LABEL description="Echo OP Java Development"
COPY ./target/application.jar /opt/application.jar
WORKDIR /opt
ENTRYPOINT ["java", "-jar", "application.jar"]
```

<br>

하나 하나 살펴보면 아래와 같다.

<br>

**Dockerfile**

```Dockerfile
#import openjdk:8 image
#FROM <이미지 이름>:[태그] 형식으로 이미지를 가져온다.
#가져온 이미지 내부에서 컨테이너 이미지를 빌드한다.
#누군가 만들어 놓은 이미지에 필요한 부분을 추구한다고 보면 된다.
#여기서는 openjdk를 기초 이미지로 사용한다.
FROM openjdk:11

#Label_desc="Echo IP Java Application"
#즉 컨테이너 이미지를 설명한다.
#LABEL <레이블 이름>=<값>의 형식으로 이미지에 부가적인 설명을 위한 레이블을 추가할 때 사용한다.
LABEL description="Echo OP Java Development"

#호스트에서 새로 생성하는 컨테이너 이미지로 필요한 파일을 복사한다.
#COPY <호스트 경로> <컨테이너 경로>의 형식이다.
#application.jar 파일을 이미지의 /opt/application.jar로 복사한다
COPY ./target/application.jar /opt/application.jar

#이미지의 현재 작업 위치를 opt로 변경한다.
WORKDIR /opt

#ENTRYPOINT ["명령어", "옵션",... "옵션"]의 형식이다.
#컨테이너 구동 시 ENTRYPOINT 뒤에 나오는 대활호([]) 안에 든 명령을 실행한다.
#콤마(,)로 구분된 문자열 중 첫 번째 문자열은 실행할 명령어고, 두 번째
#문자열부터 명령어를 실행할 때 추가하는 옵션이다.
#여기서는 컨테이너를 구동할 때 java -jar application.jar이 실행된다는 의미이다.
ENTRYPOINT ["java", "-jar", "application.jar"]
```

<br>

도커 이미지를 빌드하는 명령을 친다.

```bash
docker build --tag youngkyonyou/springboot-project:spring .
```

<br>

빌드가 되었다면 도커 허브에 우리가 만든 리포지토리에 이미지를 저장한다.

<br>

```bash
docker push youngkyonyou/springboot-project:spring
```

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-09-44.png){: p}

<br>

<span style="color:orange; font-weight:bold">spring</span>이라고 저장된 이미지가 존재하는 것을 볼 수 있다.

<br>

다시 클러스터로 돌아와서 yaml 파일을 만든다.

<br>

**deployment-app.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: demo
  name: demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo
  strategy: {}
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
        - image: youngkyonyou/springboot-project:spring
          name: kubernetes-spring
```

<br>

설명은 이전 포스트에서 많이 했고 비슷하므로 생략한다.

<br>

주의해서 볼 것은 우리가 도커 허브 리포지터리에 올린 이미지를 사용하는 부분이다.

<span style="color:orange; font-weight:bold">image: youngkyonyou/springboot-project:spring</span>

<br>

이제 deployment를 배포한다.

<br>

```bash
kubectl apply -f deployment-app.yml
```

<br>

성공적으로 만들어졌는지도 확인한다.

<br>

```bash
kubectl get deployment
```

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-12-42.png){: p}

<br>

이제 expose 명령으로 외부로 노출시켜야 한다.

<br>

```bash
kubectl expose deployment demo --type=LoadBalancer --name=webapp --port=80 --target-port=8080
```

<br>

위는 컨테이너 포트 8080을 포트 80으로 노출하여 위의 서비스를 노출한다는 것이다.

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<br>

<div class="webnots-information webnots-notification-box">여기서 <span style="color:#ff0000; font-weight:bold">http</span>는 <span style="color:#ff0000; font-weight:bold">포트 80</span>를 사용하기 때문에 우리는 단순히 <span style="color:#ff0000; font-weight:bold">External IP</span>로 접근이 가능하다.</div>

<br>

위와 같이 명령을 입력하고 확인해 본다.

```bash
kubectl get service
```

<div class="webnots-information webnots-notification-box">마스터노드의 IP와 포트 번호를 지정해서 접근도 가능하다. 즉 현재 우리 마스터노의 IP는 <span style="color:#ff0000; font-weight:bold">192.168.1.10</span>이다. 여기서 포트 30003을 이용해서 접근 가능하다. <br>
예시:<span style="color:#ff0000; font-weight:bold">192.168.1.10:30003</span></div>

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-13-57.png){: p}

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-21-49.png){: p}

<br>

위 사진은 마스터노드와 포트를 사용해 웹에 접근한다.

<br>

![](/images/Kubernetes/Kubernetes-Springboot2/2021-08-27-18-22-42.png){: p}

<br>

위 사진은 <span style="color:orange; font-weight:bold">External IP</span>만을 사용해서 접근한다. 다시 말하지만 expose할 때 port 옵션에 80를 사용하였기 때문에 가능한 것이다. 즉 <span style="color:orange; font-weight:bold">192.168.1.16:80</span>를 쓴 것과 다름이 없다. 
