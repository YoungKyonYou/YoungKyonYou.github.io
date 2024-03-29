---
layout: post
title: Grafana 대시보드 해석하기-컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커
date: 2021-08-17 10:00:00 0000
tags: [Kubernetes, grafana]
categories: [Kubernetes]
description: Grafana 대시보드
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

이번 포스팅에서는 <span style="color:orange; font-weight:bold">컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커</span> 책의 저자가 만든 <span style="color:orange; font-weight:bold">Kubernetes All-in-One Cluster Monitoring KR</span>을 하나하나 분석해 보려 한다. 나중에 내가 써야할 일이 있을 수도 있고 분석함으로써 나중에 내가 내것을 직접 만드는데 많은 도움이 될 것 같아서다.

**Kubernetes All-in-One Cluster Monitoring**

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-17-10-20-02.png){: p}

<br>

위 사진에서 나오는 대시보드를 차례대로 봐보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-17-10-25-52.png){: p}

<br>

위 대시보드와 관련한 기본정보는 아래 사진과 같다.

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-17-10-26-55.png){: p}

<br>

아마 메트릭 구성(PromQL)을 분석하는 것이 제일 어려울 듯 싶다. 하지만 천천히 하나하나 알아가 보자.

<br>

메트릭은 PromQL(Prometheus Query Language)으로 구성되어 있다.

<br>

```PromQL
avg(
avg_over_time((sum without ()(kube_pod_container_status_ready{namespace="kube-system",pod=~".*.dashboard.*|.*.dns.*|kube.*|.*.calico.*|.*.flannel.*|.*.etcd.*"})
/
count without ()(kube_pod_container_status_ready{namespace="kube-system",pod=~".*.dashboard.*|.*.dns.*|kube.*|.*.calico.*|.*.flannel.*|.*.etcd.*"}))[$duration:5m])
)
```

<br>

- <span style="color:#3D9970; font-weight:bold">avg()</span>: 평균값을 반환한다.<br><br>
- <span style="color:#3D9970; font-weight:bold">avg_over_time()</span>: 지정된 간격에 있는 모든 포인트의 평균 값을 반환한다. <br><br>
- <span style="color:#3D9970; font-weight:bold">sum</span>: 합계를 반환 <br><br>
- <span style="color:#3D9970; font-weight:bold">without</span>: by도 있는데 without과 group by와 같은 역할을 한다. without은 by의 반대 관계이다. 즉 without을 사용하면 해당 label은 제외하고 나머지로 group by를 한다.<br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

group by는 유형별로 갯수를 알고 싶을 때 컬럼에 데이터를 그룹화하게 해준다.<br><br>
예를 들어 process_count에 group이라는 라벨이 있다고 할 경우 아래와 같이 사용할 수 있다.<br><br> <span style="color:orange; font-weight:bold">sum (process_count_total) without (group)</span><br><br>
이런 식으로 사용할 수 있다. 여기서 주의해야 할 점은 by 또는 without 다음에 오는 label list는 괄호로 묶여야 하다는 점이다. 괄호로 묶지 않으면 정상적인 쿼리문이 아니게 된다. 추가로 vector expression이 길다면 by 또는 without 구문을 앞으로 가져올 수 있다. <br><br>
<span style="color:orange; font-weight:bold">sum by (group) (process_count_total)</span><br><br>
여기서는 이 형식을 사용했다.</div>

<br>

- <span style="color:#3D9970; font-weight:bold">kube_pod_container_status_ready</span>: 컨테이너의 준비 확인이 성공했는지 여부를 설명한다.(퍼센티지로 표시)<br><br>
- <span style="color:#3D9970; font-weight:bold">namespace="kube-system"</span>: 현재 내 클러스터 내에 네임스페이스 중 "kube-system"를 의미한다.<br><br>
  <link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
  <div style="background: #eee;
    box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

  superputty에서<br><span style="color:orange; font-weight:bold">kubectl get namespace</span><br>
  를 입력하면 "kube-system"이 있는 것을 볼 수 있다.</div>

    <br>

- <span style="color:#3D9970; font-weight:bold">=~</span>: 정규식 표현을 이용할 수 있는 operator이다.<br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

