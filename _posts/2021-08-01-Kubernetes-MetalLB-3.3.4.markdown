---
layout: post
title: 온프레미스에서 로드밸런서를 제공하는 MetalLB
date: 2021-08-01 11:00:00 0000
tags: [Kubernetes, MetalLB, ARP, BGP, NDP, MAC Address]
categories: [Kubernetes]
description: MetalLB 실습
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

<br><br>
_**커피 중독자되는 중...**_
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

# <center>온프레미스에서 로드밸런서를 제공하는 MetalLB</center>

<br>

노드포트는 굉장히 심플하다. 현실적으로 노드포트가 서비스하는 방식은 굉장히 효율이 떨어진다. 아래 사진을 참고해보자.

1. 사용자가 워크 노드에 있는 포트에 먼저 접속을 한다. (순서도 1번 참고)

2. 접속을 한 이후에 해당 워크 노드가 서비스로 이를 바인딩 해준다 (순서도 2번 참고)

3. 서비스가 현재 있는 상태를 봐 가면서 노드에 연결을 해주게 된다.(순서도 3번 참고)

<br>

즉 비효율적으로 사용자가 <span style="color:orange; font-weight:bold">서비스</span>에 접근해서 <span style="color:orange; font-weight:bold">서비스</span>가 바로 <span style="color:orange; font-weight:bold">파드</span>에 접근하는 게 아니라 사용자가 워크 노드 포트에 꼭 접속을 해서 이를 <span style="color:orange;font-weight:bold">서비스</span>로 보내준 다음에 <span style="color:orange; font-weight:bold">서비스</span>가 파드에 보내주는 구조이기 때문에 효율성이 떨어진다. 그리고 다른 문제는 워크 노드가 죽었다면 접속해야 되는 사용자에 있는 IP가 변경이 된다 그렇다면 이것은 대표 IP라는 컨셉이 떨어지기 때문에 사용자가 IP를 알아야된다. 이부분은 사실 제대로 서비스를 하기에는 부족한 부분이 있다. 그래서 프로덕션에서는 노드포트를 이용해서 서비스를 하진 않고 테스트용으로 노드포트를 사용한다.

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-14-45-41.png){: p}

<br>

그래서 쿠버네티스에서는 **로드 밸런서(LoadBalancer)**라는 서비스 타입을 제공해 간단한 구조로 파드를 외부에 노출하고 부하를 분산한다. 아래 사진을 참고하여 위의 사진과 구조를 비교해보자.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-15-04-07.png){: p}

<br>

노드포트의 구조와 비교해봤을 때 매우 단순하다. 이는 클라우드 환경에서 동작하는 방식이다. 사용자가 클라우드 노드밸러스 타입에 접근한지는 모른다 즉 보여지지 않지만 거기에 접근해서 바로 **Load Balancer 서비스의 External IP**(그림의 노란색 부분)에 접근한 이후에 바로 내부에 있는 파드로 연결해주게 된다. 굉장히 간결하게 동작을 한다.

<br>

온프레미스에서 로드밸러서를 사용하려면 로드밸러서를 **이미 구현해 둔 서비스업체**의 도움을 받아 **쿠버네티스 클러스터 외부**에 구현해야 한다.

<br>

온프레미스에서 로드밸런서를 사용하려면 내부에 로드밸런서 서비스를 받아주는 구성이 필요한데, 이를 지원하는 것이 **MetalLB**이다. **MetalLB**는 베어메탈(bare metal, 운영체제가 설치되지 않은 하드웨어)로 구성된 쿠버네티스에서도 로드밸런서를 사용할 수 있게 고안된 프로젝트이다. **MetalLB**는 특별한 네트워크 설정이나 구성이 있는 것이 아니라 기존의 **L2 네트워크(ARP/NDP)**와 **L3 네트워크(BGP)**로 로드밸런서를 구현한다. 그러므로 네트워크를 새로 배워야 할 부담이 없으며 연동하기도 매우 쉽다.

<br>

온프레미스 환경의 로드밸런서의 구조를 아래 사진으로 본다.

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-15-27-31.png){: p}

<br>

