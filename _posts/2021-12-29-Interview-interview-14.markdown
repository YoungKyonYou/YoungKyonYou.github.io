---
layout: post
title: 역색인-Inverted Index
date: 2021-12-28 10:00:00 0000
tags: [Inverted Index]
categories: [Interview]
description: Inverted Index란?
---

<br><br>

_**오늘의 나보다 성장한 내일의 나를 위해...**_

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

<br>

## 역색인

<br>

**역색인:** 하나의 값(term)이 들어간 문서번호를 지정하는 것

<br>

데이터 시스템에 다음과 같은 문서들을 저장한다고 가정 해 보자.

<br>

![](/images/Interview/post16/2021-12-29-20-18-55.png?style=centerme)

<br>

일반적으로 오라클이나 MySQL 같은 관계형 DB에서는 위 내용을 보이는 대로 테이블 구조로 저장을 한다. 만약에 위 테이블에서 Text에 **fox**가 포함된 행들을 가져온다고 하면 다음과 같이 Text 열을 한 줄씩 찾아 내려가면서 fox가 있으면 가져오고 없으면 넘어가는 식으로 데이터를 가져 올 것이다.

<br>

![](/images/Interview/post16/2021-12-29-20-20-18.png?style=centerme)

<br>

전통적인 RDBMS에서는 위와 같이 **like** 검색을 사용하기 때문에 데이터가 늘어날수록 검색해야 할 대상이 늘어나 시간도 오래 걸리고, row 안의 내용을 모두 읽어야 하기 때문에 기본적으로 <span style="background: rgb(251,243,219)">속도가 느리다</span>. <span style="background: rgb(251,243,219)">Elastic Search</span>는 데이터를 저장할 때 다음과 같이 **역 인덱스(inverted index)**라는 구조를 만들어 저장한다.

<br>

![](/images/Interview/post16/2021-12-29-20-21-24.png?style=centerme)

<br>

이 <span style="background: rgb(251,243,219)">역인덱스</span>는 **책에 맨 뒤에 있는** 주요 키워드에 대한 내용이 몇 페이지에 있는지 볼 수 있는 **찾아보기 페이지**에 비유할 수 있다. <span style="background: rgb(251,243,219)">Elasticsearch</span>에서는 추출된 각 키워드를 **텀(term)**이라고 부른다. 이렇게 <span style="background: rgb(251,243,219)">역인덱스</span>가 있으면 **fox**를 포함하고 있는 document의 **id**를 바로 얻어올 수 있다.

<br>

![](/images/Interview/post16/2021-12-29-20-22-33.png?style=centerme)

<br>

<span style="background: rgb(251,243,219)">Elasticsearch</span>는 데이터가 늘어나도 찾아가야 할 행이 늘어나는 것이 아니라 <span style="background: rgb(251,243,219)">역인덱스</span>가 가리키는 <span style="background: rgb(251,243,219)">id</span>의 배열값이 추가되는 것 뿐이기 때문에 큰 속도의 저하 없이 <span style="background: rgb(251,243,219)">빠른 속도</span>로 검색이 가능하다. 이런 <span style="background: rgb(251,243,219)">역인덱스</span>를 데이터가 저장되는 과정에서 만들기 때문에 <span style="background: rgb(251,243,219)">Elasticsearch</span>는 데이터를 입력할 때 저장이 아닌 **색인**을 한다고 표현한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 기존의 전톡적인 검색 방식
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 1. WHERE 검색방식
</h4>

```sql
SELECT * FROM 'M_DOCUMENT' WHERE 'bookname' = 'Buying a Home'
```

<br>

위 경우 <span style="background: rgb(251,243,219)">검색어</span>와 정확히 일치하는 문서만 선택된다. 즉, **문서 결과**를 거의 얻지 못한다. 그리고 선택되는 문서 수 자체가 거의 없다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

LIKE는 대소문자를 구분하여 검색하기 때문에, 대소문자 구분 없이 검색하기 위해서는 UPPER, LOWER 함수를 사용하여 컬럼의 값을 치환후 검색 해야 한다.</div>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 2.  WHERE LIKE 검색 방식
</h4>

<br>

```sql
SELECT * FROM `M_DOCUMENT` WHERE `bookname` LIKE '%Buying a Home%'
```

<br>

이 경우 검색어가 문서내용(bookname 필드)에 포함되어 있는 경우 선택이 된다.
1번 방식보다 진화한 방식이지만 여전히 **해당 문장이 정확히 일치**하는 경우가 적기 때문에 결과를 거의 얻지 못한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 3. Whitespace tokenizer AND 검색방식
</h4>

사용자의 쿼리를 <span style="background: rgb(251,243,219)"> 4. Whitespace</span>로 쪼개서 <span style="background: rgb(251,243,219)">AND</span> 검색을 실시한다.

