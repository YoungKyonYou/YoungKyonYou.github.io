---
layout: post
title: 직렬화(Serialization)
date: 2022-01-05 11:20:00 0000
tags: [Serialization, Deserialization]
categories: [Interview]
description: Serialization과 Deserialization
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
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/270f.png" height="30" width="30"> Serialization
</h2>

<br>

**Serialization**

- 자바 시스템 내부에서 사용되는 <span style="background: rgb(251,243,219)">Object</span> 또는 <span style="background: rgb(251,243,219)">Data</span>를 외부의 자바 시스템에서도 사용할 수 있도록 <span style="background: rgb(251,243,219)">byte 형태</span>로 데이터를 <span style="background: rgb(251,243,219)">변환하는 기술</span>이다.
- JVM의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 <span style="background: rgb(251,243,219)">바이트 형태</span>로 변환하는 기술

<br>

파일에 <span style="background: rgb(251,243,219)">텍스트를 기록</span>하고, <span style="background: rgb(251,243,219)">이진 데이터</span>를 기록하는 방법은 많이들 알고 있다.

그런데 만약 이런 종류의 데이터들이 아니라 <span style="background: rgb(251,243,219)">객체를</span> 파일로 저장하거나 읽어올 수 있을까?

**있다!!!**

**직렬화**가 그것을 가능하게 해준다.

<br>

이제부터 직렬화에 관한 간단한 예제를 살펴보자
아래 그림은 **Account**라는 클래스의 멤버 변수를 나타낸다. 이것을 객체화하여 <span style="background: rgb(251,243,219)">파일이나 네트워크로</span> **write**할 때는 **직렬화**를 거쳐서 전달된다.

반대로 읽어올때는 <span style="background: rgb(251,243,219)">역직렬화(Deserialization)</span>를 거쳐서 가져오게 된다.

<br>

![](/images/Interview/post16/2022-01-05-14-50-05.png?style=centerme)

<br>

**직렬화**에 <span style="background: rgb(251,243,219)">메서드</span>는 포함하지 않는다.

<span style="background: rgb(251,243,219)">메서드</span>는 각 클래스가 같은 동작을 수행하기 때문에 **직렬화**해서 저장할 필요는 없다.

단지 멤버들마다 다른 값을 가지고 있는 필드들이 **직렬화**가 된다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 직렬화는 어떻게 수행하는가?
</h4>

1. **직렬화가 가능한 클래스 구현하기**
2. **직렬화가 된 클래스의 객체를 쓰고 읽는 Stream 준비하기**

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 직렬화가 가능한 클래스 구현하기
</h4>

직렬화를 하려면 우선 <span style="background: rgb(251,243,219)">Serializable 인터페이스</span>를 **implements** 해야 한다. 그래서 우리가 **Account** 클래스를 정의하려면 아래와 같이 정의가 되어야 한다.

<br>

**Account.java**

```java
class Account implements Serializable{
	private String email;
	private String name;
	private String address;
	private String phone;
	private Date reg_date;
	public Account(String email,String name,String address,String phone) {
		this.email=email;
		this.name=name;
		this.address=address;
		this.phone=phone;
		reg_date=new Date();
	}

	public String getEmail() {
		return email;
	}
	public String getName() {
		return name;
	}
	public String getAddress() {
		return address;
	}
	public String getPhone() {
		return phone;
	}
	public String getRegDate() {
		SimpleDateFormat format=new SimpleDateFormat("yyyy-MM-dd");
		return format.format(reg_date);
	}
	@Override
	public String toString() {
		return "Information:"+getEmail()+"/"+getName()+"/"+getAddress()+"/"+getPhone()+"/"+getRegDate();

	}
}
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 직렬화 제외하기 - transient
</h4>

우리가 <span style="background: rgb(251,243,219)">직렬화로</span> 파일에다가 기록할 때 민감한 데이터이기 때문에 직렬화에 제외하는 방법은 <span style="background: rgb(251,243,219)">transient</span>라는 키워드를 사용하면 된다.

그러면 **직렬화**에 빠지게 되어 파일에 저장되지 않는다.

<br>

**Example**

```java
class Account implements Serializable{
	//... 생략 ...
	private Date reg_date;
	private transient String password;
	public Account(String email,String name,String address,String phone) {
		//...생략...
		reg_date=new Date();
		password="12341234";
	}
	//...생략...
}
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 객체 쓰기 (ObjectOutputStream)
</h4>

객체를 쓰려면 **stream**을 열어야 한다. 우리는 당장 파일에 그 객체를 쓸 것이기 때문에 <span style="background: rgb(251,243,219)">FileOutputStream</span>을 사용할 것이고 이 파일 스트림에 객체를 쓸 것이기 때문에 <span style="background: rgb(251,243,219)">ObjectOutputStream</span>을 사용할 것이다.

사용법은 간단하다.

아래의 차례대로 진행하면 된다.

우선 <span style="background: rgb(251,243,219)">FileOutputStream</span>으로 파일의 **Stream**을 열고 이것을 <span style="background: rgb(251,243,219)">ObjectOutputStream</span>으로 전달해주면 된다.

<br>

```java
FileOutputStream fos=new FileOutputStream("user.acc");
ObjectOutputStream oos=new ObjectOutputStream(fos);
```

<br>

여기서 <span style="background: rgb(251,243,219)">user.acc</span>는 우리가 객체를 저장할 **파일 이름**이다.

파일을 열때 <span style="background: rgb(251,243,219)">FileNotFoundException이라는 IOException</span>이 발생할 수 있다.

