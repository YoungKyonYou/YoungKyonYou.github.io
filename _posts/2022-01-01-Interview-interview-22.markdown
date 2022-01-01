---
layout: post
title: Clustered Index vs Non-Clustered Index
date: 2022-01-01 14:00:00 0000
tags: [Clustered Index, Non-Clustered Index]
categories: [Interview]
description: 클러스터 인덱스와 넌 클러스터 인덱스의 차이
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

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Clustered Index vs Non-Clustered Index
</h2>

<br>

이번에는 인덱스의 종류인 클러스터 인덱스와 넌 클러스터 인덱스에 대해서 알아보자.

일단 인덱스란 데이터를 빠르게 검색할 수 있게 해주는 객체이다.

컬럼을 정렬한 후에 데이터를 빠르게 찾을 수 있도록 도와주는 역할을 한다.

인덱스를 생성한다고 무조건 데이터를 빠르게 검색할 수 있는 것은 아니다.

인덱스를 무작정 생성하는 것은 좋은 방법이 아닌 것이다.

중요한 것은 인덱스를 생성할 때 <span style="background: rgb(251,243,219)">테이블의 용도</span>를 정확하게 파악하는 것이다.

용도에 따라서 적절한 컬럼으로 **Clustered Index와 Non-Clustered Index**를 구성해야 한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 클러스터 인덱스
</h3>

<br>

클러스터 인덱스는 데이터페이지 자체가 인덱스 키 값에 의해 물리적으로 정렬이 된다.

**즉, 데이터페이지는** <span style="background: rgb(251,243,219)">리프 레벨</span>이라고 볼 수 있다.

아래와 같은 SQL를 실행해서 **클러스터 인덱스를 구성해보자**

<br>

```sql
USE tempdb
CREATE TABLE clusterExTable (id int NOT NULL,value nvarchar(20) NOT NULL);

INSERT INTO clusterExTable VALUES (1,'indexTest1');
INSERT INTO clusterExTable VALUES (15,'indexTest15');
INSERT INTO clusterExTable VALUES (7,'indexTest7');
INSERT INTO clusterExTable VALUES (8,'indexTest8');
INSERT INTO clusterExTable VALUES (4,'indexTest4');
INSERT INTO clusterExTable VALUES (2,'indexTest2');
INSERT INTO clusterExTable VALUES (3,'indexTest3');
INSERT INTO clusterExTable VALUES (11,'indexTest7');
INSERT INTO clusterExTable VALUES (9,'indexTest8');
INSERT INTO clusterExTable VALUES (14,'indexTest14');
INSERT INTO clusterExTable VALUES (5,'indexTest5');
INSERT INTO clusterExTable VALUES (10,'indexTes10');
INSERT INTO clusterExTable VALUES (13,'indexTest13');
INSERT INTO clusterExTable VALUES (6,'indexTest6');
INSERT INTO clusterExTable VALUES (12,'indexTest12');

ALTER TABLE clusterExTable ADD CONSTRINT PK_clusterExTable_id PRIMARY KEY(id);

```

<br>

클러스터형 인덱스를 구성하려면 행 데이터를 해당 열로 정렬한 후에 루트 페이지를 만들게 된다. 즉 **데이터 페이지**는 **리프 노드**와 같은 것을 확인할 수 있다.

<br>

