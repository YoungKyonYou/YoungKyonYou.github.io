---
layout: post
title: 프로메테우스로 모니터링 데이터 수집과 통합하기-2
date: 2021-08-11 10:00:00 0000
tags: [Kubernetes, MetalLB, Prometheus]
categories: [Kubernetes]
description: 프로메테우스 설치하기
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

# <center>프로메테우스로 모니터링 데이터 수집과 통합하기</center>

<br>

이전 게시물에서 프로메테우스를 설치하기 위한 사전작업을 진행하였다. 이제 프로메테우스 설치를 위한 사전에 준비한 스크립트를 실행한다.

**prometheus-server-preconfig.sh**

```bash
#!/usr/bin/env bash

# check helm command
echo "[Step 1/4] Task [Check helm status]"
if [ ! -e "/usr/local/bin/helm" ]; then
  echo "[Step 1/4] helm not found"
  exit 1
fi
echo "[Step 1/4] ok"

# check metallb
echo "[Step 2/4] Task [Check MetalLB status]"
namespace=$(kubectl get namespace metallb-system -o jsonpath={.metadata.name} 2> /dev/null)
if [ "$namespace" == "" ]; then
  echo "[Step 2/4] metallb not found"
  exit 1
fi
echo "[Step 2/4] ok"

# create nfs directory & change owner
nfsdir=/nfs_shared/prometheus/server
echo "[Step 3/4] Task [Create NFS directory for prometheus-server]"
if [ ! -e "$nfsdir"  ]; then
  ~/_Book_k8sInfra/ch6/6.2.1/nfs-exporter.sh prometheus/server
  chown 1000:1000 $nfsdir
  echo "$nfsdir created"
  echo "[Step 3/4] Successfully completed"
else
  echo "[Step 3/4] failed: $nfsdir already exists"
  exit 1
fi

# create pv,pvc
echo "[Step 4/4] Task [Create PV,PVC for prometheus-server]"
pvc=$(kubectl get pvc prometheus-server -o jsonpath={.metadata.name} 2> /dev/null)
if [ "$pvc" == "" ]; then
  kubectl apply -f ~/_Book_k8sInfra/ch6/6.2.1/prometheus-server-volume.yaml
  echo "[Step 4/4] Successfully completed"
else
  echo "[Step 4/4] failed: prometheus-server pv,pvc already exist"
fi
```

<br>

한 줄 한 줄씩 알아가 보자.

<br>

**prometheus-server-preconfig.sh**

