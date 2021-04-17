---
layout: post
title: SpringBoot에서 시간을 MySql에 Update할 때 9시간 차이 나는 에러
date: 2021-04-03 17:00:00 0000
tags: [Intellij, SpringBoot, Mysql]
categories: [SpringBoot-Error]
description: LocalDateTime으로 Mysql 기록 시 9시간이 차이 나는 에러 해결
---

<br>

<br><br>

# <center>9시간 차이 나는 에러 해결하기</center>

<br>

스프링부트로 앱을 만들다가 심각한 에러를 하나 발견했다. 현재 내 앱은 사람들이 어떤 건물을 출입하게 되면 시간을 책정해서 mysql에 올려주게 되어 있는데 책정되는 실제 시간이랑 mysql에 올려지는 시간이 9시간 차이가 나게 되는 것이다.

<br>

이는 매우 심각한 문제여서 빠른 해결이 필요했다. 일단 인터넷을 검색한 결과 많은 수단을 써봤다.

<br>

1. 첫 번째 방법

```sql
SELECT @@global.time_zone, @@session.time_zone;
```

<br>

위 코드를 입력해서 결과를 먼저 본다.

지금은 +09:00으로 양쪽다 되어 있지만 원래는 이게 설정전에는 **SYSTEM**으로 둘다 나온다.

![](../images/SpringBoot_Error/post2/2021-04-03-17-08-14.png)

<br>

위 사진과 같이 바꾸는 코드는 아래와 같다

```sql
SET @@session.time_zone='+09:00';
```

<br>

**하지만 해결이 되지 않았다...**

그래서 다시 찾아봤다.

2. 두 번째 방법

```sql
SELECT CURRENT_TIMESTAMP();
```

위 코드를 치게 되면 아래 사진과 같이 나온다.

![](../images/SpringBoot_Error/post2/2021-04-03-17-14-48.png)

<br>

원래는 이게 지금은 현재 시간을 나타내지만 처음 설정 전에는 9시간 이전 시간으로 나타났던 것 같다. 그래서 아래와 같이 설정했더니 정상적으로 현재 시간이 나오게 되었다.

```sql
DELIMITER //
CREATE TRIGGER `update_to_utc` BEFORE INSERT ON `my_table` FOR EACH ROW BEGIN
set new.my_field=utc_timestamp();
END//
DELIMITER ;
```

<br>

**하지만 이 역시도 해결이 되지 않았다...**

다시 구글링을 해본 결과 나랑 똑같은 현상을 겪는 사람의 글을 발견해서 해결책을 찾을 수 있었다.

3. 세 번째 방법

생각 보다 너무 간단해서 현타가 왔다.
바로 스프링부트의 application.properties에서 datasource만 조금 변경하면 되는 것이다.

**application.properties**

```
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.datasource.url=jdbc:mysql://localhost:3306/frames?serverTimezone=Asia/Seoul&characterEncoding=UTF-8

(...)
```

<br>

바로 **serverTimezone=UTC**를 **serverTimezone=Asia/Seoul**로 바꿔주면 되는 것이다.

이렇게 하니까 해결이 되었다.
