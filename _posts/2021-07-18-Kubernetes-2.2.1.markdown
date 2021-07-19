---
layout: post
title: 컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커-2.2.1
date: 2021-07-18 10:00:00 0000
tags: [Kubernetes, Ruby, Vagrantfile]
categories: [Vue]
description: Vagrantfile 내용 분석
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

# <center>가상 머신에 필요한 설정 자동으로 구성하기</center>

<br>

> Vagranfile 48pg

<br>

- 알아야 할 내용

  - Vagrant Box: 설정에서 가장 기본적인 단위이다. 독립적인 운영체제 환경의 이미지다.
  - Ruby 문법 **do**: Paired with end, 코드 블럭을 구분할 수 있다.
  - VirtualBox에서 호스트는 개인 PC Window, 게스트 os는 CentOS 리눅스이다.

<br>

일단 원래 코드를 깔끔하게 보고 설명은 다시 이 코드 아래에 주석으로 적겠다.

```bash
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "m-k8s" do |cfg|
    cfg.vm.box = "sysnet4admin/CentOS-k8s"
    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "m-k8s(github_SysNet4Admin)"
      vb.cpus = 2
      vb.memory = 2048
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end
    cfg.vm.host_name = "m-k8s"
    cfg.vm.network "private_network", ip: "192.168.1.10"
    cfg.vm.network "forwarded_port", guest: 22, host: 60010, auto_correct: true, id: "ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
  end
end
```

<br>

```bash
#아래 두줄의 주석은 에디터에 현재 파일이 루비임을 인식하게 하는 호환 코드이다.
#ft는 file type(파일종류)의 약자이다.
# -*- mode: ruby -*-
# vi: set ft=ruby :

#"2"는 configuration object |config|의 버전을 명시하는 것이다.
#이것은 configuration 블록으로 사용된다.
Vagrant.configure("2") do |config|

#https://www.vagrantup.com/docs/vagrantfile/machine_settings 참고
#config.vm.define: 버추얼박스에서 보이는 가상 머신을 "m-k8s"로 정의한다.
#do |cfg|를 추가해 원하는 설정으로 변경한다.
  config.vm.define "m-k8s" do |cfg|

  #config.vm.box: 어떤 box에 대해 machine이 표시되는지 구성한다. 여기에 값은
  #HashiCorp's Vagrant Clout에 설치된 박스나 약칭으로된 이름이 들어가야 한다.
  #즉 사람들이 만들어 놓은 운영체제 이미지의 이름이 들어간다.
  #42pg를 보면 필자가 만들어 놓은 운영체제 이미지를 사용한다.
  #필자가 만든 운영체제 이미지의 이름이 "sysnet4admin/CentOS-k8s"이다.
  #https://app.vagranup.com/sysnet4admin/boxes/CentOS-k8s에서 확인할 수 있다.
    cfg.vm.box = "sysnet4admin/CentOS-k8s"

  #베이그런트의 프로바이더(provider)가 버추얼박스라는 것을 정의한다. 프로바이더는
  #베이그런트를 통해 제공되는 코드가 실제로 가상 머신으로 배포되게 하는 소프트웨어이다.
  #버추얼박스가 여기에 해당한다. 다음으로 버추얼박스에 필요한 설정을 정의하는데
  #그 시작을 do |vb|로 선언한다. provider가 존재하지 않을 경우 Vagrant는 이 설정 블록을
  #무시한다.
    cfg.vm.provider "virtualbox" do |vb|

    #VirtualBox provider는 더 VirtualBox 기반 Vagrant 환경을 보다 세밀하게 제어할 수 있는
    #몇 가지 추가 구성 옵션을 제공한다.
    #https://www.vagrantup.com/docs/providers/virtualbox/configuration 참고

    #버추얼박스에 생성한 가상 머신의 이름, CPU 수, 메모리 크기, 소속된 그룹을 명시한다.
    #그리고 마지막으로 end를 적어 버추얼박스 설정이 끝났음을 알린다.

    #VirtualBox GUI에 표시될 이름을 설정한다
      vb.name = "m-k8s(github_SysNet4Admin)"
    #사용할 CPU 수 설정
      vb.cpus = 2
    #사용할 메모리 크기 설정
      vb.memory = 2048

    # :id는 생성되는 가상 머신의 ID를 반환하는 특별한 매개변수이다.
    #그래서 VBoxManage 커맨드가 ID를 요구할 때 이 특별한 매개변수를 사용한다.
    #--groups를 이용해서 명시된 그룹으로 분리하는 것이다.
    # 여러개의 vms가 있으면 헷갈릴 수 있으므로 분류한다.
    #modifyvm은 ID에 해당하는 vm의 설정을 한다.
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end

    #여기서는 가상 머신 자체에 대한 설정이다.
    #do |cfg|에 속한 작업이다. 즉 호스트의 이름(m-k8s)을 설정한다.
    cfg.vm.host_name = "m-k8s"

    #호스트 전용 네트워크를 private_network로 설정해 eth1 인터페이스를
    #호스트 전용(Host-Only)으로 구성하고 IP는 192.168.1.10으로 지정한다. 고정 IP를 설정해주는 방법이다. 아래 document 참고
    cfg.vm.network "private_network", ip: "192.168.1.10"

    #ssh 통신은 호스트 60010번을 게스트 22번으로 전달되도록 구성한다.
    #이때 혹시 모를 포트 중복을 대비해 auto_correct: true로 설정해서
    #포트가 중복되면 포트가 자동으로 변경되도록 한다.
    cfg.vm.network "forwarded_port", guest: 22, host: 60010, auto_correct: true, id: "ssh"

    #호스트(PC 또는 노트북)와 게스트(가상 머신) 사이에
    #디렉터리 동기화가 이뤄지지 않게 설정(disabled: true)한다.
    #첫 번째 파라미터는 host의 경로이다 두 번째 파라미터는 guest(vm)의 경로이다.
    #가상머신에 들어가보면 /vagrant 경로에 Vagrantfile이 있다
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
  end
end
```