MetalLB 서비스는 위와 같이 동작하는데 기존의 봤던 클라우드 로드 밸런스와 굉장히 유사하다. 사용자가 서비스에 접근을 해서(순서도 1번) 서비스가 파드에 그대로 포워딩(순서도 2번)해주는 구조이다. 점선으로 표시한 부분은 MetalLB 컨트롤러와 MetalLB 스피커에서 자동으로 관리해주는 부분이다. 이것들이 자동으로 관리해줘서 로드 밸런스의 서비스가 파드에 접속할 수 있게 되는 것이다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">ARP(Address Resolution Protocol)</span>: 아이피주소에서 MAC 주소로 변환되는 과정을 거칠 때 사용하는 프로토콜</div>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">MAC 주소</span>: IP 주소와 MAC 주소가 있어야지만 서로 통신이 가능하다. 이는 TCP/IP와 OSI 7 Layer라는 통신표준에서 설계되어 있는대로 통신이 진행되기 때문이다. IP 주소는 Layer 3 네트워크에서 사용되고 MAC 주소는 Layer 2 데이터링크에서 사용되는 주소이다. 통신을 하기 위한 모든 랜카드에는 고유한 MAC 주소가 존재한다. 이는 세상에 딱 하나만 존재하는 주소다. 그렇기 때문에 MAC 주소를 알면 통신하고 싶은 장비를 찾을 수 있다. 처음 통신이 MAC 주소되는 것은 아니다. 처음에는 IP 주소로 시도된다. 예를 들어 내 컴퓨터 IP 주소가 192.168.0.100이라고 하다면 나랑 통신하는 상대방은 192.168.0.0 네트워크 대역까지 찾아온다. 그 뒤 192.168.0.100을 찾고 내 컴퓨터 맥 주소로 목적지를 변환한 뒤 최종적으로 나와 통신을 할 수 있게 된다. 즉 MAC 주소는 Media Access Control의 줄임말로 통신할 하드웨어 장비를 식별할 수 있는 고유 주소이다. </div>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">BGP(Boarder Gateway Protocol)</span>: AS와 AS 사이에서 이루어지는 라우팅 프로토콜이다.</div>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">NDP(Neighbor Discovery Protocol)</span>: IPv6의 핵심적인 프로토콜로써, 로컬 네트워크 내 이웃 노드, 주소 등의 정보를 탐색하기 위한 프로토콜</div>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">AS(Autonomous System)</span>: 동일한 라우팅 정책으로 하나의 관리자에 의하여 운영되는 네트워크(즉 한 회사나 단체에서 관리하는 라우터 집단이다.) 네트워크의 크기가 커지고, 라우팅 정보가 방대해짐에 따라서 하나의 라우팅 프로토콜로 전체 네트워크를 관리할 수 없게 되었다. 네트워크 관리 범위를 계층화하고, 라우팅 정보를 보다 효율적으로 관리하기 위해 자율 시스템이 도입되었다. 라우터는 모든 네트워크의 도달 정보를 가지지 않고 자율시스템(AS) 내의 도달 정보만을 가지면 된다.</div>

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-12-51-11.png){: p}

<br>

아래 사진은 특정 레이어에 따른 로드밸런싱을 하는 방법 들이다.

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-14-04-21.png){: p}

<br>

이 책에서는 MetalLB의 L2 네트워크로 로드밸런서를 구현한다.

MetalLB 컨트롤러는 작동 방식(Protocol, 프로토콜)을 정의하고 EXTERNAL-IP를 부여해 관리한다. MetalLB 스피커(speaker)는 정해진 작동 방식(L2/ARP, L3/BGP)에 따라 경로를 만들 수 있도록 네트워크 정보를 광고하고 수집해 각 파드의 경로를 제공한다. 이때 L2는 스피커 중에서 리더를 선출해 경로 제공을 총괄한다.

<br>

1. 디플로이먼트를 이용해 2종류(lb-hname-pods, lb-ip-pods)의 파드를 생성한다. 그리고 scale 명령으로 파드를 3개로 늘려 노드당 1개씩 파드가 배포되게 한다.

```bash
kubectl create deployment lb-hname-pods --image=sysnet4admin/echo-hname
kubectl scale deployment lb-hname-pods --replicas=3
kubectl create deployment lb-ip-pods --image=sysnet4admin/echo-ip
kubectl scale deloyment lb-ip-pods --replicas=3
```

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-16-32.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-17-03.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-20-50.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-21-37.png){: p}

<br>

2. 2종류의 파드가 3개씩 총 6개가 배포됐는지 확인한다.

<br>

