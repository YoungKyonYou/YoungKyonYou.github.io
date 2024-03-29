---
layout: post
title: Mutable vs Immutable
date: 2021-12-27 10:00:00 0000
tags: [Spring WebFlux]
categories: [Interview]
description: Mutable과 Immutable이란
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

## Immutable vs Mutable

<br>

<span style="color:#2ECC40; font-weight:bold">Mutable:</span> 변할 수 있는; 잘 변하는

<span style="color:#2ECC40; font-weight:bold">Immutable:</span> 변경할 수 없는; 불변의

<br>

무엇이 변하고 무엇이 변하지 않는 걸까?

값? 주소?

정의를 하자면

<span style="color:#85144b; font-weight:bold">Mutable</span>은 값을 수정해도 주소가 바뀌지 않는 것이다.

<span style="color:#85144b; font-weight:bold">Immutable</span>은 값을 수정하면 주소가 바뀌는 것을 말한다.

<br>

이렇게 말하면 앞서 말한 영어 정의랑 헷갈린다.

<br>

다시 말하면 Immutable 객체는 **객체 내의 특정 요소의 값을 변경 할 수 없는 객체**이다.

or

문자열 연산에서 <span style="background: rgb(251,243,219)">new 연산</span>을 통해 생성된 <span style="background: rgb(251,243,219)">인스턴스</span>의 <span style="background: rgb(251,243,219)">메모리 공간</span>이 절대 변하지 않는 것이다.

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

불변 객체는 생성 후 그 상태를 바꿀 수 없다. 이는 힙영역에서 그 객체가 가리키고 있는 데이터 자체의 변화가 불가능하다는 것을 의미한다.

실제 데이터는 힙 영역에 저장되고 그 힙 영역을 가리키는 주솟값을 stack 영역에서 가리키고 있는데 불변 객체는 힙 영역에 있는 데이터가 변경되지 않는 것을 의미한다. </div>

<br>

즉, 여기서 **변하지 않는다**는 것은 <span style="color:#3D9970; font-weight:bold">객체가 생성되면 변하지 않는다==객체를 재할당 받는다</span> 와 같은 말이다.

<br>

<span style="background: rgb(251,243,219)">Immutable</span>은 대표적으로 **String**이 있다.

<br>

<span style="background: rgb(251,243,219)">String</span> 변수는 <span style="background: rgb(251,243,219)">한번 할당</span>하고 그 변수에 새로운 문자열을 합치거나 변경할 때 <span style="background: rgb(251,243,219)">새로운 주소값</span>이 생기면서 <span style="background: rgb(251,243,219)">객체가 할당</span>된다.

<br>

**Example**

```java
String result = "Hello";
result = result.concat("World");
```

<br>

![](/images/Interview/post15/2021-12-28-00-35-31.png?style=centerme)

<br>

위 사진처럼 주소값이 다른 이유는 String의 concat은 **new String()**으로 새로운 객체를 만들어 할당받기 때문이다.

<br>

**Example**

```java
String userName = "홍길동";
System.out.println(userName);

userName = "둘리";
System.out.println(userName);

// result
홍길동
둘리
```

<br>

![](/images/Interview/post15/2021-12-28-00-37-07.png?style=centerme)

<br>

위 예제에서도 userName은 홍길동이라는 값을 가지고 <span style="color:#7EDBFF; font-weight:bold">1000번</span> 주소에 할당되었지만 값이 변경되면 <span style="color:#7EDBFF; font-weight:bold">1000번</span>을 가리키고 있던 것을 새로운 객체가 있는 <span style="color:#7EDBFF; font-weight:bold">2000번</span>으로 변경한다.

<br>

---

반면에 대표적인 <span style="background: rgb(251,243,219)">Mutable 개체</span>로 **StringBuilder**가 있다. (List, ArrayList, HashMap 등도 Mutable)

<br>

**Example**

```java
StringBuilder result = new StringBuilder();
result.append("Hello");
result.append("World");
```

<br>

![](/images/Interview/post15/2021-12-28-00-39-25.png?style=centerme)

<br>