<br>

**cfg.vm.network "private_network", ip: "192.168.1.10"**에 대해서 좀 더 알아보자.

공식 document에 들어가면 그 내용이 있는데 발번역을 해보려 한다. 링크는 아래에 남긴다.

<br>

**[Vagrant](https://www.vagrantup.com/docs/networking/private_network)**

<br>

---

![](/images/Kubernetes/post1/2021-07-19-09-05-59.png)

<br>

**네트워크 식별자: private_network**

<br>

Vagrant private network(사설 네트워크)는 글로벌 인터넷에서 공개적으로 접근 불가한 IP으로 게스트 머신(가상 머신)에 접근하는 것을 가능하게 한다. 일반적으로 이것은 당신의 머신이 **사설 주소 공간**으로부터 주소를 얻는 다는 것을 의미한다.

<br>

동일한 사설 네트워크 안에 여러 대의 머신은 동일한 공급자가 지원한다는 제한이 있지만 사설 네트워크 안에서 통신이 가능하다.

<br>

![](/images/Kubernetes/post1/2021-07-19-09-13-30.png)

<br>

**DHCP**

<br>

사설 네트워크를 사용하기 위한 가장 쉬운 방법은 DHCP를 통해서 IP를 할당 받는 것이다.

<br>

이렇게 하면 예약된 주소 공간에서 IP 주소가 자동으로 할당됩니다. IP 주소는 SSH에서 `vagrant ssh` 명령을 입력하고 `ifconfig`와 같은 적절한 명령줄 도구를 사용해서 IP를 찾을 수 있습니다.

<br>

![](/images/Kubernetes/post1/2021-07-19-09-17-55.png)

<br>

**고정 IP**

<br>

그리고 당신은 머신에게 고정 IP 주소를 기입할 수 있습니다. 이를 통해 알려진 고정 IP를 사용하여 Vagrant 관리 시스템에 액세스할 수 있습니다. Vagrantfile에서 고정 IP 주소를 설정하는 방법은 아래와 같습니다.

<br>

![](/images/Kubernetes/post1/2021-07-19-09-22-14.png)

<br>

동일한 네트워크에 다른 머신의 IP와 충돌하지 않도록 IP를 할당하는 것은 사용자에게 달렸습니다.

<br>

원하는 IP를 선택할 수 있지만 **[reserved private address space](https://en.wikipedia.org/wiki/Private_network#Private_IPv4_address_spaces)** 에 나와있는 IP 주소를 사용하는 게 좋습니다. 이 IP들은 절대로 공개적으로 라우팅 되지 않는 것을 보장하며 대부분의 라우터들이 실제로 외부 트래픽이 이 IP로 들어가는 것을 막는다.

<br>

일부 운영 체제의 경우 기본 게이트웨이 또는 MTU 설정과 같은 고정 IP 주소에 대한 추가 구성 옵션을 사용할 수 있습니다.

<br>

**경고!** 시스템의 다른 IP 공간과 겹치는 IP를 선택하지 마십시오. 이로 인해 네트워크에 연결할 수 없습니다.

---

<br>

**[호스트 네트워크 및 NAT에 대한 블로그 1](https://developerin.tistory.com/18)**

**[호스트 네트워크 및 NAT에 대한 블로그 2](https://liveyourit.tistory.com/26)**
