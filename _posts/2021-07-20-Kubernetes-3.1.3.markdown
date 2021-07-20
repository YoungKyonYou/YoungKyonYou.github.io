---
layout: post
title: 컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커-3.1.3
date: 2021-07-20 09:00:00 0000
tags: [Kubernetes, Ruby, Vagrantfile]
categories: [Kubernetes]
description: 쿠버네티스 구성하기
---

<br><br>

**_해당 내용은 책 <컨테이너 인프라 환경 구축을 위한 쿠버네티스/도커>에 나오는 내용이며 이는 개인적으로 공부하기 위해서 게시하는 글임을 알립니다._**

# <center>쿠버네티스 구성하기</center>

<br>

> Vagranfile 87pg

<br>

**Vagrantfile**

```bash
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  N = 3 # max number of worker nodes
  Ver = '1.18.4' # Kubernetes Version to install

  #=============#
  # Master Node #
  #=============#

    config.vm.define "m-k8s" do |cfg|
      cfg.vm.box = "sysnet4admin/CentOS-k8s"
      cfg.vm.provider "virtualbox" do |vb|
        vb.name = "m-k8s(github_SysNet4Admin)"
        vb.cpus = 2
        vb.memory = 3072
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SgMST-1.13.1(github_SysNet4Admin)"]
      end
      cfg.vm.host_name = "m-k8s"
      cfg.vm.network "private_network", ip: "192.168.1.10"
      cfg.vm.network "forwarded_port", guest: 22, host: 60010, auto_correct: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "config.sh", args: N
      cfg.vm.provision "shell", path: "install_pkg.sh", args: [ Ver, "Main" ]
      cfg.vm.provision "shell", path: "master_node.sh"
    end

  #==============#
  # Worker Nodes #
  #==============#

  (1..N).each do |i|
    config.vm.define "w#{i}-k8s" do |cfg|
      cfg.vm.box = "sysnet4admin/CentOS-k8s"
      cfg.vm.provider "virtualbox" do |vb|
        vb.name = "w#{i}-k8s(github_SysNet4Admin)"
        vb.cpus = 1
        vb.memory = 2560
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SgMST-1.13.1(github_SysNet4Admin)"]
      end
      cfg.vm.host_name = "w#{i}-k8s"
      cfg.vm.network "private_network", ip: "192.168.1.10#{i}"
      cfg.vm.network "forwarded_port", guest: 22, host: "6010#{i}", auto_correct: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "config.sh", args: N
      cfg.vm.provision "shell", path: "install_pkg.sh", args: Ver
      cfg.vm.provision "shell", path: "work_nodes.sh"
    end
  end

end
```

<br>

이제 한 줄 한 줄씩 알아가보자

<br>

**Vagrantfile**