이것이 주목적은 아니기 때문에 **메인 함수**에서 **throw**로 처리한다.

<br>

```java
public static void main(String[] ar) throws IOException
```

<br>

그리고 파일에 써줄 객체를 정의해주고 <span style="background: rgb(251,243,219)">ObjectOutputStream</span>의 객체 쓰기 메서드인 **writeObject**에 전달해주면 된다.

그리하여 객체를 쓰는 전체코드는 아래와 같다.

<br>

**Main**

```java
public static void main(String[] ar) throws IOException, ClassNotFoundException{
	Account wuser=new Account("reakwon@aaa.ccc","reakwon","seoul","010-1234-1010");

	FileOutputStream fos=new FileOutputStream("user.acc");
	ObjectOutputStream oos=new ObjectOutputStream(fos);
	oos.writeObject(wuser);
	oos.close();
}
```

<br>

위 코드를 실행하면 파일은 <span style="background: rgb(251,243,219)">working directory</span>에 있다.

<br>

![](/images/Interview/post16/2022-01-05-15-09-26.png?style=centerme)

<br>

그리고 메모장으로 그 내용을 까보면 아래와 같다.

물론 여기에는 **직렬화하지 않길 원하는 멤버 필드(transient로 선언한 멤버 필드)**가 기록되어 있지 않다.

<br>

![](/images/Interview/post16/2022-01-05-15-10-27.png?style=centerme)

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 객체 읽기 (ObjectInputStream)
</h4>

이제는 이 파일에 쓰여진 객체를 읽어보자.

<span style="background: rgb(251,243,219)">파일 읽기 스트림(FileInputStream)</span>을 열고 <span style="background: rgb(251,243,219)">ObjectInputStream</span>을 통해서 읽어오면 된다.

이것 역시 간단하게 **ObjectInputStream**에 **FileInputStream**을 전달하고 <span style="background: rgb(251,243,219)">readObject</span>를 이용해서 객체를 얻어오면 된다.

이때 **Object 객체**로 반환하기 때문에 <span style="background: rgb(251,243,219)">적절한 형변환</span>을 해줘야 한다.

<br>

**Example**

```java
Account ruser=null;

FileInputStream fis=new FileInputStream("user.acc");
ObjectInputStream ois=new ObjectInputStream(fis);
ruser=(Account)ois.readObject();

ois.close();
```

<br>

혹시나 객체의 클래스를 찾을 수가 없는 예외가 발생할 수 있다. 그때 발생할 수 있는 예외가 <span style="background: rgb(251,243,219)">ClassNotFoundException</span>이다.

이것도 메인 메서드에서 던져준다.

<br>

```java
public static void main(String[] ar) throws IOException, ClassNotFoundException{
```

<br>

객체를 쓰고 읽는 전체 코드는 아래와 같다.

<br>

**Main**

```java
public class Main {

	public static void main(String[] ar) throws IOException, ClassNotFoundException{
		Account wuser=new Account("reakwon@aaa.ccc","reakwon","seoul","010-1234-1010");

		Account ruser=null;

		FileOutputStream fos=new FileOutputStream("user.acc");
		ObjectOutputStream oos=new ObjectOutputStream(fos);
		oos.writeObject(wuser);

		FileInputStream fis=new FileInputStream("user.acc");
		ObjectInputStream ois=new ObjectInputStream(fis);
		ruser=(Account)ois.readObject();

		System.out.println(ruser);

		oos.close();
		ois.close();

	}
}
```

<br>

그래서 읽어보면 제대로 읽어오는 것을 확인할 수가 있다.

<br>

```java
Information:reakwon@aaa.ccc/reakwon/seoul/010-1234-1010/2021-04-07
```

<br>

만약 <span style="background: rgb(251,243,219)">transient</span>로 **직렬화**에 포함되지 않은 데이터를 읽을 때는 <span style="background: rgb(251,243,219)">null</span>로 읽힌다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 주의
</h4>

**객체의 직렬화나 역직렬화에서 클래스는 완전한 동일한 클래스**를 통해서 쓰고 읽혀야 한다.

그렇지 않은 경우 아래와 같은 에러가 발생한다.

여기서 쓸때는 기존의 **Account 클래스**, 그리고 읽을 때는 멤버 필드를 추가해 변경된 **Account 클래스**로 읽어보았다.

<br>

```java
Exception in thread "main" java.io.InvalidClassException: aa.Account; local class incompatible: stream classdesc serialVersionUID = 2399026023152107267, local class serialVersionUID = 9178730303496146785
	at java.base/java.io.ObjectStreamClass.initNonProxy(ObjectStreamClass.java:722)
	at java.base/java.io.ObjectInputStream.readNonProxyDesc(ObjectInputStream.java:2022)
	at java.base/java.io.ObjectInputStream.readClassDesc(ObjectInputStream.java:1872)
	at java.base/java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2179)
	at java.base/java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1689)
	at java.base/java.io.ObjectInputStream.readObject(ObjectInputStream.java:495)
	at java.base/java.io.ObjectInputStream.readObject(ObjectInputStream.java:453)
	at aa.Main.main(Main.java:15)
```

<br>

이렇게 **InvalidClassException** 이라는 예외가 발생함으로 우리는 **직렬화 클래스의 버전**을 관리해줘야 한다.

자바는 **serialVersionUID**를 통해서 버전이 같은 클래스인지 아닌지 판단할 수 있다.

그래서 이 버전이 같은지 같지 않은지를 통해서 **조치**를 취해야 한다.

<br>

```java
class Account implements Serializable{
	static final long serialVersionUID=1919191919191919L;
    //...생략...
}
```
