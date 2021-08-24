---
layout: post
title: JPA 다루기-스프링 부트와 AWS로 혼자 구현하는 웹 서비스-3-1
date: 2021-08-16 13:00:00 0000
tags: [Intellij, SpringBoot, Book]
categories: [SpringBoot]
description: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '스프링 부트와 AWS로 혼자 구현하는 웹 서비스'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>JPA 다루기</center>

<br>

개발자는 <span style="color:orange; font-weight:bold">객체지향적으로 프로그래밍을 하고,</span> JPA가 이를 관계형 데이터베이스에 맞게 SQL을 대신 생성해서 실행한다. 개발자는 항상 객체지향적으로 코드를 표현할 수 있으니 더는 SQL에 종속적인 개발을 하지 않아도 된다.

<br>

<span style="color:orange; font-weight:bold">객체 중심으로</span> 개발을 하게 되니 생산성 향상은 물론 유지 보수하기가 정말 편한다. 이런 점 때문에 규모가 크고 365일 24시간, 대규모 트래픽과 데이터를 가진 서비스에서 JPA는 점점 표준 기술로 자리 잡고 있다.

<br>

<span style="color:orange; font-weight:bold">JPA</span>는 인터페이스로서 자바 표준명세서이다. 인터페이스인 JPA를 사용하기 위해서는 구현체가 필요하다. 대표적으로 <span style="color:orange; font-weight:bold">Hibernate, Eclipse Link</span> 등이 있다. 하지만 Spring에서 JPA를 사용할 때는 이 구현체들을 직접 다루진 않는다.

<br>

구현체들을 좀 더 쉽게 사용하고자 추상화시킨 <span style="color:orange; font-weight:bold">Spring Data JPA</span>라는 모듈을 이용하여 JPA 기술을 다룬다. 이들의 관계를 보면 다음과 같다.

<br>

- <span style="color:#85144b; font-weight:bold">JPA <- Hibernate <- Spring Data JPA</span>

<br>

Hibernate를 쓰는 것과 Spring Data JPA를 쓰는 것 사이에는 큰 차이가 없다. 그럼에도 스프링 진영에서는 Spring Data JPA를 개발했고 이를 권장하고 있다. 이렇게 한 단계 더 감싸놓은 Spring Data JPA가 등장한 이유는 크게 두 가지가 있다.

<br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">구현체 교체의 용이성</span><br><br>

- <span style="color: rgba(131, 24, 67); font-weight:bold">저장소 교체의 용이성</span><br><br>

<br>

<span style="color:orange; font-weight:bold">구현체 교체의 용이성</span>이란 Hibernate 외에 다른 구현체로 쉽게 교체하기 위함이다. <span style="color:orange; font-weight:bold">저장소 교체의 용시어</span>이란 관계형 데이터베이스 외에 다른 저장소로 쉽게 교체하기 위함이다.

<br>

앞으로 게시판을 만들어보고 AWS에 무중단 배포 하는 것까지 진행해 본다.

<br>

<span style="color:#3D9970; font-weight:bold">게시판 기능</span>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">게시글 조회</div>
<div class="webnots-success webnots-notification-box">게시글 등록</div>
<div class="webnots-success webnots-notification-box">게시글 수정</div>
<div class="webnots-success webnots-notification-box">게시글 삭제</div>

<br>

<span style="color:#3D9970; font-weight:bold">회원 기능</span>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">

<div class="webnots-success webnots-notification-box">구글/네이버 로그인</div>
<div class="webnots-success webnots-notification-box">로그인한 사용자 글 작성 권한</div>
<div class="webnots-success webnots-notification-box">본인 작성 글에 대한 권한 관리</div>

<br>

프로젝트에 Spring Data Jpa를 적용해야 하는데 우리는 이미 프로젝트를 만들 때 Spring Data Jpa 의존성을 포함시켰다. 아래 링크를 참조하자.

<br>

**[Project 생성](https://youngkyonyou.github.io/springboot/2021/08/13/springboot-ISBWAWS-1.html)**

<br>

프로젝트를 처음 만들 때 **build.gradle**에서 우리는 <span style="color:orange; font-weight:bold">Spring Data Jpa</span> 의존성 부분을 주석처리 해줬었다. 데이터베이스를 등록하지 않아서 오류가 날 수 있기 때문이다. 이제 그 주석을 푼다.

<br>

**build.gradle**

```gradle
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

//인메모리 관계형 데이터베이스이다.
//별도의 설치가 필요 없이 프로젝트 의존성만으로 관리할 수 있다.
//메모리에서 실행되기 때문에 애플리케이션을 재시작할 때마다 초기화된다는 점을 이용하여
//테스트 용도로 많이 사용된다. JPA의 테스트, 로컬 환경에서의 구동에서 사용한다.
runtimeOnly 'com.h2database:h2'
```

<br>

의존성이 등록되었다면 본격적으로 JPA 기능을 사용해 본다. 아래 사진과 같이 패키지와 자바 파일을 생성한다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-3/2021-08-16-15-53-17.png){: p}

<br>

**Posts.java**