```bash
#아래 두줄의 주석은 에디터에 현재 파일이 루비임을 인식하게 하는 호환 코드이다.
#ft는 file type(파일종류)의 약자이다.
# -*- mode: ruby -*-
# vi: set ft=ruby :

#"2"는 configuration object |config|의 버전을 명시하는 것이다.
#이것은 configuration 블록으로 사용된다.
Vagrant.configure("2") do |config|

  #생성할 뭐커노드 개수 정의
  N = 3 # max number of worker nodes
  #다운받을 쿠버네티스 버젼 정의
  Ver = '1.18.4' # Kubernetes Version to install

  #=============#
  # Master Node #
  #=============#


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
      #그 시작을 do |vb|로 선언한다. provider가 존재하지 않을 경우 Vagrant는  이 설정 블록을
      #무시한다.
      cfg.vm.provider "virtualbox" do |vb|

      #VirtualBox provider는 더 VirtualBox 기반 Vagrant 환경을 보다 세밀하게 제어할 수 있는
      #몇 가지 추가 구성 옵션을 제공한다.
      #https://www.vagrantup.com/docs/providers/virtualbox/configuration 참고

      #버추얼박스에 생성한 가상 머신의 이름, CPU 수, 메모리 크기, 소속된 그룹을 명시한다.
      #그리고 마지막으로 end를 적어 버추얼박스 설정이 끝났음을 알린다.

      #VirtualBox GUI에 표시될 이름을 설정한다
        vb.name = "m-k8s(github_SysNet4Admin)"
        vb.cpus = 2
        vb.memory = 3072

       # :id는 생성되는 가상 머신의 ID를 반환하는 특별한 매개변수이다.
       #그래서 VBoxManage 커맨드가 ID를 요구할 때 이 특별한 매개변수를 사용한다.
       #--groups를 이용해서 명시된 그룹으로 분리하는 것이다.
       # 여러개의 vms가 있으면 헷갈릴 수 있으므로 분류한다.
       #modifyvm은 ID에 해당하는 vm의 설정을 한다.
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SgMST-1.13.1(github_SysNet4Admin)"]
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


      #vm.provision "shell" 구문으로 경로(path)에 있는 install_pkg.sh와 config.sh를
      #게스트(CentOS) 내부에서 호출해 실행되도록 한다.
      #변수 (N=3)를 args: N으로 받는다. 이는 사용자가 워커 노드의 개수를 직접 조절할 수 있게 한다.
      cfg.vm.provision "shell", path: "config.sh", args: N

      #args: [Ver, "Main"] 코드를 추가해 쿠버네티스 버전 정보(Ver)와 Main이라
      #는 문자를 install_pkg.sh로 넘긴다. Ver 변수는 각 노드에 해당 버전의 쿠버네티스 버전을
      #설치하게 한다. 두 번째 인자인 Main 문자는 install_pkg.sh에서 조건문으로 처리해 마스터
      #노드에만 이 책의 전체 실행 코드를 내려받게 한다.
      cfg.vm.provision "shell", path: "install_pkg.sh", args: [ Ver, "Main" ]

      #쿠버네티스 마스터 노드를 위한 master_node.sh
      cfg.vm.provision "shell", path: "master_node.sh"
    end

  #==============#
  # Worker Nodes #
  #==============#

   #for 문을 돌리는데 여기서 i는 1부터 3까지 대입되며 반복된다.
   #즉 N=3임으로 3번 구문을 반복하여 Worker Node를 3개를 만드는 것이다.
  (1..N).each do |i|

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

        vb.name = "w#{i}-k8s(github_SysNet4Admin)"
        vb.cpus = 1
        vb.memory = 2560
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SgMST-1.13.1(github_SysNet4Admin)"]
      end

      #여기서는 가상 머신 자체에 대한 설정이다.
       #do |cfg|에 속한 작업이다. 즉 호스트의 이름(w#{i}-k8s)을 설정한다.
       #superputty의 ssh에서 나타날 호스트 이름이다.
      cfg.vm.host_name = "w#{i}-k8s"

      #생략
      cfg.vm.network "private_network", ip: "192.168.1.10#{i}"
      cfg.vm.network "forwarded_port", guest: 22, host: "6010#{i}", auto_correct: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "config.sh", args: N
      cfg.vm.provision "shell", path: "install_pkg.sh", args: Ver

      #쿠버네티스 워커 노드를 위한 work_nodes.sh이다.
      cfg.vm.provision "shell", path: "work_nodes.sh"
    end
  end

end
```

<br>

config.sh는 kubeadm으로 쿠버네티스를 설치하기 위한 사전 조건을 설정하는 스크립트 파일이다. 쿠버네티스의 노드가 되는 가상 머신에 어떤 값을 설정하는지 알아본다.

<br>

**config.sh**

```bash
#!/usr/bin/env bash

# vim configuration
echo 'alias vi=vim' >> /etc/profile

# swapoff -a to disable swapping
swapoff -a
# sed to comment the swap partition in /etc/fstab
sed -i.bak -r 's/(.+ swap .+)/#\1/' /etc/fstab

# kubernetes repo
gg_pkg="packages.cloud.google.com/yum/doc" # Due to shorten addr for key
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://${gg_pkg}/yum-key.gpg https://${gg_pkg}/rpm-package-key.gpg
EOF

# Set SELinux in permissive mode (effectively disabling it)
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

# RHEL/CentOS 7 have reported traffic issues being routed incorrectly due to iptables bypassed
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
modprobe br_netfilter

# local small dns & vagrant cannot parse and delivery shell code.
echo "192.168.1.10 m-k8s" >> /etc/hosts
for (( i=1; i<=$1; i++  )); do echo "192.168.1.10$i w$i-k8s" >> /etc/hosts; done

# config DNS
cat <<EOF > /etc/resolv.conf
nameserver 1.1.1.1 #cloudflare DNS
nameserver 8.8.8.8 #Google DNS
EOF


```

<br>

한 줄 한 줄 살펴보자.

<br>

**config.sh**

