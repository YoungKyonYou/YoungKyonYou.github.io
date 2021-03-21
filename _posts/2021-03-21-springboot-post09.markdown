---
layout: post
title: Springboot JPA에서 Auto-increment 재정렬-02
date: 2021-03-21 10:00:00 0000
tags: [Intellij, SpringBoot, JPA]
categories: [SpringBoot]
description: 참조 관계에 있는 테이블의 Auto_increment 속성의 Key값 재정렬하기
---

<br><br>

# <center>참조 관계 AUTO_INCREMENT 재정렬</center>

<br>

저번 **Springboot JPA에서 Auto-increment 재정렬-01**에서는 단일 테이블에서 아이디 값으로 auto_increment 속성을 줬을 때 중간의 아이디를 삭제했을 때 재정렬하는 코드를 알아보았다.

이번에는 참조관계에 있는 테이블에서 아이디에 auto_increment 속성을 줬을 때 재정렬하는 방법을 알아보겠다. 사실 코드로 따지면 단 한줄 밖에 추가되지 않는다. 현재 내가 졸업작품으로 만들고 있는 프로젝트에서 설계하고 있는 데이터베이스는 크게 아래와 같다.

![](/images/SpringBoot/post09/2021-03-21-10-16-17.png)

<br>

MemberImage 엔티티에서 @ManyToOne를 선언해서 Member를 일대다(1:N)로 참조하고 있고 Status 엔티티에서도 @ManyToOne를 두번 선언해서 Member와 Facility를 일대다(1:N)로 참조하며 매핑 테이블 역할을 한다.

<br>

**MemberImage.java**

```java
package org.morgorithm.frames.entity;

import lombok.*;

import javax.persistence.*;
import java.time.LocalDate;
import java.time.LocalDateTime;

@Entity
@Builder
@NoArgsConstructor
@AllArgsConstructor
@Getter
@ToString(exclude="member")
public class MemberImage {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long inum;

    private String uuid;

    private String imgName;

    private String path;

    @ManyToOne(fetch=FetchType.LAZY)
    private Member member;
}

```

<br>

**Member.java**

```java
package org.morgorithm.frames.entity;


import lombok.*;


import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;


@Entity
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long mno;

    private String name;

    private String phone;
    public void changeName(String name){
        this.name=name;
    }
    public void changePhone(String phone){
        this.phone=phone;
    }
}

```

<br>
**Status.java**

```java
package org.morgorithm.frames.entity;

import com.sun.istack.Nullable;
import lombok.*;

import javax.persistence.*;
import java.time.LocalDateTime;

@Entity
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString(exclude={"member","facility"})

public class Status extends BaseEntity{
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long statusnum;

    @ManyToOne(fetch=FetchType.EAGER)
    private Member member;

    @ManyToOne(fetch=FetchType.EAGER)
    private Facility facility;

    @Column(scale=1)
    private double temperature;


    private Boolean state;

    @Override
    public LocalDateTime getRegDate() {
        return super.getRegDate();
    }

}

```

<br>

**Facility.java**

```java
package org.morgorithm.frames.entity;

import lombok.*;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
@Entity
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString
public class Facility {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long bno;

    private String building;
}

```

<br>

**Springboot JPA에서 Auto-increment 재정렬-01** 포스트에서 테이블 중간에 있는 컬럼 하나를 삭제하고 나서 재정렬하기 위해서 우리가 사용한 코드는 아래와 같다.

```
set @cnt=0;
update "테이블명" set "테이블명"."컬럼명"=@cnt:=@cnt+1;
```

<br>

이 코드를 리포지토리 인터페이스에서 @Query(쿼리 메소드)로 선언을 해서 아래와 같이 사용을 했다.

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

<br>

하지만 참조관계에 있는 테이블에서 재정렬하기 위해선 여기서 @Query 메소드를 하나 더 추가해주기만 하면 된다.

```java
    @Modifying
    @Transactional
    @Query(value="SET SQL_SAFE_UPDATES = 0", nativeQuery = true)
    void setSafeUpdate();


    @Modifying
    @Transactional
    @Query(value="set @cnt=0", nativeQuery = true)
    void initialCnt();


    @Modifying
    @Transactional
    @Query(value="update member set member.mno=@cnt\\:=@cnt+1",nativeQuery = true)
    void reorderKeyId();

```

<br>

바로 sql safe 모드라는 것인데 이 모드의 여러 단계 중에 가장 낮은 보안 모드로 바꿔서 그 스키마를 수정할 수 있도록 권한을 변경해주는 것이다. 그러기 위해서는 이 값을 0으로 해주면 된다. 반대로 다시 설정해주고 싶다면 1로 하면 된다.

<br>

결론적으로 나는 중간에 아이디 값을 삭제했을 때 재정렬을 위해서 이 세 개의 쿼리 메소드를 호출하도록 했다. 그렇게 하니까 정상적으로 재정렬하는 것을 볼 수 있었다.
