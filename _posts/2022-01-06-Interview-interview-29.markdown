---
layout: post
title: N+1 문제와 해결 방법
date: 2022-01-06 11:20:00 0000
tags: [N+1, JPA]
categories: [Interview]
description: JPQL를 사용하면 나타나는 N+1 문제
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> N+1
</h2>

<br>

<span style="background: rgb(251,243,219)">연관관계</span>에서 발생하는 이슈로 <span style="background: rgb(251,243,219)">연관관계</span>가 설정된 <span style="background: rgb(251,243,219)">엔티티</span>를 <span style="background: rgb(251,243,219)">조회</span>할 경우에 조회된 <span style="background: rgb(251,243,219)">데이터 개수(N)</span>만큼 연관관계의 조회 쿼리가 <span style="background: rgb(251,243,219)">추가</span>로 발생하여 데이터를 읽어오게 된다. 이를 <span style="background: rgb(251,243,219)">N+1</span> 문제라고 한다.

<br>

JPA로 애플리케이션을 개발할 때 <span style="background: rgb(251,243,219)">성능상</span> 가장 주의해야 하는 것이 <span style="background: rgb(251,243,219)">N+1</span> 문제이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> N+1 예제
</h3>

<br>

**Member.java**

```java
@Entity
public class Member{

  @Id
  @GeneratedValue
  private Long id;

  @OneToMany(mappedBy= "member", fetch = FetchType.EAGER)
  private List<Order> orders=new ArrayLuist<Order>();
  (...)
}
```

<br>

**Order.java**

```java
@Entity
@Table(name = "ORDERS")
public class Order{

  @Id
  @GeneratedValue
  private Long id;

  @ManyToOne
  private Member member;
  (...)
}
```

<br>

위 코드는 <span style="background: rgb(251,243,219)">1:N, N:1</span> 양방향 연관관계이다. 그리고 회원이 참조하는 주문정보인 <span style="background: rgb(251,243,219)">Member.orders</span>를 <span style="background: rgb(251,243,219)">즉시 로딩(EAGER)</span>으로 설정했다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 즉시 로딩과 N+1
</h4>

특정 회원 하나를 **em.find()** 메서드로 조회하면 <span style="background: rgb(251,243,219)">즉시 로딩(EAGER)</span>으로 설정한 주문정보도 함께 조회한다.

```java
em.find(Member.class, id)
```

<br>

실행된 SQL은 다음과 같다.

<br>

```sql
SELECT M.*, O.*
FROM
  MEMBER M
OUTER JOIN ORDERS O ON M.ID=O.MEMBER_ID
```

<br>

여기서 함께 조회하는 방법이 주요한데 SQL을 두 번 실행하는 것이 아니라 <span style="background: rgb(251,243,219)">조인을 사용해서 한 번의</span> SQL로 회원과 주문정보를 함께 조회한다. 여기까지만 보면 <span style="background: rgb(251,243,219)">즉시 로딩</span>이 상당히 좋아보인다.

<br>

**문제는 JPQL**을 사용할 때 발생한다.

다음 코드를 보자.

<br>

```java
List<Member> members=em.createQuery("select m from Member m", Member.class).getResultList();
```

<br>

<span style="background: rgb(251,243,219)">JPQL</span>을 실행하면 JPA는 이것을 분석해서 SQL을 생성한다.

이때는 <span style="background: rgb(251,243,219)">즉시 로딩</span>과 <span style="background: rgb(251,243,219)">지연 로딩</span>에 대해서 전혀 신경 쓰지 않고 JPQL만 사용해서 SQL을 생성한다. 따라서 다음과 같은 SQL이 실행된다.

<br>

```sql
SELECT * FROM MEMBER
```

<br>

SQL의 실행 결과로 먼저 <span style="background: rgb(251,243,219)">회원 엔티티</span>를 애플리케이션에 로딩한다. 그런데 <span style="background: rgb(251,243,219)">회원 엔티티와 연관된 주문 컬렉션</span>이 <span style="background: rgb(251,243,219)">즉시 로딩</span>으로 설정되어 있으므로 JPA는 주문 컬렉션을 <span style="background: rgb(251,243,219)">즉시 로딩</span>하려고 다음 SQL을 추가로 실행한다.

<br>

```sql
SELECT * FROM ORDERS WHERE MEMBER_ID=?
```

<br>

조회된 회원이 하나면 이렇게 총 2번의 SQL을 실행하지만 조회된 회원이 <span style="background: rgb(251,243,219)">5명이면</span> 어떻게 될까?