```bash
#!/usr/bin/env bash

#vim configuration
#vi를 호출하면 vim을 호출하도록 프로파일에 입력한다
#이렇게 하면 코드에 하이라이트를 넣어 코드를 쉽게 구분할 수 있다.
#리눅스 alias 설정 'alias 별명='명령어 정의'' 를 /etc/profile에 정의하면 된다.
echo 'alias vi=vim' >> /etc/profile

# swapoff -a는 스왑을 중지시키라는 명령어이다.
# 스왑을 내렸다 다시 시작해 스왑 메모리를 반환 하는데 사용한다.
#swap은 시스템에 메모리가 부족할 경우에 하드 디스크의 일부 공간을 활용하여
#계속 작업을 도와주는 영역이다. 리눅스에서는 RAM 공간이 부족하면 하드디스크의
#일부 공간을 사용하게 되는데 권장되지 않는다.(하드디스크는 접근 속도가 느리다)
# swapoff -a to disable swapping
swapoff -a

#시스템이 다시 시작되더라도 스왑되지 않도록 설정한다.
# sed to comment the swap partition in /etc/fstab
#sed는 vi 편집기랑 마찬가지로 편집에 특화된 명령어이다. 수정, 치환, 삭제, 글추가 등 편집기 기능은
#웬만해서 다 된다. vi는 편집기를 열어서 커서로 라인을 옮기고 글을 삭제하고 쓰고 하는 등 워드 파일을
#수정하는 것과 같다면 sed는 명령행에서 파일을 인자로 받아 명령어를 통해 작업한 후 결과를
#화면으로 확인하는 방식이다. 특징은 sed 편집기는 원본을 손상시키지 않고 수정한 후 결과를 보여준다
#그래서 원본을 수정하려면 -i 옵션이 필요한 것이다.
#.bak 확장자는 컴퓨터로 작업중에 생길 수 있는 전원 차단과 같은 갑자기 컴퓨터가 꺼질 경우를 대비해
#자동으로 만들어지는 백업 파일이다. 여기서 sed -i.bak은 원본 수정 후 .bak 확장자로 파일을 생성하여 백업
#하라는 것이다. 즉 /etc 아래 fstab.bak 파일이 하나 생긴다
#/etc/fstab은 파일 시스템 정보를 저장하고 있으며 리눅스 부팅시 마운트 정보를 저장하고 있다.
#이 파일안에 있는 구성값들로 인해 부팅시에 자동으로 적용될 수 있도록 한다.
#s/문자1/문자2/ [파일]은 파일 안에 있는 문자1을 2로 바꾸라는 옵션이다.
#여기선 /etc/fstab이라는 파일을 열어서 수정한다는 것이다.
#그리고 아래를 보면 .+ 라고 되어 있는 부분은 정규식 표현이다 즉 .은 임의의 한 문자를 의미하고
#+은 바로 앞의 문자가 1회 이상 반복된다는 뜻이다.
#즉 swap 이 중간에 있고 그 앞과 뒤에 반복적으로 임의의 문자가 여러 개있는 다시 말해 그 라인을 선택한다.
#/etc/fstab에 들어가보면
#/dev/mapper/centos_k8s-swap swap                    swap    defaults        0 0
# 이것 라인 전체를 선택하고 이것은 \1로 역참조하고 주석(#) 앞에 다가 이 라인을 넣으라는 것
#다시 말해 주석을 처리하는 것이다.


#시스템이 다시 시작되더라도 스왑되지 않도록 설정하려면
#/etc/fstab 파일을 열여서 swap 인트리에 주석'#'을 달아야한다.
sed -i.bak -r 's/(.+ swap .+)/#\1/' /etc/fstab

# kubernetes repo
#쿠버네티스의 리포지터리를 설정하기 위한 경로가 너무 길어지지 않게 경로를 변수로 처리하는 것이다.
gg_pkg="packages.cloud.google.com/yum/doc" # Due to shorten addr for key

#cat를 사용해서 여러 줄을 입력하기 위한 방법으로 cat <<EOF를 사용한다. 그리고 다썼으면 마지막에
#EOF로 저장하고 종료한다.
#그래서 cat으로 여러 줄을 입력하되 입력 내용을 /etc/yum.repos.d 아래 kubernetes.repo 파일에 저장한다
#/etc/yum.repos은 Package를 모아놓은 저장소이다. Yum을 통해 Package 설치 시 활성화 된
#Yum Repository에서 Package를 다운로드하여 설치하기 때문에
#Package가 Repository에 없을 경우 설치 할 수 없다.
#그래서 여기 안에는 우리가 이전에 설치했던 epel도 들어가 있다.
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://${gg_pkg}/yum-key.gpg https://${gg_pkg}/rpm-package-key.gpg
EOF

#selinux가 제한적으로 사용되지 않도록 permissive 모드로 변경한다.
#SELinux(Security-Enhanced Linux)는 관리자가 시스템 액세스 권한을 효과적으로
#제어할 수 있게 하는 Linux® 시스템용 보안 아키텍처이다.
#SELinux는 enforce, permissive, disable 세 가지 동작 모드가 있으며
#설치하면 기본적으로 enforce 모드로 동작합니다.
#enforce 모드일 경우 SELinux의 정책과 룰에 어긋나는 동작은 모두 차단되며
#permissive 모드이 경우 정책에 어긋나는 동작은 감사 로그를 남기고 허용한다.
#setenforce 0 명령이 permissive로 바꾸는 명령이다.
#그리고 /etc/selinux/config 파일에서 SELINUX로 시작되고 enforcing$으로 끝나는 부분을
#SELINUX=permissive으로 바꿔주고 있다. (옵션 s를 통해서)
#-i 옵션은 sed에서 원본을 바꾸는 옵션이다.
# Set SELinux in permissive mode (effectively disabling it)
#부팅 할때 SELinux 모드를 결정하는 설정 파일은 /etc/selinux/config 에 존재한다.
#부팅 할때 SELinux 모드를 변경하려면 /etc/selinux/config 에서
#SELINUX=enforcing 부분을 permissive 로 변경하면 된다
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

#브리지 네트워크를 통과하는 IPv4와 IPv6의 패킷을 iptables가 관리하게 설정한다
#파드의 통신을 iptables로 제어한다. 필요에 따라 IPVS 같은 방식으로도 구성할 수 있다.
# RHEL/CentOS 7 have reported traffic issues being routed incorrectly due to iptables bypassed
#iptables는 리눅스상에서 방화벽을 설정하는 도구로서 커널 2.4 이전 버전에서 사용되던
# ipchains를 대신하는 방화벽 도구이다.
#iptables란 넷필터 프로젝트에서 개발했으며 광범위한 프로토콜 상태 추적,
#패킷 애플리케이션 계층검사, 속도 제한, 필터링 정책을 명시하기 위한 강력한 매커니즘을 제공한다.
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

#br_netfilter 커널 모듈을 사용해 브리지로 네트워크를 구성한다. 이때 IP 마스커레이드(Masquerade)를
#사용해 내부 네트워크와 외부 네트워크를 분리한다.
#IP 마스커레이드는 쉽게 설명하면 커널에서 제공하는 NAT 기능으로 이해하면 된다.
#실제로는 br_netfilter를 적용함으로써 28~31번째 줄에서 적용한 iptables가 활성화된다.
#쿠버네티스 설치 시 br_netfilter 모듈이 필요하다
#이 커널 모듈을 사용하면 브릿지를 통과하는 패킷이 필터링 및 포트 전달을 위해
#iptables에 의해 처리되고 클러스터의 쿠버네티스 Pod는 서로 통신 가능.
modprobe br_netfilter

# local small dns & vagrant cannot parse and delivery shell code.
#쿠버네티스 안에서 노드 간 통신을 이름으로 할 수 있도록 각 노드의
#호스트 이름과 IP를 /etc/hosts에 설정한다. 이때 워커 노드는
#Vagrantfile에서 넘겨받은 N 변수로 전달된 노드 수에 맞게 동적으로 생성한다.
#echo는 문자열을 출력하는데 이것을 /etc 폴더 아래 hosts 파일에 저장하게 된다.
#즉 그 파일에는 원래 내용에다가

#192.168.1.10 m-k8s
#192.168.1.101 w1-k8s
#192.168.1.102 w2-k8s
#192.168.1.103 w3-k8s

#가 추가된다.
echo "192.168.1.10 m-k8s" >> /etc/hosts
for (( i=1; i<=$1; i++  )); do echo "192.168.1.10$i w$i-k8s" >> /etc/hosts; done

# config DNS
#외부와 통신할 수 있게 DNS 서버를 지정한다.
#DNS 서버는 꼭 해당 통신사의 DNS 서버를 이용하지 않아도
#된다. 단지 PC가 "자동으로 DNS 서버 주소 받기"로
#설정되어 있으면 자동으로 그 해당 통신사의
#DNS 서버 주소를 이용하게 된다.
#하지만 아래와 같이 DNS 서버를 수동으로 변경하는 과정을 거치게 되면
#다른 DNS 서버를 이용할 수도 있다
#아래는 cloudfare와 google의 퍼블릭 DNS를 사용하는 것이다.
cat <<EOF > /etc/resolv.conf
nameserver 1.1.1.1 #cloudflare DNS
nameserver 8.8.8.8 #Google DNS
EOF
```

