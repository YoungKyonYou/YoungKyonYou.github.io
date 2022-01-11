---
layout: post
title: HashMap vs Hashtable의 차이
date: 2022-01-11 14:20:00 0000
tags: [SQL, Partition]
categories: [Interview]
description: HashMap과 Hashtable의 차이
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> HashMap vs Hashtable</h2>

<br>

<span style="background: rgb(251,243,219)">Hashtalbe</span> 클래스는 <span style="background: rgb(251,243,219)">컬렉션 프레임워크</span>이 만들어지기 이전부터 존재하던 것이기 때문에 <span style="background: rgb(251,243,219)">컬렉션 프레임워크의 명명법</span>을 따르지 않는다.

<span style="background: rgb(251,243,219)">Vector나 Hashtable</span>과 같은 기존의 컬렉션 클래스들은 호환을 위해, 설계를 변경해서 남겨두었지만 가능하면 사용하지 않는 것이 좋다.(대신 ArrayList와 HashMap을 사용하는 것이 좋다.)

<br>

![](/images/Interview/post16/2022-01-11-16-32-08.png?style=centerme)

<br>

Hashtable는 자바에서 <span style="background: rgb(251,243,219)">해시 테이블을</span> 구현한 클래스 중 가장 오래되었다. 그리고 두 번째로 구현한 클래스는 <span style="background: rgb(251,243,219)">HashMap</span> 클래스이다. 즉 일반적으로 <span style="background: rgb(251,243,219)">HashMap</span>과 사용법이 거의동일하다. (예를 들면 key-value 형태이고 key는 중복될 수 없고 value는 중복될 수 있다는 특징들이다.)

<br>

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable {

    private float loadFactor;

    public Hashtable(int initialCapacity, float loadFactor) {

    }

    public Hashtable(int initialCapacity) {
        this(initialCapacity, 0.75f);
    }

    public Hashtable() {
        this(11, 0.75f);
    }
}
```

<br>

위와 같이 기본 생성자로 객체를 생성하게 되면 <span style="background: rgb(251,243,219)">초기용량(버킷의 수)=11, 로드팩터=0.75</span>로 설정된다. 

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> HashMap과 Hashtable 클래스의 차이점
</h3>

<br>

- **Thread-safe 여부**
  - Hashtalbe은 Thread-safe하고, HashMap은 Thread-safe 하지 않다는 특징을 가지고 있다. 그렇기에 멀티스레드 환경이 아니라면 Hashtable은 HashMap 보다 성능이 떨어진다는 단점을 가지고 있다.
- **Null 값 허용 여부**
  - Hashtable은 key에 null을 허용하지 않지만, HashMap은 key에 null을 허용합니다.
- **Enumeration 여부**
  - Hashtable은 not fail-fast Enumeraton을 제공하지만 HashMap은 Enumeration을 제공하지 않는다.
- HashMap은 **보조해시를 사용**하기 때문에 보조 해시 함수를 사용하지 않는 Hashtable에 비해서 해시 충돌(hash collistion)이 덜 발생할 수 있어 상대적으로 **성능상 이점**이 있다.
- 최근까지 **Hashtable**은 구현에 거의 변화가 없지만 **HashMap**은 현재까지도 지속적으로 개선되고 있다. 

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Fail Fast Iteration
</h4>

말 그대로 빠른 에러를 발생시켜 버그를 예방할 수 있다.

<br>

```java
public class Test1 {
    public static void main(String[] args) {
        Hashtable<Integer, Integer> hm = new Hashtable<>();
        hm.put(1, 1);
        hm.put(2, 1);

        Iterator<Integer> iterator = hm.keySet().iterator();
        hm.remove(1);

        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

```java
Exception in thread "main" java.util.ConcurrentModificationException
    at java.util.Hashtable$Enumerator.next(Hashtable.java:1387)
    at ExampleCode.Test1.main(Test1.java:18)
```

<br>

<span style="background: rgb(251,243,219)">Fail-fast iteration</span>은 반복자를 생성한 후 해시 테이블을 수정한 경우 위와 같은 예외가 발생한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Fail Fast Enumeration
</h4>

위에서 말하는 <span style="background: rgb(251,243,219)">not failt-fast Enumeration</span>이란 아래와 같다.

<br>

```java
public class Test1 {
    public static void main(String[] args) {
        Hashtable<Integer, Integer> hm = new Hashtable<>();
        hm.put(1, 1);
        hm.put(2, 1);

        Enumeration<Integer> keys = hm.keys();
        hm.remove(1);

        while (keys.hasMoreElements()) {
            System.out.println(keys.nextElement());
        }
    }
}
```

<br>

반면에 Enumeration를 사용한 코드는 중간에 remove를 해도 <span style="background: rgb(251,243,219)">예외</span>가 발생하지 않는다. 그렇기 때문에 나중에 버그를 발견하지 못할 확률도 존재한다.

<br>

---

<br>

<h2 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> HashMap 살펴보기
</h2>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 해시 충돌(Collisions)
</h3>

HashMap이 올바르게 작동하려면, 동일한 키는 같은 해시(hash) 값을 가져야 한다. 하지만 다른 키도 같은 해시(hash) 값을 가질 수 있다.(이것은 버킷의 용량, 해시함수 등등에 따라 영향을 받을 것이다.)

만약에 다른 키가 같은 해시 값을 가진다면 같으 버킷에 채워지게 된다. 원래는 버킷에 하나만 존재해야 시간 복잡도 O(1)에 찾아올 수 있는데 <span style="background: rgb(251,243,219)">버킷에 여러 개 존재하게 되면 어떻게 될까?</span>

이때는 버킷 내부에서 <span style="background: rgb(251,243,219)">리스트</span> 형태를 이용하여 원소들을 관리하게 된다. 그래서 버킷 내부에서 원소들을 검색할 때는 반복문으로 돌아가야 하기 때문에 <span style="background: rgb(251,243,219)">O(n)</span>의 시간이 걸리게 된다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 초기 용량과 로드 팩터
</h4>

HashMap의 <span style="background: rgb(251,243,219)">초기 용량(버킷 수)은 16</span>, <span style="background: rgb(251,243,219)">로드팩터는 0.75</span>이다. <span style="background: rgb(251,243,219)">(로드팩터=(데이터의 개수)/(초기 용량))</span> 버킷 하나에 여러 개의 값을 가지는 것, 즉 충돌을 피하기 위해서 설정한 것이다.

버킷의 <span style="background: rgb(251,243,219)">75퍼</span>가 찼다면 용량을 <span style="background: rgb(251,243,219)">2배로 </span>늘리는 과정이 일어난다. 그 과정에서 원래 버킷의 값들을 새로운 버킷에 옮기는 과정이 일어난다.(자주 일어난다면 성능에 좋지 않다.)

한마디로 <span style="background: rgb(251,243,219)">로드 팩터</span>는 언제 용량을 재설정 해주어야 효율적인지에 대한 <span style="background: rgb(251,243,219)">초기 설정 값</span>이라고 생각하면 된다.(그래서 초기용량, 로드팩터를 처음에 잘 설정하는 것이 중요하다.)