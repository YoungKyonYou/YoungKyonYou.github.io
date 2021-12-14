---
layout: post
title: PV와 PVC
date: 2021-08-15 12:00:00 0000
tags: [Kubernetes, PV, PVC, nfs]
categories: [Kubernetes]
description: PV와 PVC 다루기
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

# <center>PV와 PVC</center>

<br>

파드에서 생성한 내용을 기록하고 보관하거나 모든 파드가 동일한 설정 값을 유지하고 관리하기 위해 공유된 볼륨으로부터 공통된 설정을 가지고 올 수 있도록 설계해야 할 때가 있다. 쿠버네티스는 이런 경우를 위해 다음과 같은 목적으로 다양한 형태의 볼륨을 제공한다.

<br>

- <span style="color:#3D9970; font-weight:bold">임시:</span> emptyDir<br><br>
- <span style="color:#3D9970; font-weight:bold">로컬:</span> host Path, local<br><br>
- <span style="color:#3D9970; font-weight:bold">원격:</span> PersistentVolumeClaim, cephfs, cinder, csi, fc(fibre channel), flexVolume, flocker, glusterfs, iscsi, nfs, portworxVolume, quobyte, rbd, scaleIO, storageos, vsphereVolume<br><br>
- <span style="color:#3D9970; font-weight:bold">특수 목적:</span> downwardAPI, configMap, secret, azureFile, projected<br><br>
- <span style="color:#3D9970; font-weight:bold">클라우드:</span> awsElasticBlockStore, azureDisk, gcePersistentDisk<br><br>

<br>

쿠버네티스는 필요할 때 PVC(PersistentVolumeClaim, 지속적으로 사용 가능한 볼륨 요청)를 요청해 사용한다. PVC를 사용하려면 PV(PersistentVolume, 지속적으로 사용 가능한 볼륨)로 볼륨을 선언해야 한다. 간단하게 PV는 볼륨을 사용할 수 있게 준비하는 단계이고, PVC는 준비된 볼륨에서 일정 공간을 할당받는 것이다. 비유하면 PV는 요리사(관리자)가 피자를 굽는 것이고, PVC는 손님(사용자)가 원하는 만큼의 피자를 접시에 담아 가져오는 것이다.

<br>

그러면 가장 구현하기 쉬운 NFS 볼륨 타입으로 PV와 PVC를 생성하고 파드에 마운트해 보면서 실제로 어떻게 작동하는지 확인해 본다.

<br>

1. PV로 선언할 볼륨을 만들기 위해 NFS 서버를 마스터 노드에 구성한다. 공유되는 디렉터리는 /nfs_shared로 생성하고, 해당 디렉터리를 NFS로 받아들일 IP 영역은 192.168.1.0/24로 정한다. 옵션을 적용해 /etc/exports에 기록한다.

<br>

```bash
mkdir /nfs_shared
vi /etc/exports
```

<br>

위 명령을 입력하면 exports 파일이 열어지는데 여기서 권한 및 NFS로 받아들일 IP 영역을 설정해 줘야 한다.

파일 내에 다음 내용을 입력한다.

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-18-50-57.png){: p}

<br>

위의 사진처럼 다 입력할 필요가 없다. 나는 현재 프로메테우스와 그라파나를 사용중이여서 뭐가 많은데 이번 실습에서 필요한 건 아래와 같다.

**/etc/exports**

```bash
/nfs_shared 192.168.1.0/24(rw,sync,no_root_squash)
```

<br>

- rw는 읽기/쓰기를 가능하게 해준다<br><br>

- sync는 쓰기 작업 동기화를 가능하게 해준다<br><br>

- no_root_squash는 root 계정 사용을 의미한다. NFS 서버에도 root 사용자가 있을 것이고, NFS 클라이언트에도 root가 있을 것이다. 그러나 두 root가 같은 root가 될 순 없다. NFS 클라이언트의 root가 NFS 서버의 root 권한을 가질 수 없다. 따라서 기본값은 root_squash로 클라이언트 root는 nobody와 같은 사용자로 맵핑되어 버린다. 서버와 클라언트의 root 사용자를 일치하도록 하려고 no_root_squash라고 적는 것이다.<br><br>

<br>

위 명령을 통해서 나중에 파드에서 마운트되는 디렉토리에서 읽고 쓸 수 있는 권한이 생기게 된다.

<br>

2. 해당 내용을 시스템에 적용해 NFS 서버를 활성화하고 다음에 시작할 때도 작동으로 적용되도록 systemctl enable --now nfs 명령을 실행한다.

<br>

```bash
systemctl enable --now nfs
```

<br>

3. 다음 경로에 있는 오브젝트 스펙을 실행해 PV를 생성한다.