<br>

**install_pkg.sh**

```bash
#!/usr/bin/env bash

# install packages
yum install epel-release -y
yum install vim-enhanced -y
yum install git -y

# install docker
yum install docker -y && systemctl enable --now docker

# install kubernetes cluster
yum install kubectl-$1 kubelet-$1 kubeadm-$1 -y
systemctl enable --now kubelet

# git clone _Book_k8sInfra.git
if [ $2 = 'Main' ]; then
  git clone https://github.com/sysnet4admin/_Book_k8sInfra.git
  mv /home/vagrant/_Book_k8sInfra $HOME
  find $HOME/_Book_k8sInfra/ -regex ".*\.\(sh\)" -exec chmod 700 {} \;
fi

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

#깃허브에서 코드를 내려받을 수 있게 깃을 설치한다.
yum install git -y

# install docker
#쿠버네티스를 관리하는 컨테이너를 설치하기 위해 도커를 설치하고 구동한다.
#systemctl enable 서비스명은 서비스를 활성화시키라는 것이다.
#즉 시스템이 재부팅하면 자동으로 서비스를 실행하도록 등록한다.
yum install docker -y && systemctl enable --now docker

# install kubernetes cluster
#쿠버네티스를 구성하기 위해 첫 번째 변수($1=Ver='1.18.4')로 넘겨받은
#1.18.4 버전의 kubectl, kubelet, kubeadm을 설치하고 kubelet을 시작한다.
#$1는 Vagrantfile에서 arg으로 넘겨주는 인자이다.
yum install kubectl-$1 kubelet-$1 kubeadm-$1 -y
systemctl enable --now kubelet

# git clone _Book_k8sInfra.git
#이 책의 전체 실행 코드를 마스터 노드에만 내려받도록 Vagrantfile에서
#두 번째 변수($2='Main')를 넘겨받는다. 그리고 깃에서 코드를 내려받아 실습을 진행할
#루트 홈디렉터리(/root)로 옮긴다. 배시 스크립트(.sh)를 find로 찾아서 바로 실행 가능한 상태가 되도록
#chmod 700으로 설정한다.
if [ $2 = 'Main' ]; then

#clone해서 코드를 내려받는다.
  git clone https://github.com/sysnet4admin/_Book_k8sInfra.git

  #/home/vagrant에 있는 _Book_k8sInfra 폴더를 HOME(/root)으로 옮긴다.
  mv /home/vagrant/_Book_k8sInfra $HOME

  #/root에 있는 _Book_k8sInfra 폴더 안에
  #-exec는 검색된 파일에 대해 지정된 명령을 실행한다. 즉 여기서는 chmod 700를 한다.
  #_Book_k8sInfra 폴더 안에서 .sh 파일을 찾는 것이다. (그 폴더 안에 또 다른 폴더 안에 있을 수 있음)
  #정규식 표현을 보면 *:0개 이상을 의미하고 \:는 어떤 특수한 문자 앞에 쓰면
  #그 특수한 문자로 보는 게 아니라 그냥 단순한 문자로 본다.
  #즉 여기서 .*는 임의의 문자가 0개 이상 나타나고 \( 는 ( 이 문자를 나타내고
  #.\는 .sh에서 .를 나타낸다.
  #(sh)의 ()는 문자열에서 같은 순서로 포함된 문자와 일치함을 의미한다.기타 표현식을
  #그룹화하는 데 사용한다. \)은 )를 문자 자체를 표현한다. 마지막의 \; 는
  #세미콜론을 사용하기 위한 이스케이프 문자이다 {}문자는
  #find의 결과로 대체된다 즉 .sh의 풀이름으로 대체된다. 그래서
  #결론적으로 -exec chmod 700 test.sh; 로 실행되는 것이다.

  find $HOME/_Book_k8sInfra/ -regex ".*\.\(sh\)" -exec chmod 700 {} \;
fi

```

