---
layout: post
title: SpringBoot에서 test할 때 나는 에러 해결 및 test 생략하는 방법
date: 2021-05-16 17:10:00 0000
tags: [Intellij, SpringBoot,gradle]
categories: [SpringBoot-Error]
description: Test events were not received
---

<br>

<br><br>

# <center>Test 에러 해결 및 생략하기</center>

<br>

졸업작품이 막바지로 다다르고 있다. 팀원들이랑 깃허브 리포지터리 하나를 파서 계속 프로젝트를 손보고 merge하는 식으로 하고 있는데 ec2 상에서 테스트 데이터를 삽입해서 실시간 모니터링 기능이 제대로 되나 확인해 보려던 중 오류가 났다.

![](/images/SpringBoot_Error/post4/2021-05-16-10-08-26.png)

<br>

나는 여기서 "test events were not received"라는 문구로 구글링해서 해결책을 찾기 시작했다.

모든 블로그에서 제시하는 해결책은 똑같았다.
바로

- Settings->Build, Execution, Deploymeny-> Gradle

에서 **Build and run using**과 **Run Tests using**를 Gradle에서 Intellij IDEA로 바꿔주는 것이다.

![](/images/SpringBoot_Error/post4/2021-05-16-10-09-52.png)

<br>

하지만 이 해결책만으로 나의 문제는 해결되지 않았다. 그랬더니 또 다른 에러가 났는데 에러 문구는 아래와 같다.

**Error running 'All in project-name': Command line is too long. Shorten command line for All in project-name or also for JUnit default configuration.**

<br>

다시 구글링해서 찾기 시작했다.

또 해결책이 제시되어 있어 확인했다.

- 프로젝트 루트 경로에서 .idea/workspace.xml에서 파일을 열어

```
 <component name = "PropertiesComponent">
 섹션 안에
 <property name="dynamic.classpath" value="true" />
 태그 추가.
```

<br>

하지만 이는 다른 에러로 이어졌고..... 나는 제대로 하고 있는 것 같지가 않았다.
과거에 즉 깃허브에서 merge 전에는 **Build and run using**과 **Run tests using**이 **Intellij IDEA**가 아니라 **Gradle**로도 제대로 작동했었는데 왜 merge한 순간부터 안 될까? 라는 생각을 해봤다.

<br>

곰곰이 생각하다가 전에 팀원 중에 한명이 테스팅이 안됐을 때 말해준 것이 생각이 났다!!!

## **"프로젝트 경로 사이사이에 한글이 포함되어 있으면 테스팅이 안되더라구요"**

<br>

이말이 머릿속에서 번쩍 떠오르더니 설마? 하고 봤지만 역시나 한글은 없었다...

_"당연히 없겠지.. merge전에는 제대로 됐었는데, 한글로 되어있었으면 과거에도 테스팅이 안됐을 거 아니니..."_

<br>

다시 구글링을 하고 여러 다른 해결책을 시도했지만 별다른 성과가 없자 깃허브 프로젝트를 가장 최근에 업데이트 시킨 팀원에게 물어봤다...

<br>

![](/images/SpringBoot_Error/post4/2021-05-16-10-19-36.png)

<br>

아 프로젝트 build.gradle 안에서 테스팅을 생략하게끔 만든 것이였다.
이것도 모르고 쓸데없는 해결책이나 찾고 다녔다는 생각에 허무해졌다...

**build.gradle**

```
test {
    useJUnitPlatform()
    exclude '**/*'
}
```

<br>

build.gradle 안에 위 코드를 추가하면 배포시 jar이나 war를 추출할 때 test method를 다 생략한다는 것이다. 아무래도 현재 ec2에 배포 작업을 하고 있고 그 과정에서 jar이나 war를 추출하는 과정에 있기 때문에 긴 테스트 메소드를 생략하기 위해서 넣은 코드였나 보다.

<br>

또 새로운 것을 배웠다. 잊지 않기 위해서 이렇게 기록해 두자..
