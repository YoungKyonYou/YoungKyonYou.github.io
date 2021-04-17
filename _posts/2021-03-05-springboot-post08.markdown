---
layout: post
title: Springboot JPA에서 Auto-increment 재정렬-01
date: 2021-03-05 19:00:00 0000
tags: [Intellij, SpringBoot, JPA]
categories: [SpringBoot]
description: 특정 테이블의 Auto_increment 속성의 Key값 재정렬하기
---

<br><br>

# <center>AUTO_INCREMENT 재정렬</center>

<br>

코드로 배우는 스프링 부트 웹프로젝트 책에서 나오는 guestbook 실습을 하던 중에 궁금증이 생겼다. Part 2의 게시판을 만들고 있는데 local8080/guest/list로 접속했을 때의 모습을 일단 보자.

![](../images/SpringBoot/post08/2021-03-05-19-58-07.png)

<br>

이렇게 보면 아무 문제가 없어 보일 수 있다. 하지만 여기서의 문제는 저 많은 게시물 중 중간에 하나를 지웠을 때 어떻게 변하는 지 보자. 여기서는 예로 게시물 **298번**을 지워보겠다.

![](../images/SpringBoot/post08/2021-03-05-19-59-37.png)

<br>

위의 사진을 보면 문제가 확연히 보인다. 바로 게시물 번호가 순서대로 업데이트가 안되고 그대로를 유지해서 연속적인 순서 보장이 안 된다는 것이다. 참고로 여기서 쓴 게시물 번호는 아래 사진에서 처럼 Long gno에서 따온 것이다. GeneratedValue 어노테이션으로 Auto_increment를 구현하고 테스트 데이터를 넣어서 그 데이터로 위의 사진과 같이 리스트를 만든 것이다.

![](../images/SpringBoot/post08/2021-03-06-09-14-56.png)

<br>

**gusetbook table**

![](../images/SpringBoot/post08/2021-03-05-20-02-48.png)

<br>

mysql workbench를 확인하니 여기서도 우리가 삭제했던 gno=298를 제외하고 그대로 있는 것을 볼 수 있다. 일단 문제 해결의 순서는 이 워크벤치에서 저 auto-increment를 재정렬하는 방법을 찾으면 그것을 springboot의 @Query로 해결할 수 있다는 것이다.

그리고 구글링과 stackoverflow를 뒤진 결과 해결 방법은 아래와 같다.

```sql
set @cnt=0;
update "테이블명" set "테이블명"."컬럼명"=@cnt:=@cnt+1;
```

<br>

이것을 입력해주고 execute query를 해주면 auto_increment가 재정렬 되는 것을 볼 수 있다.

![](../images/SpringBoot/post08/2021-03-05-20-08-12.png)

<br>

자 이제 프로젝트에 적용해보자. @Query를 쓰기 위해 repository 클래스에서 해당 코드를 입력한다

**repository class**

```java
    @Modifying
    @Transactional
    @Query(value="set @cnt=0", nativeQuery = true)
    void initialCnt();


    @Modifying
    @Transactional
    @Query(value="update guestbook set guestbook.gno=@cnt\\:=@cnt+1",nativeQuery = true)
    void reorderKeyId();
```

![](../images/SpringBoot/post08/2021-03-05-20-10-35.png)

<br>

nativeQuery=true를 사용하면 sql 원시 코드를 사용할 수 있다. 그리고 reorderKeyId() 메소드를 보면 중간에 역슬레시 두개가 보인다. 이는 @Query가 ':'를 제대로 인식하지 못하기 때문에 앞에 역슬레시 2번을 해주는 건데 안 해주면 에러가 발생한다.

<br>

**org.springframework.dao.InvalidDataAccessApiUsageException: org.hibernate.QueryException: Space is not allowed after parameter prefix ':'**

<br>

그리고 해당 게시물을 삭제할 때 실행되는 service 클래스의 remove 메소드로 가보자.

![](../images/SpringBoot/post08/2021-03-05-20-13-09.png)

<br>

위 사진의 코드는 controller에서 서비스 주입을 받은 서비스 객체가 remove 메서드를 호출하면 해당 게시물이 db에서 삭제된다. 이때 삭제 처리 후 우리가 위해서 적었던 메서드 2개를 같이 호출 해 주면 auto_increment가 재정렬되어 실제 앱을 키고 특정 게시물을 삭제하면 재정렬이 되서 화면에 출력될 것이다.

자 그럼 확인해 보자.

아래 사진은 초기 화면이다.

![](../images/SpringBoot/post08/2021-03-05-20-15-42.png)

<br>

이제 298번 게시물을 다시 삭제해 본다.

![](../images/SpringBoot/post08/2021-03-05-20-16-12.png)

<br>

보시다시피 제대로 재정렬이되서 보여지는 것을 볼 수 있다.

---

다음 게시물에서는 만약 auto_increment 속성을 가진 특정 테이블의 PK을 외부키로 쓰고 있는 다른 테이블의 FK까지 재정렬하는 방법을 살펴보자.
