---
layout: post
title: Mysql Workbench를 사용하는 Springboot를 Docker Image로 만들고 배포하기
date: 2021-07-30 9:00:00 0000
tags: [Kubernetes, Mysql-Workbench, SpringBoot, Docker, Docker Image]
categories: [Kubernetes]
description: Springboot 도커 이미지 만들고 배포하기
---

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

# <center>Docker Image 만들기</center>

<br>

이번 게시물에서는 JPA를 사용하는 SpringBoot 프로젝트를 도커 이미지로 만든 후에 배포하는 작업을 하려고 한다. 그전에 꼭 봐야하는 게시물이 있는데 링크는 아래 걸어놓겠다.

**[Kubernetes와 Mysql Workbench 연동하기](https://youngkyonyou.github.io/kubernetes/2021/07/27/Kubernetes-Mysql.html)**

<br>

위의 링크에서 했던 환경과 동일한 환경으로 구성한다.

<br>

그리고 스프링부트 프로젝트는 따로 만드는 것을 하진 않고 JPA와 연동된 프로젝트를 깃허브에서 받아온다. 해당 프로젝트는 <span style="color:#2ECC40; font-weight:bold">'코드로 배우는 스프링 부트 웹 프로젝트'</span>라는 책에 나오는 프로젝트 중 하나인 <span style="color:orange; font-weight:bold">Movie Review</span> 코드이다. 아래 깃허브 링크를 참고한다.

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

<br>

**[Movie Review](https://github.com/YoungKyonYou/MovieReview-SpringBoot/tree/master)**

<br>

그리고 **Superputty**를 키고 **m-k8s**에서

```bash
kubectl get pods -o wide
```

<br>

명령으로 mysql pod가 제대로 동작하고 있는지 확인한다.

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-06-12.png){: p}

<br>

<br><br>

---

<span style="color:#85144b; font-weight:bold; font-size: 30px">데이터베이스에 데이터 넣기</span>

<br><br><br>

<div class="webnots-warning webnots-notification-box">그 전에 Intellij나 다른 IDE로 프로젝트를 열고 데이터베이스 테이블 생성을 위해서 한 번 실행시켜준다.</div>

<br>

Intellij로 깃허브에서 받은 프로젝트를 열고 아래 사진과 같이 들어간다.

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-32-34.png){: p}

<br>

**repository** 패키지에는 **MemberRepositoryTests**, **MovieRepositoryTests**, **ReviewRepositoryTests**가 있는데 여기 클래스에 있는 메소드들을 실행시켜서 데이터베이스에 데이터를 넣어준다. 실행시켜줄 메소드는 아래와 같다.

**MemberRepositoryTests.java**

```java
@Autowired
    private ReviewRepository reviewRepository;
    @Rollback(false)
    @Test
    public void insertMembers(){
        IntStream.rangeClosed(1,100).forEach(i->{
           Member member=Member.builder()
                   .email("r"+i+"@zerock.org")
                   .pw("1111")
                   .nickname("reviewer"+i).build();
           memberRepository.save(member);
        });
    }
```

<br>

**MovieRepositoryTests.java**

```java
 @Commit
    @Transactional
    @Test
    public void insertMovies(){
        IntStream.rangeClosed(1,100).forEach(i->{
            Movie movie= Movie.builder().title("Movie..."+i).build();

            System.out.println("-------------------------------------");

            movieRepository.save(movie);

            int count=(int)(Math.random()*5)+1;

            for(int j=0;j<count;j++){
                MovieImage movieImage=MovieImage.builder()
                        .uuid(UUID.randomUUID().toString())
                        .movie(movie)
                        .imgName("test"+j+".jpg").build();
                imageRepository.save(movieImage);
            }
            System.out.println("====================================");
        });
    }
```

<br>

**ReviewRepositoryTests.java**

```java

    @Test
    public void insertMovieReviews(){
        IntStream.rangeClosed(1,200).forEach(i->{
            Long mno=(long)(Math.random()*100)+1;
            Long mid=((long)(Math.random()*100)+1);
            Member member= Member.builder().mid(mid).build();

            Review movieReview=Review.builder()
                    .member(member)
                    .movie(Movie.builder().mno(mno).build())
                    .grade((int)(Math.random()*5)+1)
                    .text("feeling about this movie is..."+i)
                    .build();
            reviewRepository.save(movieReview);
        });
    }
```