<br>

```sql
SELECT * FROM MEMBER //1번 실행으로 회원 5명 조회
SELECT * FROM ORDERS WHERE MEMBER_ID=1 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBER_ID=2 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBER_ID=3 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBER_ID=4 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBER_ID=5 //회원과 연관된 주문
```

<br>

먼저 회원 조회 SQL로 <span style="background: rgb(251,243,219)">5명의 회원 엔티티</span>를 조회했다.(SELECT \* FROM MEMBER)

그리고 조회한 각각의 회원 엔티티와 연관된 주문 컬렉션을 즉시 조회하려고 <span style="background: rgb(251,243,219)">총 5번의</span> SQL을 추가로 실행했다. 이처럼 처음 실행한 SQL의 결과 수만큼(회원이 5명이니까 SELECT \* FROM ORDERS WHERE MEMBER_ID가 각각 5명에 대응되게 5번 호출되는 것) 추가로 SQL을 실행하는 것을 <span style="background: rgb(251,243,219)">N+1</span> 문제라 한다.

<br>

그렇다면 **즉시 로딩**이 JPQL을 실행할 때 <span style="background: rgb(251,243,219)">N+1</span> 문제를 야기할까?

<br>

**그렇지 않다!** Lazy로 설정해도 <span style="background: rgb(251,243,219)">N+1</span> 문제가 발생할 수 있다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20">지연 로딩과 N+1
</h4>

회원과 주문을 <span style="background: rgb(251,243,219)">지연 로딩(Lazy)</span>로 설정하면 어떻게 될까? 방금 살펴본 즉시 로딩 시나리오를 <span style="background: rgb(251,243,219)">지연 로딩</span>으로 변경해도 <span style="background: rgb(251,243,219)">N+1</span> 문제에서 **자유로울 수는 없다**

위 코드에서 EAGER 방식을 LAZY 방식으로 바꿔보자.

<br>

**Member.java**

```java
@Entity
public class Member{

  @Id
  @GeneratedValue
  private Long id;

  @OneToMany(mappedBy= "member", fetch = FetchType.LAZY)
  private List<Order> orders=new ArrayLuist<Order>();
  (...)
}
```

<br>

<span style="background: rgb(251,243,219)">지연 로딩</span>으로 설정하면 JPQL에서는 **N+1** 문제가 발생하지 않는다.

<br>

```java
List<Member> members=em.createQuery("select m from Member m", Member.class).getResultList();
```

<br>

지연 로딩이므로 데이터베이스에서 회원만 조회된다. 따라서 다음 SQL만 실행되고 연관된 주문 컬렉션은 <span style="background: rgb(251,243,219)">지연 로딩</span>된다.

<br>

```sql
SELECT * FROM MEMBER
```

<br>

이후 비즈니스 로직에서 주문 컬렉션을 실제 사용할 때 <span style="background: rgb(251,243,219)">지연 로딩이 발생한다.</span>

<br>

```java
firstMember=members.get(0);
firstMember.getOrders.size(); //지연 로딩 초기화
```

<br>

members.get(0)로 회원 하나만 조회해서 사용했기 때문에 firstMember.getOrders().size()를 호출하면서 실행되는 SQL은 다음과 같다.

<br>

```sql
SELECT * FROM ORDERS WHERE MEMBER_ID=?
```

<br>

문제는 다음처럼 모든 회원에 대해 연관된 주문 컬렉션을 사용할 때 발생한다.

<br>

```java
for(Member member:members){
  //지연 로딩 초기화
  System.out.println("member="+member.getOrders().size());
}
```

<br>

주문 컬렉션을 <span style="background: rgb(251,243,219)">초기화하는</span> 수만큼 다음 SQL이 실행될 수 있다. 회원이 <span style="background: rgb(251,243,219)">5명이면</span> 회원에 따른 주문도 <span style="background: rgb(251,243,219)">5번</span> 조회된다.

<br>

```sql
SELECT * FROM ORDERS WHERE MEMBERS_ID=1 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBERS_ID=2 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBERS_ID=3 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBERS_ID=4 //회원과 연관된 주문
SELECT * FROM ORDERS WHERE MEMBERS_ID=5 //회원과 연관된 주문
```

<br>

이것도 결국 N+1 문제다. 지금까지 살펴본 것처럼 N+1 문제는 <span style="background: rgb(251,243,219)">즉시 로딩</span>과 <span style="background: rgb(251,243,219)">지연 로딩</span>일 때 모두 발생할 수 있다.