![](/images/Interview/post16/2022-01-01-20-48-44.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

<br>

- 테이블 당 1개만 허용
- 기본 키 설정시 자동으로 만들어짐
- 테이블 자체가 인덱스 (클러스터 인덱스를 기준으로 테이블을 정렬하기 때문에 인덱스 페이지가 없다)
- 데이터 입력, 수정, 삭제 시 항상 정렬을 유지함
- 기본적으로 접근 성능이 좋음

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 넌클러스터 인덱스
</h3>

<br>

넌 클러스트형 인덱스는 **데이터 페이지**를 건들지 않고, 별도의 장소에 **인덱스 페이지**를 생성한다.

우선 **인덱스 페이지**의 **리프 페이지**에 인덱스로 구성한 열을 정렬하고 데이터 위치 포인터를 생성한다.

데이터의 위치 포인트는 클러스터형 인덱스와 달리 <span style="background: rgb(251,243,219)">'페이지 번호 + #오프셋'</span>이 기록되어 바로 데이터 위치를 가리킨다.

아래 그림을 예시로 들어보자.

**indexTest2**로 보자면 102번 페이지의 두 번째(#2)에 데이터가 있다고 기록하게 된다.

그러므로 이 데이터 위치 포인터는 데이터가 위치한 고유한 값이 된다.

<br>

![](/images/Interview/post16/2022-01-01-20-51-29.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 특징
</h4>

<br>

- 테이블 당 최대 240개 생성 가능
- 인덱스 페이지를 별도로 저장
- 테이블 자체는 정렬되지 않고, 인덱스 페이지에만 정렬
- 성능 증가는 정말 "Case By Case"

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 활용
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 클러스터 인덱스
</h4>

쿼리를 기준으로 예를 들어보자

<br>

```sql
SELECT year(hire_date), count(*)
FROM employees
WHERE hire_date >= '1997-01-01'
GROUP BY year(hire_date);
```

<br>

조건절에 <span style="background: rgb(251,243,219)">hire_date</span>가 있고, 범위 탐색이다. 이 경우 <span style="background: rgb(251,243,219)">hire_date</span>에 클러스터 인덱스를 적용하면 성능이 엄청나게 향상된다.

여기서 WHERE 절만 빼보자.

<br>

```sql
SELECT year(hire_date), count(*)
FROM employees
GROUP BY year(hire_date);
```

<br>

여기서도 마찬가지로 <span style="background: rgb(251,243,219)">hire_date</span>에 클러스터 인덱스를 건다면 어떻게 될까?

성능 향상에 도움이 안되거나, 데이터가 많아지는 경우 오히려 느려진다.

스캔 방식을 생각해야 한다.

클러스터 인덱스가 없는 경우 기본적으로 Heap 테이블 스캔이 이루어진다.

클러스터 인덱스가 있는 경우에는 클러스터 인덱스 스캔이 이루어진다.

하지만 조건절이 없으므로 무식하게 다 읽는건 Heap 테이블 스캔이 빠르다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 넌클러스터 인덱스
</h4>

<br>

위의 예시와 같은 쿼리이다.

<br>

```sql
SELECT year(hire_date), count(*)
FROM employees
WHERE hire_date >= '1997-01-01'
GROUP BY year(hire_date);
```

<br>

여기서 <span style="background: rgb(251,243,219)">hire_date</span>에 넌클러스터 인덱스를 건다면 어떻게 될까?

놀랍게도 클러스터 인덱스를 걸었을 때보다 더 빠르다.

그 이유는 넌클러스터 인덱스가 탐색 범위에 포함되었기 때문에 옵티마이저에서는 인덱스 스캔이 아닌 **Non-Clustered Index Seek** 방식을 선택하기 때문이다.

Index Scan은 인덱스의 모든 행을 인덱스 순서로 읽는 반면에 Index Seek은 필터 기준에 따라 일치하는 행이나 한정된 행만 찾으려고 리프 노드를 거치기 때문에 논리적 읽기 수가 훨씬 감소한다

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

Index Seek는 B-Tree 구조상의 Root 페이지부터 Leaf Level까지 검색 경로를 따라 수행되는 방법. Leaf Level을 제외한 상위 각 레벨에서 1페이지씩을 검색하게 된다.<br><br>

Index Scan은 Leaf Level의 첫번째 페이지부터 데이터 검색을 수행하는 방법. 일반적으로 얘기하는 Table Scan과 동일한 방법이지만, 그 대상이 Leaf Level의 인덱스 페이지라는 것이다.

</div>

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 정리
</h3>

<br>

![](/images/Interview/post16/2022-01-01-21-20-10.png?style=centerme)

<br>

여기서 물리적으로 행을 재배열한다는 것을 알아보자

<br>

아래와 같은 SQL이 있다.

<br>

```sql
CREATE TABLE TBL_CLUSTERED_TEST (
  LOG_DATE CHAR(8) NOT NULL,
  MEDIA_ID CHAR(1) NOT NULL,
  PROCEEDS DOUBLE DEFAULT NULL,
  PRIMARY KEY (LOG_DATE,MEDIA_ID)
) ENGINE=INNODB DEFAULT CHARSET=utf8;
```

<br>

5개의 테스트 데이터를 저장해 본다.

<br>

```sql
INSERT INTO TBL_CLUSTERED_TEST (LOG_DATE, MEDIA_ID, PROCEEDS) VALUES ('20130618', 'A', 1000);
INSERT INTO TBL_CLUSTERED_TEST (LOG_DATE, MEDIA_ID, PROCEEDS) VALUES ('20130619', 'A', 1000);
INSERT INTO TBL_CLUSTERED_TEST (LOG_DATE, MEDIA_ID, PROCEEDS) VALUES ('20130619', 'C', 2000);
INSERT INTO TBL_CLUSTERED_TEST (LOG_DATE, MEDIA_ID, PROCEEDS) VALUES ('20130619', 'B', 1000);
INSERT INTO TBL_CLUSTERED_TEST (LOG_DATE, MEDIA_ID, PROCEEDS) VALUES ('20130613', 'B', 3000);
```

<br>

해당 테이블을 select 하면 insert 되어 있는 순서대로 데이터가 누적되어 있을까?

아니다. **LOG_DATE, MEDIA_ID**는 클러스터드 인덱스로 생성이 되어 있기 때문에 물리적으로 **LOG_DATE**를 정렬한 후 **MEDIA_ID**를 정렬하게 된다.

물리적으로 정렬을 한다는 말은 이를 두고 하는 말이다. 실제 DB의 데이터파일에 정렬이 되어 있는 상태로 디스크에 저장이 된다는 것이다.

테이블 조회를 해보면 아래와 같이 데이터가 정렬되어 있는 것을 확인할 수 있다. (6월 13일 데이터가 가장 위에 있음)

<br>

```
mysql> select * from tbl_clustered_test;

+----------+----------+----------+

| LOG_DATE | MEDIA_ID | PROCEEDS |

+----------+----------+----------+

| 20130613 | B        |     3000 |

| 20130618 | A        |     1000 |

| 20130619 | A        |     1000 |

| 20130619 | B        |     1000 |

| 20130619 | C        |     2000 |

+----------+----------+----------+
```

<br>

그럼 <span style="background: rgb(251,243,219)">넌 클러스터드 인덱스는?</span>

일반적으로 조회문 성능 향상을 위해서 넌 클러스터드 인덱스를 생성하여 사용하곤 한다.

허나, 이 인덱스는 클러스터드인덱스와는 다르게 물리적으로 데이터가 정렬되어 저장되지 않는다.

<br>

![](/images/Interview/post16/2022-01-01-21-24-18.png?style=centerme)

<br>

위 사진의 넌클러스터 인덱스에서 데이터 페이지에 있는 데이터들은 정렬이 되지 않은 상태인 것을 볼 수 있다.