<br>

이 세가지 메소드를 실행하고 **Mysql-Workbench**에 들어가서 데이터가 정상적으로 들어갔는지 확인한다.(아래 사진 참고)

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-37-35.png){: p}

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-38-19.png){: p}

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-38-32.png){: p}

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-38-52.png){: p}

<br><br><br>

---

<span style="color:#85144b; font-weight:bold; font-size: 30px">JAR 파일 추출 및 도커 이미지로 만들기</span>

<br><br><br>

확인 했으면 깃허브에서 가져온 프로젝트의 **jar**파일을 추출한다.

인텔리제이 기준으로 프로젝트를 열면 아래 사진과 같이 우측에 **Gradle** 눌르고 **build->bootJar**를 더블 클릭한다.

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-24-58.png){: p}

<br>

잠깐 기다리면 **Jar**파일이 완성되고 이는 프로젝트가 있는 폴더에 들어가면 **build->libs**에서 찾을 수 있다.

<br>

그러면 **xxx.jar** 파일이 만들어진 것을 볼 수 있는데 이름이 복잡하니 아래 사진과 같이 **application.jar**로 이름을 변경한다.

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-27-11.png){: p}

<br>

**Superputty**로 돌아와서 **m-k8s**에서 **target** 폴더를 만든다.

```bash
mkdir target
```

<br>

이제 이 target 폴더 안에 아까 만들었던 **jar** 파일을 넣어줄 건데 우리는 **FileZilla**를 사용한다.

파일 질라를 연다. 그리고 위의 메뉴에서 **파일->사이트 관리자**에 들어간다.

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-32-06.png){: p}

<br>

프로토콜은 **SFTP**로 변경하고 호스트 아이피는 **m-k8s**의 아이피 주소를 넣는다. 사용자엔 **root**를 쓰고 비밀번호는 **vagrant**이다.

<div class="webnots-success webnots-notification-box">Vagrant로 Virtual Machine를 구성했을 때 디폴트 비밀번호가 'vagrant'이다.</div>

<div class="webnots-success webnots-notification-box">m-k8s의 아이피 주소는 Vagrantfile를 구성할 때 설정해 줬으며 명령어 kubectl get node -o wide로 확인할 수 있다.</div>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-32-41.png){: p}

<br>

이렇게 설정하고 연결을 누르면 m-k8s에 접속된다. 그리고 아까 **jar**파일을 우리가 만든 target 폴더에 넣는다.

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-36-38.png){: p}

<br>

자 이제 **FileZilla**를 닫고 **Superputty**로 돌아오자.

<br>

우리가 깃허브에서 가져온 프로젝트는 **java openjdk 11**버젼을 사용하므로 그것을 깔아야 한다. 그것은 아래 링크에 달린 블로그를 참고하도록 한다.