```java
package com.yyk.app.freelecspringbootboard.domain.posts;

import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.persistence.*;
//아래 둘은 롬복의 어노테이션이다.
@Getter
//기본 생성자 자동 생성
@NoArgsConstructor

//JPA의 어노테이션이다.
//테이블과 링크될 클래스임을 나타낸다.
@Entity
public class Posts {
    //해당 테이블의 PK 필드를 나타낸다.
    @Id
    //스프링 부트 2.0에서는 GenerationType.IDENTITY 옵션을 추가해야만
    //auto-increment가 된다.
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    //테이블의 컬럼을 나타내며 굳이 선언하지 않더라도 해당 클래스의 필드는 모두 컬럼이 된다.
    //사용하는 이유는 기본값 외에 추가로 변경이 필요한 옵션이 있을 때 사용한다.
    //문자열의 경우 VARCHAR(255)가 기본값인데 사이즈를 500으로 늘리고 싶거나
    //타입을 TEXT로 변경하고 싶거나 등의 경우에 사용된다.
    @Column(length=500, nullable=false)
    private String title;

    @Column(columnDefinition = "TEXT", nullable=false)
    private String content;

    private String author;

    //해당 클래스의 빌더 패턴 클래스를 생성
    //생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함
    @Builder
    public Posts(String title, String content, String author){
        this.title=title;
        this.content=content;
        this.author=author;
    }
}

```

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

이 Posts 클래스에는 한 가지 특이점이 있다. 바로 Setter 메소드가 없다는 점이다. 자바빈 규약을 생각하면서 getter/setter를 무작정 생성하는 경우가 있다. 이렇게 되면 해당 클래스의 인스턴스 값들이 언제 어디서 변해야 하는지 코드상으로 명확하게 구분할 수가 없어 차후 기능 변경 시 정말 복잡해 진다. 그래서 Entity 클래스에서는 절대 Setter 메소드를 만들지 않는다. 대신 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야만 한다.</div>

<br>

Setter가 없는 상황에서 어떻게 값을 채워 DB에 삽입해야 할까? 기본적인 구조는 생성자를 통해 최종값을 채운 후 DB에 삽입하는 거이며 값 변경이 필요한 경우 해당 이벤트에 맞는 public 메소드를 호출하여 변경하는 것을 전제로 한다. 

<br>

Posts 클래스 생성이 끝났다면 Posts 클래스로 Database를 접근하게 해줄 JpaRepository를 생성한다. 

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-3/2021-08-16-16-10-59.png){: p}

<br>

**PostsRepository.java**

```java
package com.yyk.app.freelecspringbootboard.domain.posts;

import org.springframework.data.jpa.repository.JpaRepository;

public interface PostsRepository extends JpaRepository<Posts, Long> {
}

```

<br>

JpaRepository<Entity 클래스, PK 타입>를 상속하면 기본적인 CRUD 메소드가 자동으로 생성된다.

<br>

모두 작성되었다면 간단하게 테스트 코드로 기능을 검증해 본다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-3/2021-08-16-16-40-01.png){: p}

<br>

**PostsRepositoryTest.java**

```java
package com.yyk.app.freelecspringbootboard.domain.posts;

import org.junit.After;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

import java.util.List;

import static org.assertj.core.api.Assertions.assertThat;


@RunWith(SpringRunner.class)
@SpringBootTest
public class PostsRepositoryTest {
    @Autowired
    PostsRepository postsRepository;

    //Junit에서 단위 테스트가 끝날 때마다 수행되는 메소드를 지정한다.
    //보통은 배포 전 전체 테스트를 수행할 때 테스트간 데이터 침범을 막기 위해 사용한다.
    //여러 테스트가 동시에 수행되면 테스트 실행시 테스트가 실패할 수 있다.
    @After
    public void cleanup(){
        postsRepository.deleteAll();
    }

    @Test
    public void 게시글저장_불러오기(){
        String title="테스트 게시글";
        String content="테스트본문";

        postsRepository.save(Posts.builder()
                .title(title)
                .content(content)
                .author("jojoldu@gmail.com")
                .build());

        //테이블 posts에 있는 모든 데이터를 조회해오는 메소드이다.
        List<Posts> postsList=postsRepository.findAll();

        Posts posts=postsList.get(0);
        assertThat(posts.getTitle()).isEqualTo(title);
        assertThat(posts.getContent()).isEqualTo(content);
    }
}

```

<br>

별다른 설정 없이 @SpringBootTest를 사용할 경우 <span style="color:orange; font-weight:bold">H2 데이터베이스</span>를 자동으로 실행해 준다. 이 테스트 역시 실행할 경우 H2가 자동으로 실행된다. 이제 테스트 코드를 한번 실행해 본다. 

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-3/2021-08-16-16-50-15.png){: p}

<br>

그리고 실행된 쿼리를 볼 수 있게 **application.properties**에 아래 내용을 추가한다.

<br>

**application.properties**

```application.properties
spring.jpa.show_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
spring.jpa.properties.hibernate.dialect.storage_engine=innodb
spring.datasource.hikari.jdbc-url=jdbc:h2:mem://localhost/~/testdb;MODE=MYSQL
```

<br>

그리고 다시 실행해 보면 콘솔을 통해 쿼리 로그를 볼 수 있다.

<br>

![](/images/SpringBoot/ImplementingWebServiceWithSpringBootAndAWS-3/2021-08-16-17-08-26.png){: p}

<br>


