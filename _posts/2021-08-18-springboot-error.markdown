---
layout: post
title: HikariPool-1 - Failed to validate connection com.mysql.cj.jdbc.ConnectionImpl 에러 해결
date: 2021-08-16 13:00:00 0000
tags: [Intellij, SpringBoot, Book]
categories: [SpringBoot]
description: 갑자기 나타난 jpa 관련 에러
---



<br><br>

# <center>HikariPool-1 - Failed to validate connection com.mysql.cj.jdbc.ConnectionImpl</center>

<br>

졸업작품으로 이미 개발이 완료된 프로젝트가 하나 있었는데 쿠버네티스 클러스터 상에서 돌리고 싶어져서 테스트로 한번 켜보려고 하던 중 오류가 발생했다.

<br>

오류를 스크린샷을 못찍어서 사진은 없지만 해당 내용은 제목과 같은 오류였다. 구글에 찾아보니까 application.properties에 뭘 추가하고 무슨 time을 늘려주고 하는 것을 봤다.

아니 그런데 전에는 잘 돌아가던 것이 몇 달 지났다고 안 될리가 없었다. 그래서 데이터베이스 username과 password를 다시 한 번 확인하고 시도를 했으나 똑같은 오류가 났다.

<br>

분명한 것은 데이터베이스에서 나는 오류인데 현재 프로젝트는 AWS의 RDS를 사용하는 상태이다. RDS에서 문제가 나는 것인지 확신하기 위해서 application.properties에서 데이터베이스를 로컬로 변경해서 프로젝트를 실행했더니 

<br>

작동한다!!!

<br>

그럼 결국엔 rds 문제라는 건데... 뭐가 문제인지 알 수 없었다. 구글에서 서칭결과 나랑 비슷한 오류가 나지만 해결방법이 나랑은 전혀 상관이 없었던 내용이다. 그래서 일단 예전에 AWS의 EC2 상에 올려놨던 프로젝트를 배포 시켜봤더니 작동이 됐다. 그리고 혹시나 하고 프로젝트를 jar 파일로 만들어서 EC2로 옮긴다음 배포시켜보니 신기하게 작동이됐다.

<br>

그리고 뭐지? 하면서 다시 프로젝트를 인텔리제이에서 실행해보니 오류가 사라지고 실행이 정상적으로 되었다..

<br>

결국 내가 한 것은 jar 파일을 다시 생성한 것이다. 

<br>

진짜 원인이 뭔지 모르겠다. 그냥 우연이라기에는 내가 jar 파일을 만들기 전에 재부팅, 캐시 삭제 후 시작 등 다시 깃허브에서 clone해서 가져와서 실행해도 오류 나던 것이 jar 파일 하나 생성했다고 됐는데 이유가 뭘까?..

<br>

jar 파일을 만드는 과정을 한번 공부를 해봐야 할까?...