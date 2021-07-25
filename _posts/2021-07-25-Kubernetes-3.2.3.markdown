---
layout: post
title: 컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커-3.2.3
date: 2021-07-25 09:00:00 0000
tags: [Kubernetes, yaml, pod-template]
categories: [Kubernetes]
description: 레플리카셋으로 파드 수 관리하기
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

# <center>레플리카셋으로 파드 수 관리하기</center>

<br>

많은 사용자를 대상으로 웹 서비스를 하려면 다수의 파드가 필요하다. 그래서 쿠버네티스에서는 다수의 파드를 만드는 레플리카셋 오브젝트를 제공한다.
<br>
디플로이먼트로 생성한 파드여야 replica 옵션을 사용할 수 있다.

<br>

```bash
//sysnet4admin/echo-hname은 도커 허브에서 해당되는 이미지를 가져온다
kubectl create deployment dpy-hname --image=sysnet4admin/echo-hname
```

<br>

통해서 디플로이먼트를 생성한다.

```bash
kubectl scale deployment echo-hname --replicas=3
```

<br>

위 명령을 통해 replica 셋을 생성할 수 있지만 한꺼번에 여러 개의 파드를 만드려면 YAML 파일로 작성해야 한다. 이러한 파일을 **오브젝트 스펙(spec)**이라 한다.

<br>

**echo-hname.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-hname
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx-test
    spec:
      containers:
        - name: echo-hname
          image: sysnet4admin/echo-hname
```

<br>

위 내용을 하나하나 알아가 보자.<br>

**echo-hname.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다. apps/v1에서는 .spec.selector 와 .metadata.labels 이
#설정되지 않으면 .spec.template.metadata.labels 은 기본 설정되지 않는다.
#그래서 이것들은 명시적으로 설정되어야 한다. 또한 apps/v1 에서는
#디플로이먼트를 생성한 후에는 .spec.selector 이 변경되지 않는 점을 참고한다.
apiVersion: apps/v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Deployment

#이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
#오브젝트를 유일하게 구분지어 줄 데이터이다.
#디플로이먼트 이름(name)은 echo-hname이다.
#차후에 이 디플로이먼트를 delete할 때 이 이름으로 지운다.
metadata:
  name: echo-hname

  #오브젝트에 첨부된 카와 값의 쌍이다. 레이블은 오브젝트 특성을
  #식별하는 데 사용되어 사용자에게 중요하지만
  #코어 시스템에 직접적인 의미는 없다.
  labels:
    app: nginx

#오브젝트에 대해 어떤 상태를 의도하는지 명시한다.
spec:
  #필드에 따라 디플로이먼트는 3개의 레플리카 파드를 생성
  replicas: 3

  #(.spec.selector)디플로이먼트가 관리할 파드를 찾는 방법을 정의한다.
  #이 사례에서는 파드 템플릿(아래 명시된 template)에 정의된 레이블(app:nginx)을
  #선택한다. 그러나 파드 템플릿(아래 명시된 template을 말함) 자체의 규칙이 만족되는 한,
  #보다 정교한 선택 규칙의 적용이 가능하다.
  selector:
    matchLabels:
      app: nginx

  #template 필드에는 다음 하위 필드가 포함된다
  template:
    #파드는 .metadata.labels 필드를 사용해서
    #app: nginx레이블을 붙인다
    metadata:
      #이 레이블을 담으로써 위에 selector에서 관리할 파드를 찾을 수 있다.
      labels:
        app: nginx

    #.template.spec 필드는 파드가 도커 허브의
    #sysnet4admin/echo-hname 이미지를 실행하는
    #nginx 컨테이너 1개를 실행하는 것을 나타낸다
    #컨테이너 1개를 생성하고 .spec.template.spec.containers[0].name 필드를
    #사용해서 echo-hname 이라는 이름을 붙인다.
    #즉 컨테이너의 이름이 echo-hname이 된다. describe deployment 명령어로 확인 가능
    spec:
      containers:
        - name: echo-hname
          #컨테이너 이미지는 도커허브에 있는 sysnet4admin/echo-hname을 가져온다.
          image: sysnet4admin/echo-hname
```

 <br>

그리고 이제

 <br>

```bash
kubectl create -f echo-hname.yaml
```

명령으로 실행해본다.
