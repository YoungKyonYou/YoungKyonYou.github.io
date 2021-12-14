---
layout: post
title: 사용 목적별로 연결하는 인그레스
date: 2021-07-31 11:00:00 0000
tags: [Kubernetes, Ingress]
categories: [Kubernetes]
description: Ingress 실습
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

<br><br>
_**피곤한데 커피 한잔만 마시고 시작해보자..**_
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

# <center>사용 목적별로 연결하는 인그레스</center>

<br>

**노드포트 서비스**는 포트를 중복 사용할 수 없어서 1개의 노드포트에 1개의 디플로이먼트만 적용된다. 여러 개의 디플로이먼트가 있을 때 그 수만큼 노드포트 서비스를 구동하기 위해서는 **인그레스**를 사용한다. **인그레스(Ingress)**는 고유한 주소를 제공해 사용 목적에 따라 다른 응답을 제공할 수 있고 트래픽에 대한 L4/L7 로드밸런서와 보안 인증서를 처리하는 기능을 제공한다.

<br>

**인그레스**를 사용하려면 <span style="color:orange; font-weight:bold">인그레스 컨트롤러</span>가 필요하다. 다양한 인그레스 컨트롤러가 있지만, 여기서는 쿠버네티스에서 프로젝트로 지원하는 <span style="color:orange; font-weight:bold">NGINX 인그레스 컨트롤러(NGINX Ingress controller)</span>로 구성해 본다. 여기서는 <span style="color:orange; font-weight:bold">NGINX 인그레스 컨트롤러</span>가 다음 단계로 동작한다.

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<style>
.webnots-notification-box {
-moz-border-radius: 5px;
-webkit-border-radius: 5px;
border-radius: 5px;
color: #ffffff;
font-family: verdana, 'open sans', sans-serif;
margin-bottom: 25px;
padding: 10px 14px 10px 44px;
position: relative;
box-shadow: 0px 1px 5px #999;
/* width: -moz-fit-content;
width: -webkit-fit-content;
width: fit-content; */
}
.webnots-notification-box:before {
font-family: FontAwesome;
font-size: 21px;
left: 14px;
position: absolute;
}
.webnots-success {
background-color: #2ecc71;
}
.webnots-success:before {
content: "\f00c";
margin-left: -2px;
}
.webnots-failure {
background-color: #e74c3c;
}
.webnots-failure:before {
content: "\f00d";
}
.webnots-warning {
background-color: #e67e22;
}
.webnots-warning:before {
content: "\f12a";
margin-left: 5px;
}
.webnots-information {
background-color: #3498db;
}
.webnots-information:before {
content: "\f129";
margin-left: 4px;
}
.webnots-question {
background-color: #f1c40f;
}
.webnots-question:before {
content: "\f128";
margin-left: 2px;
}
.webnots-tip {
background-color: #16a085;
}
.webnots-tip:before {
content: "\f0eb";
margin-left: 2px;
}
.webnots-notice {
background-color: #bea474;
}
.webnots-notice:before {
content: "\f0a1";
margin-left: -1px;
}
</style>

<div class="webnots-success webnots-notification-box">사용자는 노드마다 설정된 노드포트를 통해 노드포트 서비스로 접속한다</div>
<div class="webnots-success webnots-notification-box">NGINX 인그레스 컨트롤러는 사용자의 접속 경로에 따라 적합한 클러스터 IP 서비스로 경로를 제공한다</div>
<div class="webnots-success webnots-notification-box">클러스터 IP 서비스는 사용자를 해당 파드로 연결해 준다</div>

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

인그레스 컨트롤러는 파드와 직접 통신할 수 없어서 노드포트 또는 로드밸런서 서비스와 연동되어야 한다. 그래서 <span style="color:orange; font-weight:bold">노드포트</span>로 이를 연동했다.</div>

<br>

인그레스 컨트롤러의 궁극적인 목적은 <span style="color:red; font-weight:bold">사용자가 접속하는 경로에 따라 다른 결괏값을 제공하는 것이다.</span>

<br>