```bash
#!/usr/bin/env bash

# check helm command
#터미널에 해당 내용을 출력한다.
echo "[Step 1/4] Task [Check helm status]"

#if[조건] 조건 양 옆에 '['와 ']' 사이에 공백이 꼭 있어야 한다.
#then 다음에 명령어가 나온다.
#-e 옵션이 파일이 존재한다는 옵션이다 즉 여기서 ! 부정을 넣었으므로 파일이 존재하지 않을 경우
#아래 echo를 출력하고 exit한다.
if [ ! -e "/usr/local/bin/helm" ]; then
  echo "[Step 1/4] helm not found"
  exit 1

#fi는 그냥 if절을 끝내는 문구이다.
fi

#아래 문구 출력
echo "[Step 1/4] ok"

# check metallb
#아래 문구 출력
echo "[Step 2/4] Task [Check MetalLB status]"

#namespace라는 변수를 선언하고 해당 값을 넣어주는 것이다.
#$() 구문으로 명령어 실행 결과를 넣을 수 있다.
#마스터 노드에서 명령어로 kubectl get namespace metallb-system -o jsonpath={.metadata.name} 2> /dev/null를
#입력하면(이전 게시물에 사전작업을 했다면) metallb-system이 출력된다 즉 이 문자열이 namespace 변수 안에 들어가게 되는 것이다.
#JSONPath 템플릿은 중괄호 {}로 둘러싸인 JSONPath 표현식으로 구성된다. Kubectl은 JSONPath 표현식을
#사용하여 JSON 오브젝트의 특정 필드를 필터링하고 출력 형식을 지정한다.
#즉 metallb-system의 metadata에 설정되어 있는 name를 검색하는 것이다. 보통 이렇게 -o josnpath해서 사용한다.
#여기서 2는 STRERR(standard error)의 의미이고 1일 땐 STDOUT(standard output)이다.
#즉 STDOUT은 표준출력으로 정상적인 메시지를 출력하고 STDERR은 표준에러로 에러메시지를 출력하는 것이다.
#일반적으로 /dev/null과 1>/dev/null은 같은 의미이다.
#/dev/null이나 1>/dev/null로 했을 경우 에러 메시지가 터미널에 출력이 된다. 그럼 해당 에러메시지를 null로 만드려면
#2>/dev/null로 하는 것이다.
#즉 이는 터미널상에서 명령어를 입력하고 그에 대한 표준 출력이 표시되지 않게 하기 위해서 자주 사용하는 방법인 것이다.
namespace=$(kubectl get namespace metallb-system -o jsonpath={.metadata.name} 2> /dev/null)

#namespace 변수가 빈 문자열일 경우
if [ "$namespace" == "" ]; then.

#아래 문구 출력하고 exit한다.
  echo "[Step 2/4] metallb not found"
  exit 1
fi
echo "[Step 2/4] ok"

# create nfs directory & change owner
#nfsdir 변수에 해당 경로 문자열을 넣는다.
nfsdir=/nfs_shared/prometheus/server

#아래 문구 출력
echo "[Step 3/4] Task [Create NFS directory for prometheus-server]"

#nfsdir 경로가 존재하지 않을 경우
if [ ! -e "$nfsdir"  ]; then

#nfs-exporter.sh의 내용은 아래에서 살표보도록 하자.
#chown은 소유자를 변경하는 명령어이다.
#리눅스에서 파일은 어떤 Owner, Group에 속해있다.
#chown 명령어는 파일의 Owner 또는 Group을 변경하는 명령어이다.
#아래는 nfsdir 변수에 담긴 디렉터리의 UID와 GID를 1000, 1000으로 변경하는 것이다
#UID값이 0일경우 관리자라 생각한다.
#UID는 값을 지정하지않으면 1000부터 시작, 그다음은 1001~...가 된다.
#값을 지정하지않으면 1000부터 시작, 그다음은 1001~ ....
#그룹이 하나일 필요는 없다.
#아래 prometheus-server-colume.yaml를 통해 /nfs_shared/prometheus/server 라는 디렉터리가 만들어진다.
#여기서는 nfs-exporter.sh로 prometheus/server라는 아규먼트를 넘긴다 그 sh에서는 $1로 아규먼트를 받음
  ~/_Book_k8sInfra/ch6/6.2.1/nfs-exporter.sh prometheus/server
  chown 1000:1000 $nfsdir
  echo "$nfsdir created"
  echo "[Step 3/4] Successfully completed"
else
  echo "[Step 3/4] failed: $nfsdir already exists"
  exit 1
fi

# create pv,pvc
echo "[Step 4/4] Task [Create PV,PVC for prometheus-server]"

#pvc라는 변수에 prometheus-server라는 문자열이 들어간다.
pvc=$(kubectl get pvc prometheus-server -o jsonpath={.metadata.name} 2> /dev/null)

#빈 문자열일 경우 즉 존재하지 않을 경우
if [ "$pvc" == "" ]; then

#해당 파일을 실행한다.
  kubectl apply -f ~/_Book_k8sInfra/ch6/6.2.1/prometheus-server-volume.yaml
  echo "[Step 4/4] Successfully completed"
else
  echo "[Step 4/4] failed: prometheus-server pv,pvc already exist"
fi
```

<br>

위에 나왔던 스크립트들을 살펴보자.

<br>

**nfs-exporter.sh**

```bash
#!/usr/bin/env bash
nfsdir=/nfs_shared/$1
if [ $# -eq 0 ]; then
  echo "usage: nfs-exporter.sh <name>"; exit 0
fi

if [[ ! -d $nfsdir ]]; then
  mkdir -p $nfsdir
  echo "$nfsdir 192.168.1.0/24(rw,sync,no_root_squash)" >> /etc/exports
  if [[ $(systemctl is-enabled nfs) -eq "disabled" ]]; then
    systemctl enable nfs
  fi
    systemctl restart nfs
fi
```

<br>

**nfs-exporter.sh**