```bash
kubectl get pods
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-22-35.png){: p}

<br>

3. 인그레스와 마찬가지로 사전에 정의된 오브젝트 스펙으로 MetalLB를 구성한다. 이렇게 하면 MetalLB에 필요한 요소가 모두 설치되고 독립적인 **네임스페이스(metallb-system)**도 함께 만들어진다.

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.4/metallb.yaml
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-24-17.png){: p}

<br>

4. 배포된 MetalLB의 파드가 5개(controller 1개, speaker 4개)인지 확인하고, IP와 상태도 확인한다. 스피커는 각 노드마다 설치가 된다. 컨트롤러 같은 경우는 한 개가 설치되는데 여기 있는 기능들을 관리해주는 기능을 한다. 즉 MetalLB와 관련된 파드들을 deploy했다. 이제 여기에 MetalLB가 L2 통신을 할 수 있도록 거기에 있는 IP라던가 세팅 값을 넣어주는 것들을 배포하도록 하겠다.

```bash
kubectl get pods -n metallb-system -o wide
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-26-32.png){: p}

<br>

5. 인그레스와 마찬가지로 MetalLB도 설정을 적용해야 하는데, 다음 방법으로 적용한다. 이때 오브젝트는 ConfigMap을 사용한다. **ConfigMap**은 설정이 정의된 포맷이라고 생각하면 된다.

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-25-59.png){: p}

<br>

파일의 구성을 보자

**metallb-l2config.yaml**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: nginx-ip-range
      protocol: layer2
      addresses:
      - 192.168.1.11-192.168.1.13
```

<br>

하나 하나 살펴보자

**metallb-l2config.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: ConfigMap

#이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
#오브젝트를 유일하게 구분지어 줄 데이터이다.
#서비스 이름(name)은 config이다.
metadata:

  #ConfigMap이 위치하는 네임스페이스를
  #metallb-system로 한다.
  namespace: metallb-system
  name: config

data:
  config: |

  #metallb의 세부 설정
    address-pools:
    - name: nginx-ip-range

    #metallb에서 제공하는 로드밸런서의 동작 방식이다. 즉 L2 방식이다.
      protocol: layer2

      #metallb에서 제공하는 로드밸러서의 External 주소이다.
      #이 범위 안에서 External 주소를 부여한다.
      addresses:
      - 192.168.1.11-192.168.1.13
```

<br>

6. ConfigMap이 생성됐는지 kubectl get configmap -n metallb-system 명령으로 확인한다.

<br>

```bash
kubectl get configmap -n metallb-system
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-33-20.png){: p}

<br>

7. **-o yaml** 옵션을 주고 다시 실행해 MetalLB의 설정이 올바르게 적용됐는지 확인한다.

<br>

```bash
kubectl get configmap -n metallb-system -o yaml
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-34-33.png){: p}

<br>

8. 모든 설정이 완료됐으니 이제 각 디플로이먼트(lb-hname-pods, lb-ip-pods)를 로드밸런서 서비스로 노출한다.

```bash
kubectl expose deployment lb-hname-pods --type=LoadBalancer --name=lb-hname-svc --port=80

kubectl expose deployment lb-ip-pods --type=LoadBalancer --name=lb-ip-svc --port=80
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-36-21.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-38-11.png){: p}

<br>

9. 생성된 로드밸런서 서비스별로 CLUSTER-IP와 EXTERNAL-IP가 잘 적용됐는지 확인한다. 특히 EXTERNAL-IP에 ConfigMap을 통해 부여한 IP를 확인한다. 외부와 통신할 수 있는 EXTERNAL-IP가 부여된 것을 볼 수 있다.

```bash
kubectl get services
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-40-24.png){: p}

<br>

10. EXTERNAL-IP가 잘 작동하는지도 확인해 본다. 호스트 노트북(또는 PC)에서 브라우저를 띄우고 192.168.1.11로 접속한다. 배포된 파드 중 하나의 이름이 브라우저에 표시되는지 확인한다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-41-46.png){: p}

<br>

11. 192.168.1.12를 접속해 파드에 요청 방법과 IP가 표시되는지 확인한다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-13-43-22.png){: p}

<br>

삭제 작업

```bash
kubectl delete deployment lb-hname-pods

kubectl delete deployment lb-ip-pods

kubectl delete service lb-hname-svc

kubectl delete service lb-ip-svc
```

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">부가설명</span>: 실제로 현재에 있는 시스템은 아래 사진에서 이 <bold>INTERNAL-IP</bold>를 가지고 있는데 이 IP가 외부에 노출되는 IP 성격이다. 왜냐면 현재 시스템들은 각각의 서버들이 가지고 있는 외부와 통신하는 IP를 가지고 쿠버네티스 클러스터 외부에 있는 것과 통신하기 때문에 실제적으로 이 <bold>INTERNAL-IP</bold>가 쿠버네티스 외부 딴에서 노출되는 IP라고 보는 게 좋다 지금은 VM 단에서 하고 있기 때문이다(온프레미스). 우리가 <bold>metallb-l2config.yaml</bold>에서 설정해줬던 <bold>192.168.1.11-192.168.1.13</bold> 이 범위가 외부의 노출되는 IP range로 잡아주는 것이다. 이게 약간 private network ip 같이 생겨서 부가설명을 하였다.</div>