1. 테스트용으로 디플로이먼트 2개(<span style="color:#2ECC40; font-weight:bold">in-hname-pod, in-ip-pod)</span>)를 배포한다.

<br>

```bash
kubectl create deployment in-hname-pod --image=sysnet4admin/echo-hname
kubectl create deployment in-ip-pod --image=sysnet4admin/echo-ip
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-21-10-44.png){: p}

<br>

2. 배포된 노드의 상태를 확인한다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-21-11-13.png){: p}

<br>

3. NGINX 인그레스 컨트롤러를 설치한다. 여기에는 많은 종류의 오브젝트 스펙이 포함된다. 설치되는 요소들은 NGINX 인그레스 컨트롤러 서비스를 제공하기 위해 미리 지정돼 있다.

<br>

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.2/ingress-nginx.yaml
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-21-14-12.png){: p}

<br>

4. NGINX 인그레스 컨트롤러의 파드가 배포됐는지 확인한다. **NGINX 인그레스 컨트롤러**는 default 네임스페이스가 아닌 <span style="color:orange; font-weight:bold">ingress-nginx</span> 네임스페이스에 속하므로 <span style="color:orange; font-weight:bold">-n ingress-nginx</span> 옵션을 추가해야 한다. 여기서 **-n**은 **namespace**의 약어로, default 외의 네임스페이스를 확인할 때 사용하는 옵션이다. 파드뿐만 아니라 서비스를 확인할 때도 동일한 옵션을 준다.

```bash
kubectl get pods -n ingress-nginx
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-21-17-35.png){: p}

<br>

인그레스를 위한 설정 파일은 다음과 같다. 이 파일은 들어오는 <span style="color:orange; font-weight:bold">주소 값과 포트</span>에 따라 노출된 서비스를 연결하는 역할을 설정한다. 외부에서 **주소 값과 노드포트**를 가지고 들어오는 것은 <span style="color:orange; font-weight:bold">hname-svc-default</span> 서비스와 연결된 파드로 넘기고, 외부에서 들어오는 주소 값, 노드포트와 함께 뒤에 /ip를 추가한 주소 값은 **ip-svc** 서비스와 연결된 파드로 접속하게 설정했다.

먼저 <span style="color:#3D9970; font-weight:bold">ingress-config.yaml</span>를 살펴보자

<br>

**ingress-config.yaml**

```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: ingress-nginx
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - http:
        paths:
          - path:
            backend:
              serviceName: hname-svc-default
              servicePort: 80
          - path: /ip
            backend:
              serviceName: ip-svc
              servicePort: 80
          - path: /your-directory
            backend:
              serviceName: your-svc
              servicePort: 80
```

<br>

하나 하나 알아가보자

**ingress-config.yaml**

```yaml
#사용할 api 버젼을 명시한다.
apiVersion: networking.k8s.io/v1beta1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Ingress

#이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
#오브젝트를 유일하게 구분지어 줄 데이터이다.
#서비스 이름(name)은 ingress-nginx이다.
metadata:
  name: ingress-nginx

  #쿠버네티스 어노테이션을 사용하여 임의의 비-식별 메타데이터를 오브젝트에 첨부할 수 있다.
  #도구 및 라이브러리와 같은 클라이언트는 이 메타데이터를 검색할 수 있다.
  annotations:
    #nginx.ingress.kubernetes.io을 Prefix로 하는 Annotation은 Nginx를 위한 것이다
    #이 Prefix는 Nginx의 YAML 파일에서 확인할 수 있는 실행 옵션에 설정되어 있다.
    #이는 곧 Ingress의 규칙 또는 설정을 적용할 Nginx Ingress Controller를 선택적으로
    #사용할 수 있다는 것을 의미한다.
    #nginx.ingress.kubernetes.io/rewrite-target는 트래픽을 리디렉션해야 하는 대상 URI이다. 즉
    #rule의 path에 지정된 경로를 해당 주석에 설정된 경로로 Redirect 한다. 여기선 /로 Redirect한다.
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  #규칙 지정
  rules:
    #http에 대한 프로토콜 및 포트 지정이다
    - http:
        paths:
          #기본 경로 규칙이다.
          #외부에서 주소 값과 노드포트를 가지고 들어오는 것은
          #hname-svc-default 서비스와 연결된 파드로 넘긴다.
          - path:

            backend:
              #나중에 expose 명령으로 디플로이먼트 (in-hname-pod)를 서비스로 노출할 것이다.
              #expose할 때 이름이 hname-svc-default를 가지게 한다.
              #연결되는 서비스와 포트를 명시
              serviceName: hname-svc-default
              servicePort: 80

            #기본 경로에 ip라는 이름의 경로 추가
            #외부에서 주소 값과 노트포트와 함께 뒤에 /ip를 추가한 주소 값은
            #ip-svc 서비스와 연결된 파드로 접속하게 설정했다.
          - path: /ip

            backend:
              #나중에 expose 명령으로 디플로이먼트 (in-hname-pod)를 서비스로 노출할 것이다.
              #expose할 때 이름이 ip-svc를 가지게 한다.
              #연결되는 서비스와 포트를 명시
              serviceName: ip-svc
              servicePort: 80

            #기본 경로에 your-directory 경로 추가
          - path: /your-directory

            #연결되는 서비스와 포트
            backend:
              serviceName: your-svc
              servicePort: 80
```