<br>

```sql
SELECT * FROM `M_DOCUMENT` WHERE `bookname`
LIKE '%Buying%' AND `bookname` LIKE '%a%' AND `bookname` LIKE '%HOME%'
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 4. Whitespace tokenizer OR 검색방식
</h4>

사용자의 쿼리를 Whitespace로 쪼개서 OR 검색을 실시한다.

<br>

```sql
SELECT * FROM `M_DOCUMENT` WHERE `bookname`
LIKE '%Buying%' OR `bookname` LIKE '%a%' AND `bookname` LIKE '%HOME%'
```

<br>

문서내용(bookname 필드)에 사용자 검색어 중 하나라도 포함되는 경우를 찾는다. 사용자가 원하는 문서를 찾아준다는 점에서 매우 우수한 검색방식이다. 하지만 어느 하나의 단어만 포함되도 되기에 전혀 관계가 없는 문서도 결과물(result-set)로 추출된다.

<br>

---

<br>

전통적인 검색방식의 가장 큰 문제점은 전체 글의 <span style="background: rgb(251,243,219)">content 필드를</span> 모두 읽어들여서 검색어의 <span style="background: rgb(251,243,219)">포함여부</span>를 확인한다는 것이다.

따라서 결과를 얻기까지 많은 <span style="background: rgb(251,243,219)">노력과 시간</span>이 필요하게 된다.

이것은 <span style="background: rgb(251,243,219)">인덱싱이</span> 되지 않는다고 하는데 위의 DB 쿼리 구문은 모든 글에 대해서 <span style="background: rgb(251,243,219)">'content'</span> 항목값을 읽은 후에 찾아야하고 **이보다 더 나은 방법은 없다는 뜻**이다.

<br>

**4번의 방식**은 현재 한국 내 커뮤니티에서 가장 많이 사용하고 있는 <span style="background: rgb(251,243,219)">검색방식</span>이다.

따라서 국내 커뮤니티 검색엔진에서 좋은 결과를 얻고자 한다면 <span style="background: rgb(251,243,219)">키워드 입력방식</span>을 사용해야 한다.

예를 들어 <span style="background: rgb(251,243,219)">"집을 살때 필요한 서류"</span>를 검색하고 싶으면 <span style="background: rgb(251,243,219)">"집 서류"</span> 라고 검색해야 가장 훌륭한 결과물을 얻어낼 수 있다.

<br>

```sql
SELECT * FROM `M_DOCUMENT` WHERE `bookname` LIKE ‘%집%’ OR `bookname` LIKE ‘%서류%’
```

<br>

**4번이 정말 좋은 방식**이긴한데 <span style="background: rgb(251,243,219)">몇 가지 단점</span>이 있다.

- 의미없는 결과 값도 나온다.
- 검색 대상이 누적되면서(100만개 정도의 big data가 되면서) 검색부하가 엄청 오래 걸림

<br>

예를 들어 **4번과** 같은 쿼리를 <span style="background: rgb(251,243,219)">100만개</span> 정도의 big data라고 했을 때 검색을 진행하면 검색부하가 엄청 오래 걸린다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 역색인의 장점
</h3>

<br>

앞서 간단하게 역색인과 기존의 전통적인 검색 방식에 대해서 살펴보았다. 역색인을 지원하는 일라스틱 서치에 대해 좀 더 알아보자.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Inverted Index
</h4>

기존의 데이터베이스가 하나의 <span style="background: rgb(251,243,219)">구분자(Primary Key)</span>가 여러 필드를 지정하고 있었다면
<span style="background: rgb(251,243,219)">Inverted Index</span>에서는 <span style="background: rgb(251,243,219)">하나의 값(Term)</span>이 해당 <span style="background: rgb(251,243,219)">Term</span>이 들어간 <span style="background: rgb(251,243,219)">document id</span> 를 지정하고 있습니다.

<br>

![](/images/Interview/post16/2022-01-08-17-29-32.png?style=centerme)

<br>

1~9 document 데이터를 분석해서 테이블을 구성한다. 오른쪽 inverted index table을 보면, <span style="background: rgb(251,243,219)">becoming home</span>이라고 검색하면 <span style="background: rgb(251,243,219)">becoming</span>과 <span style="background: rgb(251,243,219)">home</span>으로 나눈 후에 빠르게 <span style="background: rgb(251,243,219)">(8), (2,5,7,8)</span>이라는 결과가 반환이 되고 **8이 가장 유사한 결과물**이라고 알게 된다.

**인덱싱을 하기 때문에** 탐색 속도가 매우 빠르다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Inverted Index with Term Position
</h4>

이 기능은 검색 결과를 향상시키기 위한 것이다.

단어 값(Term)이 추가 정보를 지정할 수 있게 된다. 여기서는 위치정보를 말한다.

<br>

![](/images/Interview/post16/2022-01-08-17-31-20.png?style=centerme)

<br>

예시로 사용자가 <span style="background: rgb(251,243,219)">new home</span>을 검색했다고 가정하면 위의 그림에 따라 <span style="background: rgb(251,243,219)">5번과 8번 document</span>를 반환하게 된다. <span style="background: rgb(251,243,219)">5번과 8번이</span> 두 단어를 모두 포함하는 document 일뿐 아니라, <span style="background: rgb(251,243,219)">new 다음에 home</span>이 나타나는 문서임을 알 수 있다. (Term position 순서 비교)

단어가 <span style="background: rgb(251,243,219)">연속되는지</span> (new home) 여부를 빠르게 파악이 가능하고 <span style="background: rgb(251,243,219)">단어(Term)</span> 사이의 값을 찾을 수도 있다. 이것을 활용해 <span style="color:#7EDBFF; font-weight:bold">new home</span>, <span style="color:#7EDBFF; font-weight:bold">new</span> <span style="color:#2ECC40; font-weight:bold">brand</span> <span style="color:#7EDBFF; font-weight:bold">home</span>, <span style="color:#7EDBFF; font-weight:bold">new</span> <span style="color:#2ECC40; font-weight:bold">super cheap</span> <span style="color:#7EDBFF; font-weight:bold">home</span> 등이 결과에 나올 수 있게 된다.(Proximity Search)

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

문서내용(bookname 필드)에 사용자 검색어의 모든 단어가 포함된 경우를 찾는다. 이전 방식과 비교해서 상당히 많이 향상된 결과를 보여주지만 <span style="background: rgb(251,243,219)">해당 단어가 모두 포함된</span> 문서가 아니면 결과에 포함되지 않는다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Whitespace tokenizer OR 검색방식
</h4>

```sql
SELECT * FROM `M_DOCUMENT` WHERE `bookname`
LIKE '%Buying%' OR `bookname` LIKE '%a%' AND `bookname` LIKE '%HOME%'
```

<br>

문서내용(bookname 필드)에 사용자 검색어 중 하나라도 포함되는 경우를 찾는다. 사용자가 원하는 문서를 찾아준다는 점에서 매우 우수한 검색방식이다. 하지만 <span style="background: rgb(251,243,219)">어느 하나의 단어만</span> 포함되도 되기에 전혀 관계가 없는 문서도 결과물로 추출된다.

<br>

Traditional SQL에서 <span style="background: rgb(251,243,219)">LIKE</span> 검색이 <span style="background: rgb(251,243,219)">INDEX</span> 기능을 이용할 수 없다는 단점이 있어서, 그 문제를 극복하기 위해서 <span style="background: rgb(251,243,219)">단어(Term)</span>로 <span style="background: rgb(251,243,219)">인덱싱</span>을 하는 <span style="background: rgb(251,243,219)">Inverted Index</span> 방식이 고안되었다.

<br>

기존의 데이터베이스가 하나의 <span style="background: rgb(251,243,219)">구분자(Primary Key)</span>가 여러 필드를 지정하고 있었다면 <span style="background: rgb(251,243,219)">Inverted Index</span>에서는 하나의 값(Term)이 해당 Term이 들어간 document id를 지정한다.

<br>

만약 DB에서 <span style="background: rgb(251,243,219)">"Trade"</span>라는 문구가 포함된 문자열을 찾으려고 한다면 SQL에서는 <span style="background: rgb(251,243,219)">%Trade%</span>라고 명확히 입력해야 검색이 가능하다.

<span style="background: rgb(251,243,219)">trade, TRADE, trAde...</span>등의 문자열은 <span style="background: rgb(251,243,219)">하나하나</span> 명시하기 전에는 찾을 수 없다. <span style="background: rgb(251,243,219)">역색인</span>을 활용하면 대소문자 구분 없이 어떤 문구가 들어와도 찾을 수 있음

<br>

- **RDB**는 행을 기반으로 데이터를 저장 그에 반해 **엘라스틱서치**는 단어를 기반으로(역인덱스) 저장한다.
- **RDB**는 데이터 **수정, 삭제**의 편의성과 속도 면에서 강점이 있지만 **다양한 조건**의 데이터를 검색하고 **집계**하는 데에는 구조적인 **한계**가 있다
  - document 개수만큼 특정 단어가 있는지 확인을 반복해야 하기 때문에 많은 수의 document가 있을 경우 비효율적이다.
- 반면 **일라스틱서치**는 특정 단어가 어디에 저장되어 있는지 이미 알고 있어 모든 document를 검색할 필요는 없다.
  - 다만 **수정과 삭제**는 엘라스틱서치 내부적으로 굉장히 많은 리소스가 소요된다.
