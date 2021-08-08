---
layout: post
title: API 서비스 만들기-코드로 배우는 스프링 부트 웹 프로젝트-12.-1
date: 2021-08-08 11:00:00 0000
tags: [Intellij, SpringBoot, Spring Security, API Service]
categories: [SpringBoot]
description: 코드로 배우는 스프링 부트 웹 프로젝트
---

<span style="color:orange; font-weight:bold">_해당 내용은 책 '코드로 배우는 스프링 부트 웹 프로젝트'에 나오는 내용이며 이는 개인적으로 공부하기 위해 기록함을 알려드립니다_</span>

<br><br>

# <center>API 서비스 만들기</center>

<br>

API 서버는 쉽게 말해서 순수하게 원하는 데이터만을 제공하는 서버라고 생각할 수 있다. 데이터만 제공하기 때문에 클라이언트의 기술이 어떻게 이루어 지는지는 중요하지 않고 서버의 데이터를 여러 형태로 사용하는 것이 가능하다.

<br>

예제에서는 간단한 Note를 작성하고 이용하는 예제를 구성한다. 이를 위해 가장 먼저 해야 하는 일은 단순히 JSON 처리를 하는 API 기능을 구성한다. 프로젝트에 entity 패키지 내에 Note 엔티티 클래스를 추가한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-17-36-18.png){: p}

<br>

**Note.java**

```java
package org.young.club.entity;

import lombok.*;

import javax.persistence.*;

@Entity
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Getter
@ToString
public class Note extends BaseEntity{
    @Id
    @GeneratedValue(strategy= GenerationType.IDENTITY)
    private Long num;

    private String title;

    private String content;

    @ManyToOne(fetch= FetchType.LAZY)
    private ClubMember writer;

    public void changeTitle(String title){
        this.title=title;
    }
    public void changeContent(String content){
        this.content=content;
    }
}
```

<br>

Note 클래스는 Clubmember와 @ManyToOne의 관계로 구성하고, 나중에 로그인한 사용자와 비교하기 위해 사용한다. Note에서 수정이 가능한 부분은 제목(title)과 내용(content)이므로 이에 대한 수정이 가능하도록 changetitle(), changeContent()를 구성한다. Note에 대한 JPA 처리는 NoteRepository를 구성한다.

<br>

![](../images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-17-44-27.png){: p}

<br>

**NoteRepository.java**

```java
package org.young.club.repository;

import org.springframework.data.jpa.repository.EntityGraph;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.young.club.entity.Note;

import java.util.List;
import java.util.Optional;

public interface NoteRepository extends JpaRepository<Note,Long> {

    /*
        @EntityGraph는 엔티티의 특정한 속성을 같이 로딩하도록 표시하는 어노테이션이다. 기본적으로 JPA를 이용하는 경우에는 연관 관계의 FATCH 속성값은 LAZY로 지정하는 것이 일반적이다.
        @EntityGraph는 이러한 상황에서 특정 기능을 수행할 때만 EAGER 로딩을 하도록 지정할 수 있다.
        @EntityGraph는 attributePaths 속성과 type 속성을 가지고 있다.

        attributePaths: 로딩 설정을 변경하고 싶은 속성의 이름을 배열로 명시한다.
        type: @EntityGraph를 어떤 방식으로 적용할 것인지를 설정한다.
        FATCH 속성값은 attributePaths에 명시한 속성은 EAGER로 처리하고 나머지는 LAZY로 처리한다.
        LOAD 속성값은 attributePaths에 명시한 속성은 EAGER로 처리하고, 나머지는 엔티티 클래스에 명시되거나 기본 방식으로 처리한다.
    */
    //여기서는 Note를 질의할 때 ClubMember도 같이 로딩하기 위해서 사용하는 것이다.
    @EntityGraph(attributePaths="writer", type=EntityGraph.EntityGraphType.LOAD)
    @Query("select n from Note n where n.num=:num")
    Optional<Note> getWithWrtier(Long num);

    @EntityGraph(attributePaths = {"writer"}, type=EntityGraph.EntityGraphType.LOAD)
    @Query("select n from Note n where n.writer.email=:email")
    List<Note> getList(String email);
}

```

<br>

<link rel="stylesheet" href="https: //www.webnots.com/resources/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" href="/assets/css/webnots.css">
<div class="webnots-information webnots-notification-box">ClubMember를 @EntityGraph를 사용해서 처리할 때 ClubMember의 roleSet이 toString()에 사용되지 않도록 주의한다. 만일 roleSet까지 같이 로딩하고 싶다면 attributePaths={"writer", "writer.roleSet"}과 같이 구성할 수 있다. </div>

<br>

Note 엔티티를 다루기 위해서 중간에 NoteDTO를 구성하고, 이를 이요하는 서비스 계층을 설계해 본다. 프로젝트 내에 dto 패키지를 구성하고 NoteDTO를 구성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-02-36.png){: p}