```bash
#!/usr/bin/env bash
#prometheus-server-preconfig.sh에서 아규먼트로 넘겨진 것을 $1로 받는다
#prometheus/server가 아규먼트로 넘겨온다.
nfsdir=/nfs_shared/$1

#$#는 매개변수의 총 개수를 의미한다.
# -eq는 같음을 의미 즉 총 매개변수의 개수가 0일 경우
#then이하를 실행한다.
if [ $# -eq 0 ]; then
  echo "usage: nfs-exporter.sh <name>"; exit 0
fi

# -d 는 파일이 존재하고 디렉터리인 경우이다.
#즉 위에서 설정한 변수 nfsdir의 값에 해당하는 디렉터리가 존재하는 경우
if [[ ! -d $nfsdir ]]; then

#-p 옵션은 부모 디렉터리를 같이 생성하라는 것이다.
  mkdir -p $nfsdir

  #/etc 아래 exports 파일 안에 해당 내용을 넣으라는 것이다.
  echo "$nfsdir 192.168.1.0/24(rw,sync,no_root_squash)" >> /etc/exports

  #systemctl은 systemd를 관리하는 명령어이다.
  #Systemd는 부팅부터 서비스관리 로그관리등의 시스템 전반적인 영역에 걸쳐있는 프로세스이다.
  #이것이 도입된 OS는 이것의 개념이나 기능등을 한번은 파악하는 것이 도움이 될 것이다.
  #이것이 도입되면 부팅시에도 병렬로 실행되어서 상당히 부팅속도가 빨리잔다.
  #$() 구문으로 명령어 실행 결과를 넣을 수 있다.
  #is-enalbed name.service를 통해 서비스의 활성화 여부를 표시할 수 있다.
  #활성화되어 있으면 enabled라고 뜨고 비활성화되어 있으면 disabled라고 뜬다.
  #즉 저 명령어를 쳐서 나오는 문자열이 disabled일 경우 then 이하가 실행된다.
  if [[ $(systemctl is-enabled nfs) -eq "disabled" ]]; then
    systemctl enable nfs
  fi
    systemctl restart nfs
fi
```

<br>

**prometheus-server-volumn.yaml**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: prometheus-server
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 192.168.1.10
    path: /nfs_shared/prometheus/server
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: prometheus-server
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
```

<br>

**prometheus-server-volume.yaml**

```yaml
#apiVersion: API 버전을 명시한다
#이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
#명시한다.
apiVersion: v1

#어떤 종류의 오브젝트를 생성하고자 하는지 명시한다.
kind: PersistentVolume

#이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여
#오브젝트를 유일하게 구분지어 줄 데이터이다.
#서비스 이름(name)은 prometheus-server이다.
metadata:
  name: prometheus-server

spec:
  capacity:
    #storage는 실제로 사용하는 용량을 제한하는 것이 아니라 쓸 수 있는 양을 레이블로
    #붙이는 것과 같다. 이는 현재 스토리지가 단순히 NFS로 설정돼서 그렇다.
    storage: 10Gi

  #PV를 어떤 방식으로 사용할지를 정의한 부분이다. ReadWriteMany는 여러 개의 노드가
  #읽고 쓸 수 있도록 마운트하는 옵션이다. 이외에도 ReadWriteOnce(하나의 노드에서만 볼륨을
  #읽고 쓸 수 있게 마운트)와 ReadOnlyMany(여러 개의 노드가 읽도록 마운트) 옵션이 있다
  accessModes:
    - ReadWriteMany

  #persistentVolumeReclaimPolicy는 PV가 제거됐을 때 PV가 작동하는 방법을 정의하는 것으로
  #여기서는 유지하는 Retain을 사용합니다. 그 외에 Delete(삭제)와 Recycle(재활용, Deprecated) 옵션이 있다.
  persistentVolumeReclaimPolicy: Retain

  #NFS 서버의 연결 위치에 대한 설정이다.
  nfs:
    server: 192.168.1.10
    path: /nfs_shared/prometheus/server
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: prometheus-server
spec:
  accessModes:
    - ReadWriteMany
  resources:
    #PV는 사용자가 요청할 볼륨 공간을 관리자가 만들고 PVC는 사용자(개발자)간 보륨을 요청하는 데
    #사용한다는 점에서 차이가 있다.
    #여기서 요청하는 storage: 10Gi는 동적 볼륨이 아닌 경우에는 레이블 정도의 의미를 가진다.
    requests:
      storage: 10Gi