<br>

**master_node.sh**

```bash
#!/usr/bin/env bash

# init kubernetes
kubeadm init --token 123456.1234567890123456 --token-ttl 0 \
--pod-network-cidr=172.16.0.0/16 --apiserver-advertise-address=192.168.1.10

# config for master node only
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config

# config for kubernetes's network
kubectl apply -f \
https://raw.githubusercontent.com/sysnet4admin/IaC/master/manifests/172.16_net_calico.yaml
```

<br>

**master_node.sh**

```bash
#!/usr/bin/env bash

# init kubernetes
#kubeadm을 통해 쿠버네티스의 워커 노드를 받아들일 준비를 한다.
#먼저 토큰을 123456.1234567890123456으로 지정하고 ttl(time to live, 유지되는 시간)을
#0으로 설정해서 기본값인 24시간 후에 토큰이 계속 유지되게 한다.
#그리고 워커 노드가 정해진 토큰으로 들어오게 한다. 쿠버네티스가
#자동으로 컨테이너에 부여하는 네트워크를 172.16.0.0/16(172.16.0.1~172.16.255.254)으로 제공하고
#워커 노드가 접속하는 API 서버의 IP를 192.168.1.10으로 지정해 워커 노드들이 자동으로 API 서버에
#연결되게 한다.
#--pod-network-cidr string에 대한 문서 내용
#Specify range of IP addresses for the pod network.
#If set, the control plane will automatically allocate CIDRs for every node.
#control plane=master node
#--apiserver-advertise-address에 대한 공식문서 내용은 아래와 같다
#The IP address the API Server will advertise it's listening on.
#If not set the default network interface will be used.
#CIDR에 대한 내용 https://kim-dragon.tistory.com/9
kubeadm init --token 123456.1234567890123456 --token-ttl 0 \
--pod-network-cidr=172.16.0.0/16 --apiserver-advertise-address=192.168.1.10


#마스터 노드에서 현재 사용자가 쿠버네티스를 정상적으로 구동할 수 있게 설정 파일을
#루트의 홈디렉터리(/root)에 복사하고 쿠버네티스를 이용할 사용자에게 권한을 준다.
# config for master node only
#/etc/kubernetes 폴더 안에 admin.conf 파일을 /root/.kube 폴더 아래 config 파일을 생성해서
#내용을 복사한다는 것이다.
#chown을 사용하여 파일의 소유자를 소유자가 지정한 사용자 ID 또는 프로파일로
#설정할 수 있다. 선택적으로 chown은 파일의 그룹을 그룹이 지정한 그룹ID 또는
#프로파일로 설정할 수도 있다.
# Owner와 group을 변경하려면 Owner:Group 여기에 넣으면 된다.
#즉 Owner를 id -u로 바꾸고 group를 id -g로 바꾼다.
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config

#컨테이너 네트워크 인터페이스(CNI)인 캘리코(Calico)의 설정을 적용해 쿠버네티스의
#네트워크를 구성한다.
# config for kubernetes's network
#kubectl apply를 사용해서 리소스를 생성하거나 업데이트 할 수 있다
kubectl apply -f \
https://raw.githubusercontent.com/sysnet4admin/IaC/master/manifests/172.16_net_calico.yaml
```

<br>

**work_nodes.sh**

```bash
#!/usr/bin/env bash

# config for work_nodes only
kubeadm join --token 123456.1234567890123456 \
             --discovery-token-unsafe-skip-ca-verification 192.168.1.10:6443
```

<br>

**work_nodes.sh**

```bash
#!/usr/bin/env bash

# config for work_nodes only
#kubeadm을 이용해 쿠버네티스 마스터 노드에 접속합니다. 이때 연결에 필요한 토큰은
#기존에 마스터 노드에서 생성한 123456.1234567890123456을 사용한다
#간단하게 구성하기 위해 --discovery-token-unsafe-skip-ca-verification으로
#인증을 무시하고, API 서버 주소인 192.168.1.10으로 기본 포트 번호인 6443번 포트에 접속하도록 설정한다.
#--discovery-token-unsafe-skip-ca-verification에 대한 문서 내용은 아래와 같다.
#This weakens the kubeadm security model since other nodes can potentially
#impersonate the Kubernetes Control Plane.
kubeadm join --token 123456.1234567890123456 \
             --discovery-token-unsafe-skip-ca-verification 192.168.1.10:6443
```