<br>

**이제부터 N+1 문제를 피할 수 있는 다양한 방법을 알아보자**

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 해결 방법
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 페치 조인 사용
</h4>

<span style="background: rgb(251,243,219)">N+1</span> 문제를 해결하는 가장 일반적인 방법은 <span style="background: rgb(251,243,219)">페치 조인</span>을 사용하는 것이다. <span style="background: rgb(251,243,219)">페치 조인</span>은 SQL 조인을 사용해서 연관된 엔티티를 함께 조회하므로 <span style="background: rgb(251,243,219)">N+1</span> 문제가 발생하지 않는다.

<br>

<span style="background: rgb(251,243,219)">페치 조인</span>을 사용하는 JPQL을 보자.

<br>

```java
select m from Member m join fetch m.orders
```

<br>

실행된 SQL은 다음과 같다.

<br>

```sql
SELECT M.*, O.* FROM MEMBER M INNER JOIN ORDERS O ON M.ID=O.MEMBER_ID
```

<br>

참고로 이 예제는 <span style="background: rgb(251,243,219)">일대다 조인</span>을 했으므로 결과가 늘어나서 중복된 결과가 나타날 수 있다. 따라서 JPQL의 <span style="background: rgb(251,243,219)">DISTINCT</span>를 사용해서 <span style="background: rgb(251,243,219)">중복</span>을 제거하는 것이 좋다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 하이버네이트 @BatchSize
</h4>

하이버네이트가 제공하는 <span style="background: rgb(251,243,219)">org.hibernate.annotations.BatchSize</span> 어노테이션을 사용하면 연관된 엔티티를 조회할 때 지정한 size만큼 SQL의 IN 절을 사용해서 조회한다. 만약 조회한 회원이 10명인데 size=5로 지정하면 2번의 SQL만 추가로 실행한다.

<br>

**Member.java(BatchSize 적용)**

```java
@Entity
public class Member{
  ...
  @org.hibernate.annotations.BatchSize(size=5)
  @OneToMay(mappedBy="member", fetch=FetchType.EAGER)
  private List<Order> orders=new ArrayList<Order>();
  ...
}
```

<br>

<span style="background: rgb(251,243,219)">즉시 로딩</span>으로 설정하면 조회 시점에 10건의 데이터를 모두 조회해야 하므로 다음 SQL이 두 번 실행된다. <span style="background: rgb(251,243,219)">지연 로딩으로</span>설정하면 지연 로딩된 엔티티를 최초 사용하는 시점에 다음 SQL을 실행해서 <span style="background: rgb(251,243,219)">5건의</span> 데이터를 미리 로딩해둔다. 그리고 6번 째 데이터를 사용하면 다음 SQL을 추가로 실행한다.

<br>

```sql
SELECT * FROM ORDERS WHERE MEMBER_ID IN (?, ?, ?, ?, ?)
```

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

참고<br>

hibernate.default_batch_fetch_size 속성을 사용하면 애플리케이션 전체에 기본적으로 @BatchSize를 적용할 수 있다.<br>
<property name="hibernate.default_batch_fetch_size" value="5"/></div>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 하이버네이트 @Fetch(FetchMode.SUBSELECT)
</h4>

하이버네이트가 제공하는 <span style="background: rgb(251,243,219)">org.hibernate.annotations.Fetch</span> 어노테이션에 FetchMode를 SUBSELET로 사용하면 연관된 데이터를 조회할 때 서브 쿼리를 사용해서 <span style="background: rgb(251,243,219)">N+1</span> 문제를 해결한다.

<br>

```java
@Entity
public class Member{
  ...
  @org.hibernate.annotations.Fetch(FetchMode.SUBSELECT)
  @OneToMay(mappedBy="member", fetch=FetchType.EAGER)
  private List<Order> orders=new ArrayList<Order>();
  ...
}
```

<br>
 
다음 JPQL로 회원 식별자 값이 <span style="background: rgb(251,243,219)">10</span>를 초과하는 회원을 모두 조회해보자.

<br>

```java
select m from Member m where m.id>10
```

<br>

<span style="background: rgb(251,243,219)">즉시 로딩</span>으로 설정하면 조회 시점에, <span style="background: rgb(251,243,219)">지연 로딩</span>으로 설정하면 지연 로딩된 엔티티를 사용하는 시점에 다음 SQL이 실행된다.