```

<br>

이제 마스터노드에서 실행해 본다.

<br>

```bash
~/_Book_k8sInfra/ch6/6.2.1/prometheus-server-preconfig.sh
```

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-11-13-48-06.png){: p}

<br>

나는 이미 전에 설치한 적이 있어서 출력화면이 다를 수 있다.

이제 프로메테우스 차트를 설치하려고 준비해 둔 prometheus-install.sh를 실행해 모니터링에 필요한 3가지 프로메테우스 오브젝트(프로메테우스 서버, 노드 익스포터, 쿠버 스테이트 메트릭)를 설치한다.

<br>

```bash
~/_Book_k8sInfra/ch6/6.2.1/prometheus-install.sh
```

<br>

나는 이미 설치했으므로 따로 사진을 올리지 않는다.

**prometheus-install.sh**

```bash
#!/usr/bin/env bash
helm install prometheus edu/prometheus \
--set pushgateway.enabled=false \
--set alertmanager.enabled=false \
--set nodeExporter.tolerations[0].key=node-role.kubernetes.io/master \
--set nodeExporter.tolerations[0].effect=NoSchedule \
--set nodeExporter.tolerations[0].operator=Exists \
--set server.persistentVolume.existingClaim="prometheus-server" \
--set server.securityContext.runAsGroup=1000 \
--set server.securityContext.runAsUser=1000 \
--set server.service.type="LoadBalancer" \
--set server.extraFlags[0]="storage.tsdb.no-lockfile"

```

<br>

**prometheus-install.sh**

```bash
#!/usr/bin/env bash
#edu 차트 저장소의 prometheus 차트를 사용해 prometheus 릴리스를 설치한다.
helm install prometheus edu/prometheus \

#푸시게이트웨이를 사용하지 않도록 설정한다. 푸시게이트웨이는 짧은 작업의
#메트릭을 적재하거나 보안상 내부 접급을 제어하는 폐쇄망 등에서 프로메테우스로 데이터를
#내보내는 데 사용한다.
--set pushgateway.enabled=false \

#얼럿매니저를 사용하지 않도록 설정한다.
--set alertmanager.enabled=false \

#테인트가 설정된 노드의 설정을 무시하는 톨러레이션을 설정한다.
#톨러레이션을 설정하면 마스터 노드에도 노드 익스포터를 배포할 수 있고, 프로메테우스가
#마스터노드의 메트릭 데이터를 수집할 수 있다.
--set nodeExporter.tolerations[0].key=node-role.kubernetes.io/master \
--set nodeExporter.tolerations[0].effect=NoSchedule \
--set nodeExporter.tolerations[0].operator=Exists \

#PVC 동적 프로비저닝을 사용할 수 없는 가상 머신 환경이기 때문에 이미 만들어 놓은
#prometheus-server라는 이름의 PVC를 사용하게 설정한다.
--set server.persistentVolume.existingClaim="prometheus-server" \

#프로메테우스 서버를 구성할 때 컨테이너에 할당할 사용자 ID와 그룹 ID를 1000번으로 설정한다
--set server.securityContext.runAsGroup=1000 \
--set server.securityContext.runAsUser=1000 \

#MetalLB로부터 외부 IP를 할당받기 위해서 타입을 LoadBalancer로 설정한다
--set server.service.type="LoadBalancer" \

#프로메테우스의 설정을 변경할 때 lockfile(잠긴 파일)이 있으면 변경 작업을 실패할 수 있다.
#특히 얼럿매니저를 나중에 설치할 대 lockfile 관련 문제가 발생할 수 있으므로
#lockfile이 생성되지 않게 설정한다.
--set server.extraFlags[0]="storage.tsdb.no-lockfile"

```

<br>

프로메테우스 차트를 설치하고 나면 구성 요소인 프로메테우스 서버, 노드 익스포터, 쿠버 스테이트 메트릭이 설치됐는지 확인한다. 이때 노드 익스포터가 여러 개인 이유는 노드마다 메트릭을 수집하기 위해 데몬셋으로 설치했기 때문이다.

```bash
kubectl get pods --selector=app=prometheus
```

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-11-13-57-34.png){: p}

<br>

프로메테우스 서버에서 제공하는 웹 UI로 접속하기 위한 프로메테우스 서비스의 IP 주소(EXTERNAL-IP)를 확인한다.

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-warning webnots-notification-box">위에 사진에 나오는 prometheus-node-exporter 파드 4개를 지우기 위해서는 helm uninstall prometheus한 다음에 kubectl delete pods --all 해줘야 한다.</div>

<br>

```bash
kubectl get service prometheus-server
```

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-11-13-58-30.png){: p}

<br>

호스트 노트북(혹은 PC)의 웹 브라우저에 192.168.1.11을 입력해 프로메테우스의 웹 UI가 정상적으로 동작하는지 확인한다.

<br>

![](/images/Kubernetes/kubernetes-Prometheus/2021-08-11-13-59-25.png){: p}