<br>

**NoteDTO.java**

```java
package org.young.club.security.dto;


import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.time.LocalDateTime;

@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class NoteDTO {
    private Long num;
    private String title;
    private String content;
    private String writerEmail;
    private LocalDateTime regDate, modDate;
}

```

<br>

프로젝트에 service 패키지를 구성하고, NoteService와 NoteServiceImpl 클래스를 구성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-23-36.png){: p}

<br>

**NoteDTO.java**

```java
package org.young.club.security.dto;


import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.time.LocalDateTime;

@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class NoteDTO {
    private Long num;
    private String title;
    private String content;
    private String writerEmail;
    private LocalDateTime regDate, modDate;
}

```

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-25-35.png){: p}

<br>

**NoteService.java**

```java
package org.young.club.security.service;


import org.young.club.entity.ClubMember;
import org.young.club.entity.Note;
import org.young.club.security.dto.NoteDTO;

import java.util.List;

public interface NoteServiceImpl {
    Long register(NoteDTO noteDTO);

    NoteDTO get(Long num);

    void modify(NoteDTO noteDTO);

    void remove(Long num);

    List<NoteDTO> getAllWithWriter(String writerEmail);

    default Note dtoToEntity(NoteDTO noteDTO){
        Note note=Note.builder()
                .num(noteDTO.getNum())
                .title(noteDTO.getTitle())
                .content(noteDTO.getContent())
                .writer(ClubMember.builder().email(noteDTO.getWriterEmail()).build())
                .build();
        return note;
    }
    default NoteDTO entityToDTO(Note note){
        NoteDTO noteDTO=NoteDTO.builder()
                .num(note.getNum())
                .content(note.getContent())
                .writerEmail(note.getWriter().getEmail())
                .regDate(note.getRegDate())
                .modDate(note.getModDate())
                .build();
        return noteDTO;
    }
}

```

<br>

NoteService 인터페이스는 CRUD 기능과 entityToDto(), dtoToEntity() 기능을 구현한다.

<br>

**NoteServiceImpl.java**

```java
package org.young.club.security.service;

import lombok.RequiredArgsConstructor;
import lombok.extern.log4j.Log4j2;
import org.springframework.stereotype.Service;
import org.young.club.entity.Note;
import org.young.club.repository.NoteRepository;
import org.young.club.security.dto.NoteDTO;

import java.util.List;
import java.util.Optional;
import java.util.stream.Collectors;

@Service
@Log4j2
@RequiredArgsConstructor
public class NoteService implements NoteServiceImpl{

    private final NoteRepository noteRepository;

    @Override
    public Long register(NoteDTO noteDTO) {
        Note note=dtoToEntity(noteDTO);

        log.info("================");
        log.info(note);
        noteRepository.save(note);
        return note.getNum();
    }

    @Override
    public NoteDTO get(Long num) {
        Optional<Note> result = noteRepository.getWithWrtier(num);
        if(result.isPresent())
            return entityToDTO(result.get());

        return null;
    }

    @Override
    public void modify(NoteDTO noteDTO) {
        Long num=noteDTO.getNum();

        Optional<Note> result=noteRepository.findById(num);

        if(result.isPresent()){
            Note note=result.get();
            note.changeTitle(noteDTO.getTitle());
            note.changeContent(noteDTO.getContent());
            noteRepository.save(note);
        }
    }

    @Override
    public void remove(Long num) {
        noteRepository.deleteById(num);
    }

    @Override
    public List<NoteDTO> getAllWithWriter(String writerEmail) {
        List<Note> noteList=noteRepository.getList(writerEmail);

        return noteList.stream().map(note->entityToDTO(note)).collect(Collectors.toList());
    }
}

```

<br>

JSON으로 데이터를 처리하는 NoteController는 @RestController를 사용해서 구현한다. 구현 시에는 화면이 없는 상태이므로 REST 방식을 테스트할 수 있는 크롬 확장 프로그램을 사용한다. controller 패키지에 NoteController를 아래와 같이 작성한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-41-47.png){: p}

<br>

**NoteController.java**

```java
package org.young.club.controller;

import lombok.RequiredArgsConstructor;
import lombok.extern.java.Log;
import lombok.extern.log4j.Log4j2;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.young.club.security.dto.NoteDTO;
import org.young.club.security.service.NoteService;

@RestController
@Log4j2
@RequestMapping("/notes/")
@RequiredArgsConstructor
public class NoteController {
    private final NoteService noteservice;

    @PostMapping(value="")
    public ResponseEntity<Long> register(@RequestBody NoteDTO noteDTO){
        log.info("---------register------------------------");
        log.info(noteDTO);

        Long num=noteservice.register(noteDTO);

        return new ResponseEntity<>(num, HttpStatus.OK);
    }
}

```

<br>