<br>

```sql
SELECT O FROM ORDERS
  WHERE O.MEMBER_ID IN (
    SELECT
        M.ID
    FROM
        MEMBER M
    WHERE M.ID > 10
  )
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> EntityGraph
</h4>

@EntityGraph의 <span style="background: rgb(251,243,219)">attributePaths</span>에 쿼리 수행시 바로 가져올 필드명을 지정하면 <span style="background: rgb(251,243,219)">Lazy가 아닌 Eager</span> 조회로 가져오게 된다. <span style="background: rgb(251,243,219)">Fetch join</span>과 동일하게 JPQL을 사용하면 query 문을 작성하고 필요한 연관관계를 <span style="background: rgb(251,243,219)">EntityGraph</span>에 설정하면 된다. 그리고 <span style="background: rgb(251,243,219)">Fetch Join과는</span> 다르게 join 문이 <span style="background: rgb(251,243,219)">outer join</span>으로 실행된다.(Fetch Join은 Inner join)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Fetch Join과 EntityGraph 주의할 점
</h4>

**Fetch Join과 EntityGraph**는 JPQL을 사용하여 <span style="background: rgb(251,243,219)">JOIN</span>문을 호출한다는 공통점이 있다. 또한, 공통적으로 <span style="background: rgb(251,243,219)">카테시안 곱(Cartesian Product)</span>이 발생하여 데이터 수만큼의 <span style="background: rgb(251,243,219)">중복 데이터</span>가 존재할 수 있다. 그러므로 <span style="background: rgb(251,243,219)">중복된 데이터</span>가 <span style="background: rgb(251,243,219)">컬렉션</span>에 존재하지 않도록 주의해야 한다.

<br>

**그렇다면 어떻게 중복된 데이터를 제거할 수 있을까?**

- 컬렉션을 **Set**을 사용하게 되면 중복을 허용하지 않는 자료구조이기 때문에 중복된 데이터를 제거할 수 있다.
- **JPQL**을 사용하기 때문에 **DISTINCT**를 사용하여 중복된 데이터를 조회하지 않을 수 있다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> N+1 정리
</h3>

<br>

<span style="background: rgb(251,243,219)">즉시 로딩과 지연 로딩</span> 중 추천하는 방법은 <span style="background: rgb(251,243,219)">즉시 로딩</span>은 사용하지 말고 <span style="background: rgb(251,243,219)">지연 로딩</span>만 사용하는 것이다.

<span style="background: rgb(251,243,219)">즉시 로딩</span> 전략은 그럴듯해 보이지만 <span style="background: rgb(251,243,219)">N+1</span> 문제는 물론이고 비즈니스 로직에 필요하지 않은 <span style="background: rgb(251,243,219)">엔티티를 로딩</span>해야 하는 상황이 자주 발생한다. 그리고 <span style="background: rgb(251,243,219)">즉시 로딩</span>의 가장 큰 문제는 <span style="background: rgb(251,243,219)">성능 최적화</span>가 어렵다는 점이다. 엔티티를 조회하다보면 <span style="background: rgb(251,243,219)">즉시 로딩</span>이 연속으로 발생해서 전혀 예상하지 못한 SQL이 실행될 수 있다. 따라서 모두 <span style="background: rgb(251,243,219)">지연 로딩으로</span> 설정하고 <span style="background: rgb(251,243,219)">성능 최적화</span>가 꼭 필요한 곳에는 **JPQL Fetch Join**을 사용하자.

<br>

JPA의 **글로벌 페치 전략 기본값은 다음과 같다**

- @OneToOne, @ManyToOne: 기본 페치 전략은 **즉시 로딩**
- @OneToMany, @ManyToMany: 기본 페치 전략은 **지연 로딩**

<br>

따라서 기본값이 즉시 로딩인 <span style="background: rgb(251,243,219)">@OneToOne과 @ManyToOne</span>은 <span style="background: rgb(251,243,219)">fetch=FetchType.LAZY</span>로 설정해서 <span style="background: rgb(251,243,219)">지연 로딩 전략</span>을 사용하도록 변경하자.

<br>

**[N+1에 대해 잘 설명한 글](https://velog.io/@jinyoungchoi95/JPA-%EB%AA%A8%EB%93%A0-N1-%EB%B0%9C%EC%83%9D-%EC%BC%80%EC%9D%B4%EC%8A%A4%EA%B3%BC-%ED%95%B4%EA%B2%B0%EC%B1%85)**