위 에서는 변수의 문자열이 추가되어도 주소가 변하지 않는 것을 볼 수 있다.

<br>

#### Immutable한 클래스에는 어떤 것이 있을까?

<br>

- **String, Boolean, Integer, Float, Long** 등이 있다.

<br>

<span style="background: rgb(251,243,219)">immutable한 클래스</span>를 만들어 보자.

<br>

<span style="background: rgb(251,243,219)">immutable</span>은 값을 변경할 수 없는 클래스를 뜻한다. 즉 <span style="background: rgb(251,243,219)">setter 메서드</span>가 없다. 또한 <span style="background: rgb(251,243,219)">final 키워드</span>를 사용해 변수 초기화 이후 바뀌지 않도록 막는다.

<br>

**Example**

```java
public class ImmutableTest {

    private final String userName;

    ImmutableTest(String userName){
        this.userName = userName;
    }

    @Override
    public String toString(){
        return this.userName;
    }

}
```

<br>

```java
String userName = "홍길동";
ImmutableTest immutableString = new ImmutableTest(userName);
userName = new String("둘리");
System.out.println(immutableString);
```

<br>

결과 값은 <span style="background: rgb(251,243,219)">immutable</span>로 만들었던 <span style="background: rgb(251,243,219)">userName(홍길동)</span>은 변하지 않고, <span style="background: rgb(251,243,219)">새로운 객체</span> 둘리가 <span style="background: rgb(251,243,219)">userName에 할당</span>된다.

<br>

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Immutable Object의 장단점
</h3>

<br>

**장점**

- 객체에 대한 **신뢰도가 높아진다.** 객체가 한번 생성되어서 그게 변하지 않는다면 transaction 내에서 그 객체가 변하지 않기에 믿고 쓸 수 있기 때문이다.
- 생성자, 접근메소드에 대한 **방어 복사가 필요없다.**
- 멀티스레드 환경에서 동기화 처리없이 **객체를 공유**할 수 있다.

<br>

**단점**

- 객체가 가지는 값마다 **새로운 객체가 필요**하다. 따라서 **메모리 누수**와 새로운 객체를 계속 생성해야 하기 때문에 **성능저하**를 발생시킬 수 있다.

---

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> Java에서 불변 객체를 생성하기 위한 규칙
</h3>

<br>

1. 클래스를 **final**로 선언하라
2. 모든 클래스 변수를 **private와 final**로 선언하라
3. 객체를 생성하기 위한 생성자 또는 **정적 팩토리 메서드**를 추가하라
4. 참조에 의해 변경가능성이 있는 경우 **방어적 복사**를 이용하여 전달하라

<br>

**Example**

```java
public final class ImmutableClass {
    private final int age;
    private final String name;
    private final List<String> list;

    private ImmutableClass(int age, String name) {
        this.age = age;
        this.name = name;
        this.list = new ArrayList<>();
    }

    public static ImmutableClass of(int age, String name) {
        return new ImmutableClass(age, name);
    }

    public int getAge() {
        return age;
    }

    public String getName() {
        return name;
    }

    public List<String> getList() {
        return Collections.unmodifiableList(list);
    }
}
```

<br>

위의 코드에서 특히 주목해야 하는 부분은 내부 생성자를 만드는 대신 객체의 생성을 위해 **정적 팩토리 메소드**를 제공하고 있다는 점과 참조를 전달하여 클라이언트에 의해 **수정 가능성**이 있는 **list를 방어적 복사**하여 제공하고 있다는 것이다.

Java에서는 **생성자를 선언하지 않으면 기본 생성자가 자동으로 생성**되는데, 그러면 다른 클래스에서 해당 객체를 자유롭게 호출할 수 있다. 그렇기 때문에 내부 생성자를 만드는 대신 **정적 팩토리 메소드**를 통해 객체를 생성하도록 강요하는 것이 좋다.

또한 배열이나 다른 객체 또는 컬렉션은 참조가 전달되어 **수정 가능성**이 있다. 그렇기 때문에 참조를 통해 변경이 가능한 경우에는 **방어적 복사**를 통해 값을 반환해야 한다.
