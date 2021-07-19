---
layout: post
title: 컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커-2.2.3
date: 2021-07-19 10:00:00 0000
tags: [Kubernetes, Ruby, Vagrantfile]
categories: [Vue]
description: Vagrantfile 내용 분석
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

# <center>가상 머신 추가로 구성하기</center>

<br>

> Vagranfile 55pg

<br>

이번에는 기존에 설치한 가상 머신 외에 가상 머신 3대를 추가로 설치해본다. 그리고 기존의 가상 머신과 추가한 가상 머신 간에 네트워크 통신이 원활하게 작동하는지 확인해 본다.

**Vagrantfile**

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
    cfg.vm.provision "shell", path: "install_pkg.sh"
    cfg.vm.provision "file", source: "ping_2_nds.sh", destination: "ping_2_nds.sh"
    cfg.vm.provision "shell", path: "config.sh"
  end

  #=============#
  # Added Nodes #
  #=============#

  (1..3).each do |i|
    config.vm.define "w#{i}-k8s" do |cfg|
      cfg.vm.box = "sysnet4admin/CentOS-k8s"
      cfg.vm.provider "virtualbox" do |vb|
        vb.name = "w#{i}-k8s(github_SysNet4Admin)"
        vb.cpus = 1
        vb.memory = 1024
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
      end
      cfg.vm.host_name = "w#{i}-k8s"
      cfg.vm.network "private_network", ip: "192.168.1.10#{i}"
      cfg.vm.network "forwarded_port", guest: 22, host: "6010#{i}",auto_correct: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "install_pkg.sh"
    end
  end
end
```

<br>

한줄한줄 씩 알아가보자.

**Vagrantfile**

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
    #SSH에 보여질 호스트 이름이다.
    cfg.vm.host_name = "m-k8s"

    #호스트 전용 네트워크를 private_network로 설정해 eth1 인터페이스를
    #호스트 전용(Host-Only)으로 구성하고 IP는 192.168.1.10으로 지정한다. 고정 IP를 설정해주는 방법이다.
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

    #vm.provision "shell" 구문으로 경로(path)에 있는 install_pkg.sh과 config.sh를
    #게스트(CentOS) 내부에서 호출해 실행되도록 한다.
    cfg.vm.provision "shell", path: "install_pkg.sh"

    #파일을 게스트 운영 체제에 전달하기 위해 "shell"이 아닌 "file" 구문으로 변경한다.
    #이렇게 하면 호스트에 있는 ping_2_nds.sh 파일을
    #게스트의 홈 디렉터리(/home/vagrant)로 전달한다
    cfg.vm.provision "file", source: "ping_2_nds.sh", destination: "ping_2_nds.sh"
    cfg.vm.provision "shell", path: "config.sh"
  end

  #=============#
  # Added Nodes #
  #=============#

   #for 문을 돌리는데 여기서 i는 1부터 3까지 대입되며 반복된다.
   #즉 3번 구문을 반복하여 Worker Node를 3개를 만드는 것이다.
  (1..3).each do |i|

    # #{i} 구문으로 i의 값을 가져온다 그래서 w1-k8s, w2-k8s, w3-k8s로 가상머신을 정의한다.
    #버추얼박스에서 보이는 가상 머신을 정의하는 것이다.
    config.vm.define "w#{i}-k8s" do |cfg|

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
      #생략
        vb.name = "w#{i}-k8s(github_SysNet4Admin)"
        vb.cpus = 1
        vb.memory = 1024
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
      end

       #여기서는 가상 머신 자체에 대한 설정이다.
       #do |cfg|에 속한 작업이다. 즉 호스트의 이름(w#{i}-k8s)을 설정한다.
      cfg.vm.host_name = "w#{i}-k8s"

      #생략
      cfg.vm.network "private_network", ip: "192.168.1.10#{i}"
      cfg.vm.network "forwarded_port", guest: 22, host: "6010#{i}",auto_correct: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "install_pkg.sh"
    end
  end
end
```

<br>

**install_pkg.sh**

```bash
#!/usr/bin/env bash
# install packages

#EPEL(Extra Packages for Enterprise Linux) 저장소 설치
yum install epel-release -y

#코드 하이라이트를 위한 Vim의 추가 기능을 설치
yum install vim-enhanced -y
```

<br>

EPEL은 리눅스의 추가 패키지이다. 리눅스에서 yum으로 패키지들을 설치하는데 패키지들이 그리 많지가 않다. 그래서 설치가 안 되는 패키지들을 설치하게 도와주는 것이 EPEL이다.

`repolist` 명령어를 사용해서 epel 설치전과 후의 패키지 수 차이를 확인해볼 수 있다.

<br>

**pin_2_nds.sh**

```bash
# ping 3 times per nodes
ping 192.168.1.101 -c 3
ping 192.168.1.102 -c 3
ping 192.168.1.103 -c 3
```

<br>

**config.sh**

```bash
#!/usr/bin/env bash
# modify permission

# -rwxr--r--는 744,
# 소유자 권한: 읽기, 쓰기, 실행 부여
# 소유그룹권한: 읽기 부여
# 나머지권한: 읽기 부여
chmod 744 ./ping_2_nds.sh
```

<br>