\*: 앞 문자가 0개 이상의 개수가 존재할 수 있다.<br><br>
.: 임의의 문자 [단 '`는 넣을 수 없다.]<br><br>
|: 패턴을 OR 연산을 수행할 때 사용한다.</div><br><br>
즉 여기서는 클러스터내 kube-system 네임스페이스에 있는 파드 중에 dashboard, dns, kube, calico, flannel, etcd라는 문자열이 들어가 있는 파드를 모두 선택하는 것이다.

<br>

- <span style="color:#3D9970; font-weight:bold">[$duration: 5m]</span>: $ 표시는 미리 등록한 변수를 사용하는 것이다. 대시보드의 setting에 들어가면 변수를 확인할 수 있다.<br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Range Vector: Range Vector는 쿼리 시점까지 Time duration에 대해 일치하는 모든 시계열을 가지고 있다. 간단하게 말하면 Instant Vector에 []라는 Range Vector Selector를 사용한 데이터라고 보면 된다. 여기서 [] 안이 5m으로 설정되어 있는데 이는 5분의 간격을 의미한다. 즉 앞에서 avg_over_time()를 사용했었는데 5분을 간격으로 평균을 집계해주는 함수이다.</div>

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

avg()와 avg_over_time()[]을 지우면 아래와 같은 사진이 나온다.</div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-10-17-05.png){: p}

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

해당 정규식 표현에 알맞는 파드들의 각 상태정보가 수집되고 이 각각의 파드의 5분 간격의 시계열 데이터의 평균을 avg_over_time() 함수로 집계하고 다시 그것을 avg() 평균을 구해서 표시한다.

주의할 것은 100%은 1을 의미한다는 것이다. 이게 무슨 말이냐면 아래 사진과 같이 0~1 값을 가지게 필드를 설정해 놨다는 것이다. 그래서 나누기를 하면 1/1=1이 나와서 100%가 된다.</div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-11-06-43.png){: p}

- <span style="color:#3D9970; font-weight:bold">/</span>: 산술 연산자에서 나누기를 의미<br><br>

---

다음 지표를 보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-11-17-50.png){: p}

<br>

다음은 쉽다 그냥 클러스터내에 존재하는 namespace의 개수를 가져온다.

<br>

```PromQL
 count(kube_namespace_created)
```

<br>

---

다음 지표는 클러스터 내에 존재하는 모든 pod의 수를 반환한다.

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-11-19-24.png){: p}

<br>

```PromQL
 count(count by (pod)(container_spec_memory_reservation_limit_bytes{pod!=""}))
```

<br>

- <span style="color:#3D9970; font-weight:bold">container_spec_memory_reservation_limit_bytes</span>: 컨테이너가 예약할 수 있는 메모리 한계를 표시한다.<br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

여기서 중요한 것은 container_spec_memory_reservation_limit_bytes가 아니다. 이것은 단지 모든 파드를 조회하기 위한 한 방법으로서만 사용된 것이다. 즉 여기선 파드들의 어떤 정보를 조회하기 위한 다른 함수를 써도 무방하다. 아래 사진에 나오는 다른 함수를 써도 상관이 없는 것이다 중요한 것은 그 함수의 내용을 알고 싶은 것이 아니라 파드들의 개수를 구하고 싶은 것이기 때문이다.</div>

<br>

- <span style="color:#3D9970; font-weight:bold">{pod!=""}</span>:파드의 이름이 빈 문자열이 아닌 것을 다 조회한다. 즉 모든 파드를 조회한다는 것이다.<br><br>
- <span style="color:#3D9970; font-weight:bold">count by (pod)()</span>: 파드는 여러 개의 컨테이너를 가질 수 있다. 그래서 (pod), 즉 파드로 group by 하고 그것을 카운팅하는 것이다. 아래 사진을 참고한다.<br><br>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-11-54-24.png){: p}

<br>
- <span style="color:#3D9970; font-weight:bold">count()</span>: 위의 사진에 나오는 모든 파드들의 수를 구한다. <br><br>

---

다음 지표는 아래와 같다.

PVC의 개수를 구하는 지표다.

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-18-11-57-36.png){: p}

<br>

```PromQL
count(kube_persistentvolumeclaim_info)
```

<br>