<br>

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pv.yaml
```

<br>

**nfs-pv.yaml**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 192.168.1.10
    path: /nfs_shared
```

<br>

이제 하나 하나 씩 알아가 보자.

<br>

**nfs-pv.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: PersistentVolume

#PV의 이름을 설정한다 이름을 nfs-pv로 한다.
metadata:
  name: nfs-pv

spec:
  capacity:
    #storage는 실제로 사용하는 용량을 제한하는 것이 아니라 쓸 수 있는 양을 레이블로 붙이는 것과 같다. 이는 현재 스토리지가 단순히 NFS로 설정돼서 그렇다.
    storage: 100Mi

  #PV를 어떤 방식으로 사용할지를 정의한다. ReadWriteMany는 여러 개의 노드가 읽고 쓸 수
  # 있도록 마운트하는 옵션이다. 이외에도 ReadWriteOnce(하나의 노드에서만 볼륨을 읽고 쓸 수 있게 마운트)와
  #ReadOnlyMany(여러 개의 노드가 읽도록 마운트) 옵션이 있다.
  accessModes:
    - ReadWriteMany

  #볼륨에 대한 반환 정책으로 Retain, Recycle, 그리고 Delete가 있다.
  #Retain은 PVC가 삭제되어 Released 상태가 되어도 실제 내부의
  #파일을 삭제하지 않는 정책이다
  #한 가지 알아둬야 할 점은 Released 상태의 PV는 다른 PVC에 의해 사용될 수 있는 상태는 아니며,
  #이는 해당 PV에 아직 데이터가 남아있기(Retain) 때문이라고 한다.
  #Delete 정책은 PVC가 삭제되어 PV가 Released 상태가 되면 PV와 연결된 디스크 내부 자체를 삭제하는것이다
  #Recycle은 NFS와 HostPath를 사용하는 PV에 적용할 수 있는 방식으로, 사용하던 볼륨 내부의 파일을 전부 삭제(scrub)한다.
  #마치 rm -rf 를 사용하는 것과 동일하다고 볼 수 있으며,
  #프로비저닝된 스토리지 자체를 삭제하지는 않는다는 점에서 Delete 방식과는 다르다고 볼 수 있다.
  persistentVolumeReclaimPolicy: Retain

  nfs:
    #
    server: 192.168.1.10
    #우리가 위에서 생성한 디렉터리랑 바인딩한다.
    path: /nfs_shared
```

<br>

4. kubectl get pv를 실행해 생성된 PV의 상태가 <span style="color:orange; font-weight:bold">Available</span>(사용 가능)임을 확인한다.

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-11-30.png){: p}

<br>

위 사진에서 grafana는 내가 이전에 만든 것이므로 무시하고 <span style="color:orange; font-weight:bold">nfs-pv</span>의 <span style="color:orange; font-weight:bold">Status</span>가 <span style="color:orange; font-weight:bold">Available</span>인지 확인한다.

<br>

5. 다음 경로에서 오브젝트 스펙을 실행해 PVC를 생성한다.

<br>

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pvc.yaml
```

<br>

**nfs-pvc.yaml**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 10Mi
```

<br>

한 줄 한 줄 알아가 보자.

<br>

**nfs-pvc.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: PersistentVolumeClaim
metadata:
  #PVC의 이름을 설정한다 이름을 nfs-pvc로 한다.
  name: nfs-pvc
spec:
  #PVC를 어떤 방식으로 사용할지를 정의한다. ReadWriteMany는 여러 개의 노드가 읽고 쓸 수
  # 있도록 마운트하는 옵션이다. 이외에도 ReadWriteOnce(하나의 노드에서만 볼륨을 읽고 쓸 수 있게 마운트)와
  #ReadOnlyMany(여러 개의 노드가 읽도록 마운트) 옵션이 있다.
  accessModes:
    - ReadWriteMany

  resources:
    requests:
      #요청하는 storage: 10Mi는 동적 볼륨이 아닌 경우에는
      #레이블 정도의 의미만을 가진다.
      storage: 10Mi
```

<br>

```bash
kubectl get pv
```

<br>

위 명령을 사용해서 상태가 <span style="color:orange; font-weight:bold">Bound(묶여짐)</span>로 변경됨을 확인한다. PV와 PVC가 연결된 것이다.

<br>

용량이 설정한 10Mi가 아닌 100Mi인 것은 동적으로 PVC를 따로 요청해 생성하는 경우가 아니면 의미가 없다. 따라서 <span style="color:orange; font-weight:bold">Bound</span>만 확인하면 된다.

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-18-43.png){: p}

<br>

생성한 PVC를 볼륨으로 사용하는 디플로이먼트 오브젝트 스펙을 배포한다.