**[사진 참고]**
![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-21-32-44.png){: p}

<br>

제대로 생성되었는지 확인하기 위해서는 -n 옵션을 사용해야 한다. 네임스페이스가 다르기 때문이다.

```bash
kubectl get pods -n ingress-nginx
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-22-32-44.png){: p}

<br>

5. 설정을 적용한다.

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.2/ingress-config.yaml
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-23-33-27.png){: p }

<br>

6. 인그레스 설정 파일이 제대로 등록됐는지 확인한다.

<br>

```bash
kubectl get ingress
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-23-36-46.png){: p}

<br>

7. \*\*kubectl get ingress -o yaml을 실행해 인그레스에 요청한 내용이 확실하게 적용됐는지 확인한다. 이 명령은 인그레스에 적용된 내용을 야믈 형식으로 출력해 적용된 내용을 확인할 수 있다. 우리가 적용한 내용 외에 시스템에서 자동으로 생성하는 것까지 모두 확인할 수 있으므로 이 명령을 응용하면 오브젝트 스펙 파일을 만드는 데 도움이 된다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-23-44-36.png){: p}

<br>

8. NGINX 인그레스 컨트롤러 생성과 인그레스 설정을 완료했다. 이제 **외부에서 NGINX 인그레스 컨트롤러에 접속**할 수 있게 노드포트 서비스로 NGINX 인그레스 컨트롤러를 **외부에 노출**한다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-23-46-23.png){: p}

<br>

적용하는 코드를 살펴보자.

**ingress.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-ingress-controller
  namespace: ingress-nginx
spec:
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30100
    - name: https
      protocol: TCP
      port: 443
      targetPort: 443
      nodePort: 30101
  selector:
    app.kubernetes.io/name: ingress-nginx
  type: NodePort
```

<br>

한 줄 한 줄 살펴보자.

**ingress.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Service

#이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
#오브젝트를 유일하게 구분지어 줄 데이터이다.
#서비스 이름(name)은 nginx-ingress-controller.

metadata:
  name: nginx-ingress-controller

  #NGINX 인그레스 컨트롤러가 위치하는 네임스페이스를
  #ingress-nginx로 한다.
  namespace: ingress-nginx

spec:
  ports:
    - name: http
      protocol: TCP

      #http를 처리하기 위해 30100번 포트로 들어온 요청을
      #80번 포트로 넘긴다.
      port: 80
      #내부에 있는 컨테이너를 연결해주기 위하여 80포트를 사용하는 것이다.
      targetPort: 80
      nodePort: 30100

    - name: https
      protocol: TCP

      #https를 처리하기 위해 30101번 포트로 들어온 것을
      #443번 포트로 넘긴다.
      port: 443
      #내부에 있는 컨테이너를 연결해주기 위하여 443포트를 사용하는 것이다.
      targetPort: 443
      nodePort: 30101

      #NGINX 인그레스 컨트롤러의 요구 사항에 따라
      #셀렉터를 ingress-nginx로 지정한다.
      #즉 ingress-nginx라는 이름을 통해서 통신할 ingress 컨트롤러를 확인한다.
      #위의 ingress-config.yaml에서 metadata.name이 ingress-nginx이다.
  selector:
    app.kubernetes.io/name: ingress-nginx

  #서비스 타입을 설정
  type: NodePort
```

