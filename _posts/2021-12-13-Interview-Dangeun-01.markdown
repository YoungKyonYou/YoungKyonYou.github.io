---
layout: post
title: 당근페이를 향한 도전-1
date: 2021-12-13 10:00:00 0000
tags: [ElasticSearch, RDBMS, INDEX]
categories: [Interview]
description: 당근페이를 향한 도전기 1탄
---

<br><br>
_**3달만에 블로그 포스팅...**_
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

# <center>Backend Interview Questions 모음-1</center>

<br>

글을 너무 오랜만에 쓴다. 그동안 이것저것하느라 바쁘기도 했고 아무래도 취업을 준비해야 하다보니 정신이 없었다. 내가 벌써 4학년이라는 게 믿기지가 않는다. 생각보다 오랜 시간이 지난거 같은데 이 포스트를 작성하기 전 마지막 포스트가 2021년 8월 29일인 것을 보면 그다지 많이 지난 것 같지 않다. 그동안 많은 **실패 및 성공?**(실패 90%, 성공 1%, 기타9%..) 이 있었다. 되돌아보면 가슴만 아프니까 여기까지만 하자. 이제 다시 마음 잡고 일어날 때다. 항상 힘들때면 되돌아보는 대사가 하나 있다. 그래도 이전에는 여유가 생기면 PC방에 가서 **오버워치**를 하는 즐거움도 있었는데 이제는 그러지도 못할 것 같다. **오버워치**에 나오는 캐릭터 중에서 **솔져76**이 게임 도중에 하는 대사가 있다.

<br>
<br>

![](/images/Interview/post1/2021-12-13-20-44-30.png){: p}

**"쓰러뜨려 봐라. 다시 일어날테니"**

<br>

오글거릴 수도 있는 나름 간단하면서 임펙트 있어서 좋아한다.

<br>

이제 헛소리 그만하고 본론을 써야겠다. 다시 블로그 글을 쓰게 된 이유는 면접 및 CS 지식을 다지기 위해서다. 오늘부터 차근차근 하나하나 자세하게 보며 써내려 가려고 한다. 하면서 많이 힘들겠지만 천천히 가는 만큼 더 많은 것을 볼 수 있지 않을까 싶다.

<br>

이번 편에서는 그동안 당근에서 면접을 봤던 사람들의 후기를 바탕으로 작성해보려 한다. 먼저 면접을 보신 선배님들이 겪으신 문제를 하나하나 보며 그것에 대해 답을 찾아나가려 한다.

<br>

### <span style="color:#85144b; font-weight:bold">**"ElasticSearch의 키워드 검색과 RDBMS에서 %LIKE% 검색의 차이점"**</span>

<br>

<span style="background: rgb(251,243,219)">관계형 데이터베이스</span>에서 조건에 맞는 데이터를 검색할 때 주로 <span style="background: rgb(251,243,219)">SQL</span>를 사용한다.

SQL의 경우 <span style="background: rgb(251,243,219)">정확히 일치</span>하는 데이터를 검색하고 싶다면 **where ='...'**를 이용할 수 있고 해당하는 단어가 포함된 데이터를 검색하고 싶다면 **where like '%...%'**와 같은 형식으로 훌륭하게 데이터 검색이 가능하다.

**Elastic Search**와 차이가 뭘까?

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 관계형 데이터베이스와 일라스틱서치의 차이
</h3>

<br>

- 관계형 데이터베이스는 <span style="background: rgb(251,243,219)">단순 텍스트 매칭</span>에 대한 검색만을 제공함
  - MySql 최신 버전에서 <span style="background: rgb(251,243,219)">n-gram 기반</span>의 <span style="background: rgb(251,243,219)">Full-text 검색</span>을 지원하지만, <span style="background: rgb(251,243,219)">한글 검색</span>의 경우에 아직 많이 <span style="background: rgb(251,243,219)">빈약</span>한 감이 있음