<br>

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pvc-deploy.yaml
```

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-21-46.png){: p}

<br>

위 사진을 보면 파드가 4개가 만들어진 것을 볼 수 있다. 해당 yaml 파일을 봐 보자.

<br>

**nfs-pcv-deploy.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-pvc-deploy
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nfs-pvc-deploy
  template:
    metadata:
      labels:
        app: nfs-pvc-deploy
    spec:
      containers:
        - name: audit-trail
          image: sysnet4admin/audit-trail
          volumeMounts:
            - name: nfs-vol
              mountPath: /audit
      volumes:
        - name: nfs-vol
          persistentVolumeClaim:
            claimName: nfs-pvc
```

<br>

한 줄 한 줄 해석해 보자.

<br>

**nfs-pcv-deploy.yaml**

```yaml
#api 버젼을 명시한다.
apiVersion: apps/v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: Deployment

#오브젝트를 유일하게 구분지어 줄 데이터이다.
#서비스 이름(name)은 nfs-pvc-deploy이다..
metadata:
  name: nfs-pvc-deploy

spec:
  #파드를 4개를 만드다.
  replicas: 4
  selector:
    #(.spec.selector)디플로이먼트가 관리할 파드를 찾는 방법을 정의한다.
    #이 사례에서는 파드 템플릿(아래 명시된 template)에 정의된 레이블(app:nfs-pvc-deploy)을 선택한다.
    matchLabels:
      app: nfs-pvc-deploy
  template:
    metadata:
      labels:
        app: nfs-pvc-deploy
    spec:
      #컨테이너 이름 명시
      containers:
        - name: audit-trail

          #도커 허브에서 해당 이미지를 가져와 쓴다.
          image: sysnet4admin/audit-trail

          #볼륨이 만운트될 위치(/audit)를 지정한다
          #즉 /nfs_shared 디렉터리를 /audit과 동기화 시키는 것이다.
          volumeMounts:
            - name: nfs-vol
              mountPath: /audit
      volumes:
        #PVC로 생성된 볼륨을 마운트하기 위해서 nfs-pvc라는 이름을 사용한다.
        - name: nfs-vol
          persistentVolumeClaim:
            claimName: nfs-pvc
```

<br>

자 이제 exec 명령을 사용해서 4개의 파드 중 하나에 접속한다.

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-31-39.png){: p}

<br>

```bash
kubectl exec -it nfs-pvc-deploy-5fd9876c46-2ntgz -- /bin/bash
```

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-32-14.png){: p}

<br>

/audit 디렉터리로 이동한다.

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-32-36.png){: p}

<br>

audit 디렉토리에서 ls 명령을 치면 내가 이전에 만든 grafana와 prometheus가 있다. 여기에 새로운 파일 하나를 만들어본다.

<br>

```bash
touch test.txt
```

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-34-01.png){: p}

<br>

이제 해당 파드에서 exit하고 다른 파드로 접속해 본다.

```bash
kubectl exec -it nfs-pvc-deploy-5fd9876c46-2ntgz -- /bin/bash
```

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-36-07.png){: p}

<br>

위의 사진과 같이 ls 명령으로 확인해보니 다른 파드에서 만든 <span style="color:orange; font-weight:bold">test.txt</span>가 있는 것을 볼 수 있다. 즉 볼륨이 공유되는 것이다.

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-information webnots-notification-box">우리가 이 /audit 디렉토리에서 자유롭게 읽고 쓸 수 있는 이유는 앞에서 /etc/exports에 권한을 명시해줬기 때문이다. </div>

<br>

현재 나는 이 실습을 하는 것 외에 프로메테우스와 그라파나를 nfs 볼륨에 연동하여 쓰고 있으므로 아래 사진과 같이 설정이 좀 많다. 이렇게 설정해줌으로써 위에서 생성했던 파드에 접속해서 /audit 디렉토리에서 prometheus 디렉터리와 grafana 디렉터리에 들어가서 파일을 생성, 삭제, 수정, 읽기가 가능하다.

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-38-36.png){: p}

<br>

<div class="webnots-warning webnots-notification-box">위와 같이 설정을 해주지 않는다면 아래 사진과 같은 에러가 발생한다.</div>

<br>

![](/images/Kubernetes/Kubernetes-PV-PVC/2021-08-15-19-40-53.png){: p}

<br>

이를 위해서 /etc/exports에 명시를 꼭 해줘야하며 nfs 서버가 켜진 상태에서 고칠 경우 꼭 <span style="color:#85144b; font-weight:bold">nfs restart</span>를 해줘야 한다. 안 그러면 적용이 되지 않는다! nfs 서버를 다시 시작하는 명령어는 아래와 같다.

<br>

```bash
systemctl restart nfs
```

<br>

**[nfs 관련 참고 링크](https://coding-chobo.tistory.com/27)**
