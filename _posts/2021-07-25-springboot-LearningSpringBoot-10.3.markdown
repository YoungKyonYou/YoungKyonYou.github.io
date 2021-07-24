---
layout: post
title: 프로젝트를 위한 JPA 처리
date: 2021-07-25 10:00:00 0000
tags: [Intellij, SpringBoot, Spring Security]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_

<br><br>

# <center>프로젝트를 위한 JPA 처리</center>

<br>

패키지와 자바 파일을 아래 사진과 같이 생성한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-3/2021-07-25-17-21-10.png)

<br>

**BaseEntity.java**

```java
package org.young.club.entity;

import lombok.Getter;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import javax.persistence.Column;
import javax.persistence.EntityListeners;
import javax.persistence.MappedSuperclass;
import java.time.LocalDateTime;

@MappedSuperclass
@EntityListeners(value={AuditingEntityListener.class})
@Getter
abstract class BaseEntity {
    @CreatedDate
    @Column(name="regdate",updatable=false)
    private LocalDateTime regDate;

    @LastModifiedDate
    @Column(name="moddate")
    private LocalDateTime modDate;
}
```

<br>

**ClubMember.java**

```java
package org.young.club.entity;

import lombok.*;

import javax.persistence.ElementCollection;
import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.Id;
import java.util.HashSet;
import java.util.Set;

@Entity
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString
public class ClubMember extends BaseEntity{
    @Id
    private String email;
    private String password;
    private String name;
    private boolean fromSocial;

    //이 어노테이션은 지정된 속성이 컬렉션을 사용할 것이라는 의미이다.
    //Entity가 아닌 단순한 형태의 객체 집합을 정의하고 관리하는 방법이다.
    //한 테이블에서 연관된 다른 테이블에 대한 정보를 다루는데 One-To-Many관계를 다룬다

    //Fetch Type은 크게 Eager와 Lazy 두 가지의 전략이 있습니다. Eager 전략은 엔티티를 조회할 때,
    // 연관 관계에 있는 엔티티도 함께 가져오고,
    // 반대로 Lazy 전략은 연관 관계 엔티티를 참조할 때 그때서야
    // 가져오게 됩니다.
    @ElementCollection(fetch= FetchType.LAZY)
    @Builder.Default
    private Set<ClubMemberRole> roleSet=new HashSet<>();

    public void addMemberRole(ClubMemberRole clubMemberRole){
        roleSet.add(clubMemberRole);
    }
}

```

<br>

**ClubMemberRole.java**

```java
package org.young.club.entity;

public enum ClubMemberRole {
    USER, MANAGER, ADMIN
}

```

<br>

ClubMember의 데이터 중에서 패스워드는 반드시 암호화해서 데이터를 추가해야 하기 때문에 테스트 코드를 작성해서 100개의 계정을 생성한다. 프로젝트 내에 repository 패키지를 추가한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-3/2021-07-25-17-31-33.png)

<br>

**ClubMemberRepository 인터페이스**

```java
package org.young.club.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.young.club.entity.ClubMember;

public interface ClubMemberRepository extends JpaRepository<ClubMember, String> {
}

```

<br>

테스트 데이터 생성을 위한 코드도 생성한다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part5/Chapter10/10-3/2021-07-25-17-32-44.png)

<br>

**ClubMemberTests.java**

```java
package org.young.club.security;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.young.club.entity.ClubMember;
import org.young.club.entity.ClubMemberRole;
import org.young.club.repository.ClubMemberRepository;

import java.util.stream.IntStream;

@SpringBootTest
public class ClubMemberTests {
    @Autowired
    private ClubMemberRepository repository;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @Test
    public void insertDummies(){
        //1-80까지는 USER만 지정
        //81-90까지는 USER, MANAGER
        //91-100까지는 USER, MANAGER, ADMIN

        IntStream.rangeClosed(1,100).forEach(i->{
            ClubMember clubMember= ClubMember.builder()
                    .email("user"+i+"@zerock.org")
                    .name("사용자"+i)
                    .fromSocial(false)
                    .password(passwordEncoder.encode("1111"))
                    .build();
            //default role
            clubMember.addMemberRole(ClubMemberRole.USER);

            if(i>80){
                clubMember.addMemberRole(ClubMemberRole.MANAGER);
            }
            if(i>90){
                clubMember.addMemberRole(ClubMemberRole.ADMIN);
            }
            repository.save(clubMember);
        });


    }
}

```

<br>

ClubMember 조회 시에는 이메일을 기준으로 조회하고 일반 로그인 사용자 뒤에 추가되는 소셜 로그인 사용자를 구분하기 위해서 ClubMemberRepository에 별도의 메서드로 처리한다.

<br>

**ClubMemberRepository 인터페이스**

```java
package org.young.club.repository;

import org.springframework.data.jpa.repository.EntityGraph;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import org.young.club.entity.ClubMember;

import java.util.Optional;

public interface ClubMemberRepository extends JpaRepository<ClubMember, String> {

    //EntityGraph는 연관 엔티티의 특정한 속성을 같이 로딩하도록 표시한다
    //기본적으로 JPA를 이용하는 경우에는 연관 관계의 FATCH 속성값은 LAZY로 지정하는 것이 일반적이다
    //@EntityGraph는 이러한 상황에서 특정 기능을 수행할 때만 EAGER 로딩을 하도록 지정할 수 있다.
    //attirubtePaths: 로딩 설정을 변경하고 싶은 속성의 이름을 배열로 명시한다
    //type: @EntityGraph를 어떤 방식으로 적용할 것인지를 설정
    //FATCH 속성값은 attributePaths에 명시한 속성은 EAGER로 처리하고 나머지는 LAZY로 처리한다.
    //LOAD 속성값은 attributePaths에 명시한 속성은 EAGER로 처리하고 나머지는 엔티티 클래스에 명시되거나 기본 방식으로 처리한다.

    //EntityGraph를 이용해서 'left outer join'으로 ClubMemberRole이 처리될 수 있도록 한다.
    @EntityGraph(attributePaths = {"roleSet"}, type=EntityGraph.EntityGraphType.LOAD)
    @Query("select m from ClubMember m where m.fromSocial=:social and m.email=:email")
    //Optional은 non-null 값을 가지고 있거나 안 가지고 있을 수 있는 컨테이너 오브젝트이다
    // 값이 존재하면 isPresent()는 true를 반환하고
   //값이 존재하지 않으면 false를 반환한다. 객체를 감싸고 그 안에 값이 있는지 없는지 유무를 판별하기 좋다.
    Optional<ClubMember> findByEmail(@Param("email") String email,@Param("social") boolean social);
}

```

<br>