- 텍스트를 <span style="background: rgb(251,243,219)">여러 단어로 변형</span>하거나 <span style="background: rgb(251,243,219)">텍스트의 특질</span>을 이용한 <span style="background: rgb(251,243,219)">동의어나 유의어</span>를 활용한 검색이 가능
- <span style="background: rgb(251,243,219)">Elastic Search</span>에서는 관계형 데이터베이스에서 불가능한 <span style="background: rgb(251,243,219)">비정형 데이터의 색인과 검색</span>이 가능
  - 이러한 특성은 빅데이터 처리에서 매우 중요하게 생각됨
- <span style="background: rgb(251,243,219)">Elastic Search</span>에서는 <span style="background: rgb(251,243,219)">형태소 분석</span>을 통한 <span style="background: rgb(251,243,219)">자연어 처리</span>가 가능
  - <span style="background: rgb(251,243,219)">Elastic Search</span>는 <span style="background: rgb(251,243,219)">다양한 형태소 분석 플러그인</span>을 제공
- <span style="background: rgb(251,243,219)">역색인 지원</span>으로 매우 빠른 검색이 가능

<br>

**[n-gram이란?](https://velog.io/@ny_/n-gram)**<br><br>
**[형태소 분석 예시](https://velog.io/@yundleyundle/ElasticSearch-Nori-%ED%98%95%ED%83%9C%EC%86%8C-%EB%B6%84%EC%84%9D%EA%B8%B0-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0)**

<br>

### RESTful API를 사용하는 Elastic Search

<br>

<span style="background: rgb(251,243,219)">관계형 DB</span>와 <span style="background: rgb(251,243,219)">Elastic Search</span>를 비교했을 때 가장 커다란 부분 중 하나는 데이터의 <span style="background: rgb(251,243,219)">CRUD</span>를 하는 방식이 조금 다른 것이다.

<span style="background: rgb(251,243,219)">관계형 DB</span>의 경우 우리가 주로 데이터의 추가, 삭제 등을 위해 사용하는 방법은 클라이언트에서 관계형 DB가 있는 서버에 연결을 맺어 <span style="background: rgb(251,243,219)">SQL</span>을 날리는 방식이었을 것이다.

이를 테면 JDBC에서 관계형 DB가 있는 아이피와 포트를 연결하여 **SELECT, INSERT, DELETE**등의 <span style="background: rgb(251,243,219)">쿼리</span>를 날리는 방식이었다.

<span style="background: rgb(251,243,219)">Elastic Search</span>의 경우에는 이와 약간 다르다. 데이터를 <span style="background: rgb(251,243,219)">CRUD</span>하기 위해서 <span style="color:#2ECC40; font-weight:bold">RESTful API</span>라는 방식을 이용한다.

<span style="background: rgb(251,243,219)">HTTP 통신</span>에서 갖는 <span style="background: rgb(251,243,219)">GET, POST, PUT, DELETE</span> 등의 메서드가 <span style="background: rgb(251,243,219)">RESTful API</span>의 형식대로 그대로 적용된다. HEAD 메소드는 친숙하진 않지만, 특정 문서의 정보 유무를 확인하는데 이용될 수 있다.

또한 <span style="background: rgb(251,243,219)">Elastic Search</span>의 POST 즉, <span style="background: rgb(251,243,219)">데이터 삽입</span>의 경우에는 관계형 데이터베이스와 약간 다른 특성을 갖고 있는데 <span style="background: rgb(251,243,219)">스키마가 미리 정의되어 있지 않더라도</span>, <span style="background: rgb(251,243,219)">자동으로 필드를 생성</span>하고 저장한다는 점이다.

이러한 특성은 <span style="background: rgb(251,243,219)">큰 유연성을 제공</span>하지만 선호되는 방법은 아니다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Elastic Search의 장점
</h3>

<br>

<span style="color:#2ECC40; font-weight:bold">데이터베이스 대용으로 사용가능</span>

<br>
 <span style="background: rgb(251,243,219)">NoSQL 데이터베이스</span>처럼 사용이 가능하다. 또한 분류가 가능하고 분산 처리를 통해 거의 <span style="background: rgb(251,243,219)">실시간(NRT-Near Real Time)에 데이터 검색</span>이 가능하다.

<br>

<span style="color:#2ECC40; font-weight:bold">대량의 비정형 데이터 보관 및 검색 가능</span>

<br>

기존 데이터베이스로 처리하기 어려운 대량의 <span style="background: rgb(251,243,219)">비정형 데이터 검색</span>이 가능하며, <span style="background: rgb(251,243,219)">전문 검색(Full-Text-Search)</span>과 <span style="background: rgb(251,243,219)">구조 검색</span> 모두를 지원한다. 기본적으로 검색엔진이지만 MongoDB나 Hbase처럼 <span style="background: rgb(251,243,219)">대용량 스토리지</span>로 사용도 가능하다.

<br>

**[일라스틱 서치의 전문검색](https://esbook.kimjmin.net/05-search/5.1-query-dsl)**<br><br>
**[정형 데이터, 비정형 데이터, 반정형 데이터](https://deep-jin.tistory.com/entry/%EC%A0%95%ED%98%95-%EB%B0%98%EC%A0%95%ED%98%95-%EB%B9%84%EC%A0%95%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0)**

<br>

<span style="color:#2ECC40; font-weight:bold">오픈소스 검색엔진</span>

<br>

<span style="background: rgb(251,243,219)">아파치 루씬(Lucene)기반 오픈소스 검색엔진</span>으로 무료로 사용 가능하며, 많은 컨트리뷰터들이 실시간으로 소스를 수정해주기 때문에 버그가 발생하면 빠르게 해결된다.

<br>

<span style="color:#2ECC40; font-weight:bold">전문 검색(Full-text Search)</span>

<br>

<span style="background: rgb(251,243,219)">내용 전체를 색인</span>하여 <span style="background: rgb(251,243,219)">특정 단어</span>가 포함된 문서를 검색하는 것이 가능하다.

<br>

<span style="color:#2ECC40; font-weight:bold">통계 분석</span>

<br>

<span style="background: rgb(251,243,219)">비정형 로그 데이터</span>를 수집하고 한 곳에 모아서 <span style="background: rgb(251,243,219)">통계 분석</span>이 가능하다. <span style="background: rgb(251,243,219)">키바나</span>를 이용하면 시각화 또한 가능하다.

<br>

<span style="color:#2ECC40; font-weight:bold">스키마리스(Schemaless)</span>

<br>

기존의 관계형 데이터베이스는 <span style="background: rgb(251,243,219)">스키마</span>라는 구조에 따라 데이터를 적합한 형태로 변경하여 저장 관리하지만 Elastic Search는 <span style="background: rgb(251,243,219)">비정형의 다양한 형태의 문서</span>도 자동으로 색인, 검색이 가능하다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

스키마란<br>
데이터베이스의 구조와 제약 조건에 관해 전반적인 명세를 기술한 것</div>

<br>

<span style="color:#2ECC40; font-weight:bold">RESTful API</span>

<br>

<span style="background: rgb(251,243,219)">RESTful API를</span> 사용하여 HTTP 통신 기반으로 요청을 받아 <span style="background: rgb(251,243,219)">JSON 형식으로 응답</span>한다는 것은 <span style="background: rgb(251,243,219)">다양한 플랫폼에서 응용</span> 가능하다는 것을 의미한다.

<br>

<span style="color:#2ECC40; font-weight:bold">멀티 테넌시(Multi-tenancy)</span>

<br>

<span style="background: rgb(251,243,219)">Elastic Search</span>에서 인덱스는 관계형 DB의 데이터베이스와 같은 개념임에도 불구하고 <span style="background: rgb(251,243,219)">서로 다른 인덱스</span>에서도 검색할 필드명만 같으면 여러 개의 인덱스를 <span style="background: rgb(251,243,219)">한번에 조회</span>할 수 있다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

ElasticSearch는 여러 개의 분리된 인덱스를 그룹으로 저장한다. 관계형 DB에서 다른 데이터베이스의 데이터를 검색하려면 별도의 커넥션을 생성해야 하는데, ElasticSearch에서는 서로 다른 인덱스의 데이터를 하나의 쿼리로 묶어서 검색하고 하나의 출력으로 모아줄 수 있다.(멀티테넌시 구조) 관계형 데이터베이스에서는 쿼리 하나만을 이용하여 각각 다른 데이터베이스에 있는 데이터를 동시에 조회하는 것은 불가능하다. 하지만 엘라스틱서치는 여러 개의 인덱스를 동시에 조회 가능핟.</div>

<br>

<span style="color:#2ECC40; font-weight:bold">Document-Oriented</span>

<br>

여러 계층의 데이터를 <span style="background: rgb(251,243,219)">JSON 형식의 구조화된 문서</span>로 <span style="background: rgb(251,243,219)">인덱스에 저장</span> 가능하다. 계층 구조로 문서도 한 번의 쿼리로 쉽게 조회 가능하다.

<br>

<span style="color:#2ECC40; font-weight:bold">역색인(Inverted-Index)</span>

<br>

<span style="background: rgb(251,243,219)">역색인</span>을 지원한다.

<br>

**[역색인](https://youngkyonyou.github.io/interview/2021/12/28/Interview-interview-14.html)**

<br>

<span style="color:#2ECC40; font-weight:bold">확장성과 가용성</span>

<br>

매우 많은 데이터가 존재할 때 <span style="background: rgb(251,243,219)">분산 시스템 구성</span>으로 <span style="background: rgb(251,243,219)">병렬적인 처리</span>가 가능하다. 분산 환경에서는 데이터가 <span style="background: rgb(251,243,219)">샤드(Shard)라는 단위</span>로 나누어 제공된다. 인덱스 생성 시마다 샤드의 수 조정이 가능하다. <span style="background: rgb(251,243,219)">데이터의 종류와 성격</span>에 따라 데이터를 분산하여 빠르게 처리 가능하다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 단점
</h3>

<br>

<span style="color:#85144b; font-weight:bold">'실시간'(Real Time) 처리는 불가능</span>

<br>

Elastic Search의 <span style="background: rgb(251,243,219)">데이터 색인의 특징</span> 때문에 Elastic Search의 색인된 데이터는 1초 뒤에나 검색이 가능하다. 왜냐하면 색인된 데이터가 내부적으로 <span style="background: rgb(251,243,219)">커밋(Commit)과 플러시(Flush)</span>와 같은 과정을 거치기 때문이다. 그래서 Elastic Search 공식 홈페이지에서도 <span style="background: rgb(251,243,219)">NRT(Near Real Time)</span>라는 표현을 쓴다.

<br>

<span style="color:#2ECC40; font-weight:bold">트랜잭션(Transactio) 롤백(Rollback) 등의 기능을 제공하지 않는다.</span>

<br>

분산 시스템 구성의 특징 때문에, 시스템적으로 비용 소모가 큰 <span style="background: rgb(251,243,219)">롤백, 트랜잭션</span>을 지원하지 않는다. 그래서 <span style="background: rgb(251,243,219)">데이터 관리에 유의</span>해야 함

<br>

일단 Elasticsearch와 관계형 DB를 비교해보자.

![](/images/Interview/post1/2021-12-13-21-30-31.png){: p}

<br>

먼저 위의 테이블에 나오는 용어를 정리해보자.

<br>

#### **Elasticsearch 아키텍쳐 / 용어정리**

<br>

![](/images/Interview/post1/2021-12-13-21-34-11.png){: p}

<br>

**1)** **클러스터(Cluster)**

- <span style="background: rgb(251,243,219)">클러스터</span>란 <span style="background: rgb(251,243,219)">Elasticsearch</span>의 가장 큰 시스템 단위를 의미하며, 최소 하나 이상의 노드로 이루어진 <span style="background: rgb(251,243,219)">노드들의 집합</span>이다. 서로 다른 클러스터는 데이터의 접근, 교환을 할 수 없는 <span style="background: rgb(251,243,219)">독립적인 시스템</span>으로 유지되며, 여러 대의 서버가 하나의 클러스터를 구성할 수 있고, 한 서버에 여러 개의 클러스터가 존재할 수도 있다.

<br>

**2)** **노드(Node)**

- <span style="background: rgb(251,243,219)">Elasticsearch</span> 를 구성하는 <span style="background: rgb(251,243,219)">하나의 단위 프로세스</span>를 의미한다. 그 역할에 따라 <span style="background: rgb(251,243,219)">Master-eligible, Data, Ingest, Tribe</span> 노드로 구분할 수 있다.

<br>

- **master-eligible node**:<span style="background: rgb(251,243,219)">클러스터를 제어</span>하는 마스터로 선택할 수 있는 노드를 말한다. 여기서 master 노드가 하는 역할은 다음과 같다

  - 인덱스 생성, 삭제
  - 클러스터 노드들의 추적, 관리
  - 데이터 입력 시 어느 샤드에 할당할 것인지

<br>

- **Data Node**: 데이터와 관련된 <span style="background: rgb(251,243,219)">CRUD 작업</span>과 관련있는 노드이다. 이 노드는 CPU, 메모리 등 자원을 많이 소모하므로 모니터링이 필요하며, master 노드와 분리하는 것이 좋다.

<br>

- **Ingest Node**: <span style="background: rgb(251,243,219)">데이터를 변환</span>하는 등 사전 처리 파이프라인을 실행하는 역할을 한다.

<br>

- **Coordination Only Node**: data node와 master-eligible node의 일을 대신하는 이 노드는 <span style="background: rgb(251,243,219)">대규모 클러스터에서 큰 이점</span>이 있다. 즉 <span style="background: rgb(251,243,219)">로드밸런서</span>와 비슷한 역할을 한다.

<br>

**3)** **인덱스(Index) / 샤드(Shard) / 복제(Replica)**

<br>

- Elasticsearch에서 <span style="background: rgb(251,243,219)">index</span>는 RDBMS에서 <span style="background: rgb(251,243,219)">database</span>와 대응하는 개념이다. 또한 <span style="background: rgb(251,243,219)">shard</span>와 <span style="background: rgb(251,243,219)">replica</span>는 Elasticsearch에만 존재하는 개념이 아니라, 분산 데이터베이스 시스템에도 존재하는 개념이다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 파티셔닝과 샤딩의 차이
</h4>

- **파티셔닝**: 하나의 데이터베이스 인스턴스에서 데이터(테이블)를 분리
- **샤딩**: 데이터를 여러 데이터베이스 인스턴스로 분할

![](/images/Interview/post16/2022-01-16-00-43-54.png?style=centerme)

<br>

- **샤딩(sharding)**은 <span style="background: rgb(251,243,219)">데이터를 분산</span>해서 저장하는 방법을 의미한다. 즉, <span style="background: rgb(251,243,219)">Elasticsearch</span>에서 스케일 아웃을 위해 <span style="background: rgb(251,243,219)">index</span>를 여러 <span style="background: rgb(251,243,219)">shard</span>로 쪼갠 것이다. 기본적으로 1개가 존재하며, 검색 성능 향상을 위해 클러스터의 샤드 갯수를 조정하는 튜닝을 하기도 한다.

<br>

- **replica**는 또 다른 형태의 <span style="background: rgb(251,243,219)">shard</span>라고 할 수 있다. 노드를 손실했을 경우 데이터의 신뢰성을 위해 <span style="background: rgb(251,243,219)">샤드들을 복제</span>하는 것이다. 따라서 replica는 서로 다른 노드에 존재할 것을 권장한다. 아래 사진에서 보는 바와 같이 Replica1은 Node2에 존재하는 것을 확인할 수 있다.

<br>

![](/images/Interview/post1/2021-12-13-22-05-57.png?style=centerme)

<br>

**4)** **Elasticsearch의 특징**

<br>

- **Scale out**

  - <span style="background: rgb(251,243,219)">샤드</span>를 통해 규모가 수평적으로 늘어날 수 있음

<br>

- **고가용성**

  - <span style="background: rgb(251,243,219)">Replica</span>를 통해 데이터의 안정성을 보장

<br>

- **Schema Free**

  - Json 문서를 통해 데이터 검색을 수행하므로 <span style="background: rgb(251,243,219)">스키마 개념이 없음</span>

- **Restful**

  - 데이터 <span style="background: rgb(251,243,219)">CRUD 작업</span>은 <span style="background: rgb(251,243,219)">HTTP Restful API</span>를 통해 수행하며 각각 다음과 같이 대응한다.

<br>

![](/images/Interview/post1/2021-12-13-22-13-42.png?style=centerme)

<br>