- <span style="color:#3D9970; font-weight:bold">kube_persistentvolumeclaim_info</span>: PV와 PVC의 매핑 정보를 반환하는데 여기서는 개수를 구하는 것임으로 count로 그 개수를 구한다. <br><br>

---

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-09-44-40.png){: p}

<br>

이 대시보드에 구성은 테이블로 되어 있다. 컬럼 구성은 <span style="color:orange; font-weight:bold">Transform에서 볼 수 있다.</span> 아래 사진을 참고하자.

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-00-24.png){: p}

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-09-45-51.png){: p}

<br>

뭔가 많은 것을 볼 수 있는데 하나 하나 봐 보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-09-46-30.png){: p}

<br>

```PromQL
kube_node_info
```

<br>

- <span style="color:#3D9970; font-weight:bold">kube_node_info</span>: 클러스터 노드에 대한 정보를 반환한다. <br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

이 대시보드에서 Pod CIDR, OS verison, Kernel version, K8s version, Docker version을 반환한다. 아래 사진의 Filter가 체크되어 있는 것과 연관이 있다.</div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-06-35.png){: p}

<br>

지금 Query가 A, B, D, E, F ,G, H 이렇게 있는데 B, D, E는 이 대시보드에서 표시되지 않는 내용이다. 프로메테우스로 값을 확인해보려고 돌려보니 값을 찾을 수가 없었다. 왜 추가한지는 잘 모르겠다. 그래서 나는 이 B, D, E 쿼리는 해석하지 않으려 한다. 바로 F를 보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-17-10.png){: p}

<br>

```PromQL
kube_node_role
```

<br>

- <span style="color:#3D9970; font-weight:bold">kube_node_role</span>: 클러스터 노드에 역할 정보를 반환한다. <br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

테이블 컬럼에서 role 중에 master인 노드의 정보를 알 수 있게 해준다.</div>

<br>

Query G를 보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-23-25.png){: p}

<br>

```PromQL
label_replace(up{job="kubernetes-nodes"}, "node", "$1", "instance", "(.+)")
```

<br>

- <span style="color:#3D9970; font-weight:bold">label_replace(v instant-vector, dst_label string, replacement string, src_label string, regex string)</span>: v안에 각 시계열에 대해 labe_replace는 레이블 src_label의 값에 대해 정규식 regex와 일치시킨다. 만약 일치한다면 시계열에서 리턴된 레이블 dst_label의 값은 입력의 원래 레이블들과 함께 확장이 된다. 정규식의 캡처 그룹은 $1, $2 등으로 참조할 수 있습니다. 정규식이 일치하지 않으면 시계열이 변경되지 않고 반환됩니다.<br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

공식 문서를 발번역한거라 솔직히 무슨 말인지 잘 모르겠다. 쉽게 생각해보면 up{job="kubernetes-nodes}를 프로메테우스에서 돌리면 여러 레이블과 값이 나온다. (아래 사진 참고) 거기서 instance 레이블과 해당하는 값이 있는데 그 instance의 값에서 정규식과 일치하는 부분을 추출하고 그 추출한 값을 node라는 새로운 레이블의 값으로 넣어주는 것이다. 즉 처음 up{job="kubernetes-nodes}을 했을 때 나왔던 레이블들과 값들에 새로운 레이블 node를 추가하고 값은 instance 레이블에서 정규식과 매칭되는 값을 추출해서 넣어주겠다는 것이다. $1과 $2는 정규식으로 캡쳐된 그룹을 명시한다는 것이다. </div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-57-38.png){: p}

<br>

label_replace()를 추가하고 나면 위 사진에서 <span style="color:orange; font-weight:bold">node</span> 레이블과 값이 추가된 것을 볼 수 있다.(아래 사진 참고)

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-10-58-20.png){: p}

<br>

- <span style="color:#3D9970; font-weight:bold">up</span>: up은 수집 대상이 작동하고 있는지 알려준다. 결과로 나온 메트릭 데이터를 보면 up이라는 메트릭 이름을 가지는 대상을 검색하고 그중에 job="kubernetes-nodes"라는 레이블 이름을 검색 조건에 추가한다. 이를 일반적으로 필터링이라고 하고 검색 조거네 맞는 메트릭 데이터가 존재하고 추출에 성공하면 1이라는 값으로 표현한다. 즉 여기서 1의 값을 가지니까 Node Status 값이 Good를 표시한다.<br><br>