NoteController에는 POST 방식으로 새로운 Note를 등록할 수 있는 기능을 작성한다. register()에는 @ReqeustBody를 이용해서 JSON 데이터를 받아서 NoteDTO로 변환할 수 있도록 한다.

<br>

<span style="color:#85144b; font-weight:bold; font-size: 30px">크롬 확장 프로그램을 이용한 POST 방식 테스트</span>

<br>

Thymeleaf를 이용하는 화면이 없는 상황이므로 브라우저에서 사용 가능한 REST 방식의 테스트 도구를 이용한다. 크롬 브라우저의 확장 프로그램 중에서 'Yet Another REST Client'를 이용했지만 PostMan이나 기타 다른 프로그램을 사용해도 무방하다. <span style="color:orange; font-weight:bold">나는 여기서 POSTMAN를 사용해 본다.</span>

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-45-26.png){: p}

<br>

프로젝트를 실행한 후에 REST 테스트를 진행한다. POST 방식을 선택하고 JSON 타입의 데이터를 작성한다. 작성할 때 주의할 점은 writerEmail은 반드시 데이터베이스에 있는 ClubMember의 메일 계정을 사용해야 한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-54-09.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-53-47.png){: p}

<br>

위의 세팅이 완료된 상태에서 Send를 누르면 Note의 num을 확인할 수 있다.

<br>

NoteController에는 GET 방식으로 특정한 번호의 Note를 확인할 수 있는 기능을 추가한다.

**NoteController.java**

```java
(...)
    //ResponseEntity를 리턴할 때 어떤 Mime Type으로 할 것인지 지정한다
    //Json이 리턴됨으로 Application Json Value로 지정한다.
    @GetMapping(value="/{num}", produces= MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<NoteDTO> read(@PathVariable("num") Long num){

        log.info("-----------------------read------------------------");
        log.info(num);
        return new ResponseEntity<>(noteService.get(num), HttpStatus.OK);
    }
(...)

```

<br>

read()는 @PathVariable을 사용해서 경로에 있는 Note의 num을 얻어서 해당 Note 정보를 반환한다. GET 방식은 브라우저에서도 확인할 수 있지만 REST 테스트 도구를 이용할 수도 있다. 현재 존재하는 Note의 번호를 '/note/2'와 같이 @PathVariable로 지정할 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-18-58-46.png){: p}

<br>

NoteController에는 특정 이메일을 가진 회원(나중에 시큐리티로 처리할)이 작성한 모든 Note를 조회할 수 있는 기능을 아래와 같이 구현한다.

**NoteController.java**

```java
(...)
    //ResponseEntity를 리턴할 때 어떤 Mime Type으로 할 것인지 지정한다
    //Json이 리턴됨으로 Application Json Value로 지정한다.
    @GetMapping(value="/all", produces= MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<List<NoteDTO>> getList(String email){

        log.info("-----------------------getList------------------------");
        log.info(email);
        return new ResponseEntity<>(noteService.getAllWithWriter(email), HttpStatus.OK);
    }
(...)
```

<br>

getList()는 파라미터로 전달되는 이메일 주소를 통해서 해당 회원이 작성한 모든 Note에 대한 정보를 JSON으로 반환한다. 여러 개의 Note를 추가한 상태에서 GET 방식으로 확인하면 아래와 같이 JSON의 배열을 확인할 수 있다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-19-04-44.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-19-04-51.png){: p}

<br>

Note의 삭제는 DELETE 방식으로 처리한다. 응답에 사용하는 포맷은 단순한 문자열로 지정한다.

<br>

**NoteController.java**

```java
(...)

    @DeleteMapping(value="/{num}", produces=MediaType.TEXT_PLAIN_VALUE)
    public ResponseEntity<String> remove(@PathVariable("num") Long num){
        log.info("-----------remove-----");
        log.info(num);

        noteService.remove(num);

        return new ResponseEntity<>("removed", HttpStatus.OK);
    }
(...)
```

<br>

REST 테스트를 할 때는 반드시 현재 데이터베이스에 존재하는 Note의 번호(num)를 이용해서 테스트를 진행한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-19-09-11.png){: p}

<br>

Note를 수정할 때는 등록과 달리 JOSN 데이터에 num 속성을 포함해서 전송한다.

<br>

**NoteController.java**

```java
(...)
    @PutMapping(value="/{num}", produces=MediaType.TEXT_PLAIN_VALUE)
    public ResponseEntity<String> modify(@RequestBody NoteDTO noteDTO){
        log.info("-----------modify-----");
        log.info(noteDTO);

        noteService.modify(noteDTO);

        return new ResponseEntity<>("modified", HttpStatus.OK);
    }
(...)
```

<br>

최종 결과가 제대로 나오는지 아래 사진으로 확인한다.

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-19-13-07.png){: p}

<br>

![](/images/SpringBoot/LearningSpringbootWithWebProject-12.1/2021-08-08-19-13-16.png){: p}