**[CentOS에서 자바 11 설치하기](https://growingsaja.tistory.com/357)**

<br>

설치가 완료되었다면 환경변수를 설정해줘야 한다. 이것 또한 아래 링크를 참고한다.

**[CentOS에서 자바 11버젼 환경변수 설정하기](https://www.hanumoka.net/2018/04/30/centOs-20180430-centos-install-jdk/)**

<br>

자 이제 **도커 이미지**를 만들기 위해 **Dockerfile**를 정의해 본다.

도커파일은 **root**에 만든다.

```bash
vi Dockerfile
```

<br>

**Dockerfile**

```Dockerfile
FROM openjdk:11
LABEL description="Echo OP Java Development"
EXPOSE 60431
COPY ./target/application.jar /opt/application.jar
WORKDIR /opt
ENTRYPOINT ["java", "-jar", "application.jar"]
```

<br>

한 줄 한 줄 알아가보자.

<br>

**Dockerfile**

```Dockerfile
#import opendjk:11 image를 하는 것과 같다.
#From <이미지 이름>:[태그] 형식으로 이미지를 가져온다.
#가져온 이미지 내부에서 컨테이너 이미지를 빌드한다. 즉 누군가가 만들어 놓은
#이미지에 필요한 부분을 추가한다고 보면 된다. 여기서는 openjdk를 기초 이미지로 사용한다.
FROM openjdk:11

#LABEL <레이블 이름>=<값>의 형식으로 이미지에 부가적인 설명을 위한 레이블을 추가할 때 사용한다.
LABEL description="Echo OP Java Development"

#EXPOSE <숫자>의 형식으로 생성된 이미지로 컨테이너를 구동할 때 어떤 포트를
#사용하는지 알려준다. EXPOSE를 사용한다고 해서 컨테이너를 구동할 때 자동으로
#해당 포트를 호스트 포트와 연결하지 않는다. 외부에서 접속하려면 docker run으로
#이미지를 컨테이너로 빌드할 때,반드시 -p 옵션을 넣어 포트를 연결해야 한다.
EXPOSE 60431

#호스트에서 새로 생성하는 컨테이너 이미지로 필요한 파일을 복사한다.
#COPY <호스트 경로> <컨테이너 경로>의 형식이다. 생성한 application.jar 파일을
# 이미지의 /opt/application.jar로 복사한다.
COPY ./target/application.jar /opt/application.jar

#이미지의 현재 작업 위치를 opt로 변경한다.
WORKDIR /opt

#ENTRYPOINT["명령어", "옵션"... "옵션"]의 형식이다.
#컨테이너 구동 시 ENTRYPOINT 뒤에 나오는 대괄호([]) 안에 든 명령을 실행한다.
#콤마(,)로 구분된 문자열 중 첫 번째 문자열은 실행할 명령어고,
#두 번째 문자열부터 명령어를 실행할 때 추가하는 옵션이다.
#여기서는 컨테이너를 구동할 때 java -jar application.jar이 실행된다는 의미이다.
#ENTRYPOINT로 실행하는 명령어는 컨테이너를 구동할 때 첫 번째로 실행된다.
#이 명령어로 실행된 프로세스 컨테이너 내부에서 첫 번째로 실행됐다는 의미로 PID는 1이 된다.
ENTRYPOINT ["java", "-jar", "application.jar"]
```

<br>

**Dockerfile**를 만들었다면 이제 이 파일이 있는 위치에서 **docker build -t springboot-img .**를 입력한다.

<br>

```bash
docker build -t springboot-img .
```

<br>

**docker build** 명령으로 컨테이너 이미지를 빌드한다. 여기서 사용된 **-t**(tag)는 만들어질 이미지를 의미하고 **.**(dot, 점)은 이미지에 원하는 내용을 추가하거나 변경하는 데 필요한 작업 공간을 현재 디렉터리로 지정한다는 의미다.

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-57-20.png){: p}

<br>

이미지가 제대로 만들어졌는지 확인한다.

```bash
docker images springboot-img
```

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-11-58-33.png){: p}

<br>

자 이제 **docker run**으로 컨테이너를 실행하고 docker ps로 컨테이너 상태를 출력한다.

```bash
docker run -d -p 60431:8080 --name springboot-run --restart always springboot-img
```

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-12-00-02.png){: p}

<br>

그리고 **http://192.168.1.10:60431/movie/list**로 접속해보자.

<br>

화면이 아래 사진과 같이 나오면 성공이다.

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-27-30.png){: p}

<br>

<div class="webnots-warning webnots-notification-box">위 사진처럼 화면이 나오면 성공이다. 하지만 화면 상에 REGISTER 버튼을 눌러서 서비스를 사용하고 나면 에러가 발생하니 그냥 한 예로서 제대로 배포됐는지만 확인하기</div>

<br>

이미지가 제대로 작동하는 것을 확인했으니 작동 중인 컨테이너를 중지 시키고 삭제한다.

**중지**

```bash
docker stop springboot-run
```

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-44-35.png){: p}

<br>

**작동 중인 컨테이너를 삭제**

```bash
docker rm springboot-run
```

<br>

<div class="webnots-information webnots-notification-box">작동 중인 컨테이너를 -f(force) 옵셔으로 바로 삭제해도 되지만 안전하게 작업하려면 작동을 중지시킨 후 삭제하는 것이 좋다. <br>
<span style="color:yellow; font-weight:bold">docker rmi -f $(docker images -q springboot-run)</span> </div>

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-50-39.png){: p}

<br>

**이미지 삭제**

```bash
docker rmi -f $(docker images -q springboot-img)
```

<br>

![](/images/Kubernetes/kubernetes-springboot/2021-07-30-13-47-22.png){: p}

<br>