<br>

다음 H Query를 보자.

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-11-03-39.png){: p}

<br>

```PromQL
label_replace(avg by (kubernetes_node) (time() - node_boot_time_seconds), "node", "$1", "kubernetes_node", "(.+)")
```

<br>

- <span style="color:#3D9970; font-weight:bold">time()</span>: 1970년 1월 1일 UTC 이후 경과된 시간(초)을 반환한다. 이것은 실제로 현재 시간을 반환하는 것이 아니라 표현식이 평가되는 시간을 반환한다는 점에 유의해야 한다.<br><br>
- <span style="color:#3D9970; font-weight:bold">node_boot_time_seconds</span>: 노드의 부팅 시간(리눅스타임) <br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

avg by()는 여기서 평균을 내고 싶은 것은 아니다. 단순히 time()-node_boot_time_seconds를 했을 때 아래 사진에서와 같이 여러 레이블과 값들이 나오는 것을 볼 수 있다. 여기서 레이블을 kubernetes_node로만 표시되게 하기 위해서 avg by를 사용한 것이라고 볼 수 있다. 즉 avg 자체는 의미가 없다 sum, count 등을 써도 무방한 것이다 단순히 group by 기능을 쓰기 위한 조치일 뿐이다.</div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-11-50-35.png){: p}

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-11-52-34.png){: p}

<br>

그리고 이 쿼리로 인해 대시보드의 Uptime이 표시되는 것을 볼 수 있다.

---

다음 대시보드다.

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-12-21-51.png){: p}

<br>

```PromQL
(sum by (instance,nodename) (irate(node_cpu_seconds_total{mode!~"guest.*|idle|iowait"}[$duration])) + on(instance) group_left(nodename)
node_uname_info) - 1
```

<br>

- <span style="color:#3D9970; font-weight:bold">node_cpu_seconds_total</span>: 노드의 총 CPU 사용 시간을 파악할 수 있다. <br><br>
- <span style="color:#3D9970; font-weight:bold">idle</span>: CPU가 할 일이 없는 시간 <br><br>
- <span style="color:#3D9970; font-weight:bold">guest</span>: vm를 돌리고 있다면 사용하고 있는 cpu를 의미 <br><br>
- <span style="color:#3D9970; font-weight:bold">rate(node_cpu_seconds_total{mode="system"}[1m])</span>: 지난 1분 동안 시스템 모드에서 사용한 평균 CPU 시간(초) <br><br>
- <span style="color:#3D9970; font-weight:bold">irate(v range-vector)</span>: 범위 벡터에서 시계열의 초당 순간 증가율을 계산한다. 이것은 마지막 두 데이터 포인트를 기반으로 한다. rate는 구간 시작 값과 구간 종료 값의 차이에 대한 변화율을 다루고 irate는 구간 종료 바로 전 값과 구간 종료 값의 차이에 대한 변화율을 나타낸다는 점이 다르다. 따라서 구간이 매우 길면 irate의 변화율은 큰 의미가 없기 때문에 rate 함수를 사용하는 것이 낫다.<br><br>
- <span style="color:#3D9970; font-weight:bold">!~</span>: 조건에 넣은 정규 표현식에 해당하지 않는 메트릭을 보여준다. 예를 들어 {instance!~ "w.+"}는 instance 레이블 값이 w로 시작하지 않는 모든 메트릭을 찾아 출력한다. <br><br>
<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

즉 여기서 node_cpu_seconds_total{mode!~"guest.\*|idle|iowait"}는 cpu의 모드가 guest, idle, iowait 문자열을 포함하는 mode를 제외한 노드의 각 mode의 CPU 사용 시간을 나타내라는 것이다. 아래 사진을 참고한다.</div>

<br>

![](/images/Kubernetes/Kubernetes-Grafana-all-in-one/2021-08-19-12-43-16.png){: p}

<br>

- <span style="color:#3D9970; font-weight:bold"></span>: 노드의 부팅 시간(리눅스타임) <br><br>

<br>