<br>

기존의 노드포트에서 사용했을 때 인터넷 브라우저로 접근하려면 ip와 노드포트를 적어줘야 했었는데 만약에 해당 노드가 죽게 된다면 이 ip로 접근을 할 수 없었다. 그래서 실질적으로 expose하는 의미가 떨어지게 되는데 metallb를 사용하면 모든 노드에 걸쳐서 데몬셋이 생성이 되고 그 데몬셋이 리턴을 해주기 때문에 **EXTERNAL IP** 하나로 전체에 있는 클러스터의 대표 IP, 즉 VIP 성격으로 쓸 수 있는 것이다.

<br>

또 이런 생각을 해볼 수 있다.

VIP, 즉 지금 EXTERNAl 되는 IP가 **192.168.11-192.168.1.13**까지 있었는데 만약 추가로 요구사항이 있어서 VIP를 추가로 생성하는 부분에 대해서는 어떻게 할까? 이것은 걱정할 필요는 없다. 우리가 추가로 서비스를 expose하면 된다. 만약에 VIP를 새로 생성한다는 의미는 다른 종류의 deployment를 붙인다는 것이 된다. 아래 사진과 같이 새로 생성한 디플로이먼트를 expose한 경우에 우리가 잡아놓은 IP range에서 부여되는 것을 볼 수 있다.

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-17-54-13.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-17-54-52.png){: p}

<br>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">추가설명</span>: MetalLB는 우리가 앞에서 비교해봤듯이 설치가 간단하고 ConfigMap를 조금만 구성하면 바로 쓸 수 있는 것을 확인했다. 그리고 노드포트와 다르게 노드는 노드가 죽는 경우에는 서비스하기 어렵다. 사용자에게 알려줘야 한다. 하지만 MetalLB는 대표 Ip 즉 VIP 성격을 가지기 때문에 IP를 우리가 설정한 대로만 계속 가져갈 수 있는 것을 확인했다. 그리고 우리가 추가로 Deployment 할 게 있다면 거기에 자동으로 CIDR 개념으로 IP가 자동으로 할동하는 것을 봤다. 굉장히 효율적으로 동작하게 온프레미스를 만들어주는 것을 볼 수 있다. </div>

<br>

<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

<span style="color:#85144b; font-weight:bold">결론</span>: MetalLB같은 경우 지금 쭉 설명을 들었다시피 굉장히 간편하고 바로 쓸 수 있는 온프레미스 로드 밸런서이다. 그런데 이게 아래 사진을 보듯이 내부적으로 들어가게 되면 점선 부분에 의해서 효율성이 좀 떨어진다. 엄밀히 따라서 같진 않지만 노드포트와 동일하게 내부에서 L2 통신을 한다는 것은 경로를 모르기 때문에 혹은 경로를 기억하고 통신을 해야 하기 때문에 지속적으로 통신을 해서 이를 업데이트 해줘야 한다는 이야기가 된다. 즉 실질적으로 내부에 L2 스위치가 소프트웨어로 구현된 느낌으로 보면 된다. 소프트웨어로 구현되어 있는 L2 스위칭은 고속 스위칭이 되지 않기 때문에 속도나 효율적인 부분에서 좀 떨어진다. 그래서 현실적으로는 MetalLB를 프로덕션에서 enterprise, 즉 규모가 있는 곳에서 쓴다고 했을 때 MetalLB는 L3 BGP로 구현을 해서 경로를 외부에 알려주고 바로바로 경로로 올 수 있도록 구현을 한다. 그래서 네트워크 엔지니어와 상의를 해서 외부 단에 있는 라우터, BGP 라우터를 통해서 통신이 다 구현되기 때문에 BGP에 대한 개념을 알아야만 좀 더 효과적인 네트워크를 구현할 수 있다. 엄청난 속도를 바라지 않는다면 우리가 했던 L2로 구현해도 문제가 되지 않는다. 사실 성능에 큰 문제가 생기지 않는다. 왜냐면 pod를 deployment하고 pod를 쓰고 scale out하는 부분에 대해서 많은 성능 저하가 일어나지 않는다 당장 쓰는데는 크게 문제가 없지만 규모 큰 규모, 조금이라도 성능 향상 효과적인 네트워크를 구성을 한다고 한다면 L3의 BGP로 구성하는 게 맞다. 그래서 네트워크 엔지니어와 상담해야 한다.</div>

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-15-27-31.png){: p}