<br>

9. 노드포트 서비스로 생성된 <span style="color:orange; font-weight:bold">NGINX 인그레스 컨트롤러(nginx-ingress-controller)</span>를 확인한다. 이때도 -n ingress-nginx(ingress.yaml를 작성할 때 metadata.namespace를 ingress-nginx로 위치하게 했음)로 네임스페이스를 지정해야만 내용을 확인할 수 있다.

<br>

```bash
kubectl get services -n ingress-nginx
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-07-31-23-59-09.png){: p}

<br>

10. <span style="color:orange; font-weight:bold">expose</span> 명령으로 디플로이먼트(**in-hname-pod, in-ip-pod)**도 서비스로 노출한다. 외부와 통신하기 위해 클러스터 내부에서만 사용하는 파드를 클러스터 외부에 노출할 수 있는 구역으로 옮기는 것이다.

<br>

```bash
kubectl expose deployment in-hname-pod --name=hname-svc-default --port=80,443

kubectl expose deployment in-ip-pod --name=ip-svc --port=80,443
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-00-02-59.png){: p}

<br>

11. 생성된 서비스를 점검해 디플로이먼트들이 서비스에 정상적으로 노출되는지 확인한다. 새로 생성된 서비스는 default 네임스페이스에 있으므로 -n 옵션으로 네임스페이스를 지정하지 않아도 된다.

<br>

```bash
kubectl get services
```

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-00-04-13.png){: p}

<br>

12. 이제 호스트 노트북(또는 PC)에서 웹 브라우저를 띄우고 **192.168.1.101:30100**에 접속해 외부에서 접속되는 경로에 따라 다르게 작동하는지 확인한다. 이때 워커 노드 IP는 **192.168.1.101이 아닌 102 또는 103을** 사용해도 무방하다. 파드 이름이 웹 브라우저에 표시되는지도 확인한다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-00-11-53.png){: p}

<br>

13. 이번에는 경로를 바꿔서 **192.168.1.101:30100** 뒤에 **/ip**를 추가해 본다.

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-00-12-12.png){: p}

<br>

14. **https://192.168.1.101:30101**으로 접속해 HTTP 연결이 아닌 **HTTPS** 연결도 정상적으로 작동하는지 확인한다. **30101**은 **HTTPS**의 포트인 **443**번으로 변환해 접속된다.

<br>

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-11-00-45.png){: p}

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-11-01-13.png){: p}

<br>

<div class="webnots-warning webnots-notification-box">https 접속할 때 그냥 ip:port 만 적으면 애라 사진과 같이 나올 수 있다. 이럴 땐 https://ip:port 이렇게 적는다.</div>

<br>

![](/images/Kubernetes/kubernetes-Ingress/2021-08-01-11-02-22.png){: p}

<br>

<div class="webnots-warning webnots-notification-box">브라우저에 따라 경고 메시지가 뜰경우 고급 > 주소(안전하지 않음)(으)로 이동을 클릭하면 접속된다.</div>

<br>

**디플로이먼트와 서비스 및 NGINX 인그레스 컨트롤러와 관련된 내용 삭제**

```bash
kubectl delete deployment in-hname-pod
kubectl delete deployment in-ip-pod
kubectl delete services hname-svc-default
kubectl delete services ip-svc

kubectl delete -f ~/_Book_k8sInfra/ch3/3.3.2/ingress-nginx.yaml
kubectl delete -f ~/_Book_k8sInfra/ch3/3.3.2/ingess-config.yaml
```
