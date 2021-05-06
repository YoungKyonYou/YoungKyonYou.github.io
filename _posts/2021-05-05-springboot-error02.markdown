---
layout: post
title: Springboot "uses unchecked or unsafe operations" 에러
date: 2021-05-05 09:00:00 0000
tags: [Intellij, SpringBoot, error, test, folder path]
categories: [SpringBoot-Error]
description: Test Failure in SpringBoot
---

<br>

<br><br>

# <center>FAILURE: Build failed with an exception. 에러 해결</center>

<br>

졸업작품으로 프로젝트를 진행하던 차에 어떤 것을 실험해보려고 깃허브에서 Zip 파일을 다운받아서 새로 만든 폴더에 넣고 인텔리제이로 돌려보고 테스트 메소드를 돌리던 중 에러가 발생했다.

![](/images/SpringBoot_Error/post3/2021-05-05-10-04-24.png)

<br>

도저히 원인을 알 수 없었다. 구글링을 해봐도, stackoverflow에 질문을 해봐도 답을 알 수 없었다. 거기서 알려주는 해결 방법인 인텔리제이에서 **ctrl+alt+s**를 누르게 되면 아래 사진과 같이 창이 뜨게 된다.

![](/images/SpringBoot_Error/post3/2021-05-05-10-07-22.png)

<br>

거기서 **Build, Execution, Deployment-> Build Tools-> Gradle**에 들어가서 **Build and run using과 Run tests using:**를 **Gradle**이 아닌 **Intellij**로 바꿔주라는 것이였다.

<br>

이렇게 설정해도 역시나 테스트 failure가 발생했다...

~~때려 칠까..~~

<br>

그렇게 시간을 엄청 버리고 스트레스 받는 차에 졸업작품 단톡방에 한탄을 했다. 그랬더니 팀원 중 한명이 물어봤다.

\***\*"혹시 폴더 경로명에 한글로 되어 있는 거 없으시죠?" 저도 그걸로 고생 한동안 했었는데 한글 중간에 껴있으면 안되더라구요.\*\***

<br>

그때 아차 싶었다. 아 설마...

내 프로젝트의 경로 사이에 '**테스트**' 가 있었다. 아 이것 때문인가? 하고 영어로 바꿨더니 **정상동작**하기 시작했다..

<br>

알려준 팀원 중 한명은 평소에도 잘한다고 생각했지만 역시나... 경험은 무시할 게 안되나보다.

**결론:** 프로젝트 경로명 사이에 **한글**로 되어 있으면 오류가 난다...
