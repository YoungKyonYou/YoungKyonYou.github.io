---
layout: post
title: 당근페이 면접 후기 및 질문과 답-3
date: 2021-12-21 13:00:00 0000
tags: [java 11]
categories: [Interview]
description: 당근페이 면접 질문에 대한 답
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

다음 당근 페이 질문은 아래와 같다.

<span style="color:#107896; font-weight:bold">Q: 어떤 버전의 자바를 쓰시고 계신가요?</span>

<span style="color:#85144b; font-weight:bold">A: java 11 버전을 쓰고 있습니다.</span>

<span style="color:#107896; font-weight:bold">Q: java 11 버전에 추가된 것엔 어떤 것들이 있나요?</span>

<br>

참 당혹스러운 질문이다... 사실 팀이랑 버젼을 맞추기 위해 LTS 버젼으로 맞춘건데 java 11에는 뭐가 추가됐냐니... 그래도 java 8에는 뭐가 추가 됐는지는 대충 안다. Nashorn, Stream API, Lambda 가 추가된 걸로 아는데 java 11은 아무것도 모르겠다.. 그래서 이번 기회에 java 11에서 추가된 것을 적어보자.

<br>

**Java 11**은 **Java 8** 이후 첫 번째 <span style="background: rgb(251,243,219)">LTS (장기 지원) 릴리스</span>이다. Oracle도 2019년 1월 Java 8 지원을 중단 했다. 결과적으로 많은 사람들이 Java 11로 업그레이드하는 결과를 가져왔다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 개발자 측면
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 새로운 문자열 메서드
</h4>

**Java 11은 몇 가지 새로운 메서드를 String 클래스에 추가한다**

- **isBlank():** 문자열이 비어있거나 공백만 포함되어 있을 경우 true를 반환한다. 즉, String.trim().isEmpty() 호출 결과와 같다.

<br>

- **lines():** 문자열을 라인 단위로 쪼개는 스트림을 반환한다.

**Example**

```java
import java.io.IOException;
import java.util.stream.Stream;

public class Main
{
    public static void main(String[] args)
    {
        try
        {
            String str = "A \n B \n C \n D";

            Stream<String> lines = str.lines();

            lines.forEach(System.out::println);
        }
        catch (IOException e)
        {
            e.printStackTrace();
        }
    }
}
```

<br>

**결과**

![](/images/Interview/post9/2021-12-21-21-57-18.png?style=centerme)

<br>

- **repeat(n):** 지정된 수 만큼 문자열을 반복하여 붙여 반환한다

<br>

**Example**

```java
String str = "ABC";
String repeated = str.repeat(3);	// "ABCABCABC"
```

<br>

- **strip:** 문자열 앞, 뒤의 공백 제거
- **stripLeading():** 문자열 앞의 공백 제거
- **stripgTrailing():** 문자열 뒤의 공백 제거

<br>

여기서 <span style="background: rgb(251,243,219)">strip</span>이 <span style="background: rgb(251,243,219)">trime</span>과 다를 게 없다고 생각할 수 있으나 **trim**은 '\u0020' 이하의 공백들만 제거한다. **strip**은 유니코드의 공백들을 모두 제거한다.

<br>

사실 <span style="background: rgb(251,243,219)">유니코드</span>에는 우리가 일반적으로 많이 사용하는 스페이스('\u0020'), 탭('\u0009) 등 외에도 더 많은 종류의 공백 문자들이 있습니다. <span style="background: rgb(251,243,219)">strip()</span> 메소드는 <span style="background: rgb(251,243,219)">trim()</span> 보다 <span style="background: rgb(251,243,219)">더 많은 종류의 공백을 제거</span>할 수 있습니다. 보통 <span style="background: rgb(251,243,219)">whitespace</span>라고 하면 간단하게 tab 문자(U+0009), 공백(U+0020), CR(U+000D), LF(U+000A) 등이 있다.

**라인피드(LF : Line Feed)** => 현재 위치에서 바로 아래로 이동

**캐리지리턴(CR: Carriage return)** => 커서의 위치를 앞으로 이동

<br>

<link href="http://fonts.googleapis.com/earlyaccess/hanna.css" rel="stylesheet">
<div style="background: #eee;
  box-shadow: 0 8px 8px -4px lightblue; font-family: 'Hanna', sans-serif;; padding: 40px;">

자바에서 String.format()를 쓸 때 줄바꿈을 하기 위해 \n으로 쓰게 되는데 이렇게 쓰면 어떤 OS에서는 제대로 작동하지 않을 수가 있다. 예를 들어 윈도우/DOS 에서는 CRLF 조합으로 줄바꿈을 정의하는 반면에 Unix/Linux/C는 LF 만으로 줄바꿈을 정의한다. 그럼으로 \n으로 줄바꿈을 하는 것보다 System.lineSeparator()를 쓰는 것을 추천한다.</div>

<br>

**Example**

```java
public class StringSpace {
  public static void main(String[] args) {
    // 앞뒤로 공백이 있는 문자열
    String str = "\u2003Hi Anna!\u2003";
    // 공백 제거
    String trimStr = str.trim();
    String stripStr = str.strip();
    // 공백 제거 문자열 출력
    System.out.println("원본 문자열 : '" + str + "'");
    System.out.println("trim 문자열 : '" + trimStr + "'");
    System.out.println("strip 문자열 : '" + stripStr + "'");
  }
}
```

<br>

**결과**

```java
원본 문자열 : ' Hi Anna! '
trim 문자열 : ' Hi Anna! '
strip 문자열 : 'Hi Anna!'
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 새 파일 방법
</h4>

이제 <span style="background: rgb(251,243,219)">파일에서 String을 읽고 쓰는 것</span>이 더 쉬워졌다. File 클래스에서 새로운 <span style="background: rgb(251,243,219)">readString 및 writeString 정적 메서드를 사용</span>할 수 있기 때문이다.

<br>

**Example**

```java
Path filePath = Files.writeString(Files.createTempFile(tempDir, "demo", ".txt"), "Sample text");
String fileContent = Files.readString(filePath);
assertThat(fileContent).isEqualTo("Sample text");
```

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 컬렉션을 배열로 수집하기
</h4>

<span style="background: rgb(251,243,219)">java.util.Collection</span>은 새로운 디폴트 메서드로 <span style="background: rgb(251,243,219)">toArray</span>가 생겼다. 이것은 컬렉션을 배열로 쉽게 변환시켜 준다.

<br>

**Example**

```java
List sampleList = Arrays.asList("Java", "Kotlin");
String[] sampleArray = sampleList.toArray(String[]::new);
assertThat(sampleArray).containsExactly("Java", "Kotlin");
```

<br>

### 1-4. Not 술어 메서드

**Predicate** 인터페이스에 <span style="background: rgb(251,243,219)">정적 not 메서드</span>가 추가되었다. <span style="background: rgb(251,243,219)">negate 메서드</span>와 같이 기존 술어를 부정하는데 사용할 수 있다.

**Example**

```java
List<String> sampleList = Arrays.asList("Java", "\n \n", "Kotlin", " ");
List withoutBlanks = sampleList.stream()
  .filter(Predicate.not(String::isBlank))
  .collect(Collectors.toList());
assertThat(withoutBlanks).containsExactly("Java", "Kotlin");
```

<span style="background: rgb(251,243,219)">not (isBlank)</span>가 <span style="background: rgb(251,243,219)">isBlank .negate()</span> 보다 더 자연스럽게 읽는 반면 , 큰 장점은 <span style="background: rgb(251,243,219)">not (String : isBlank)</span>와 같은 메소드 참조와 함께 <span style="background: rgb(251,243,219)">not</span>을 사용할 수도 있다는 것 입니다.

<br>

또 여러 가지 개발자 측면에서 바뀐 게 있지만 여기까지만 설명하고 다음으로 측면으로 넘어가보자. 추가적인 것은 이 **[링크](https://www.baeldung.com/java-11-new-features)**를 참조한다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 성능 향상
</h3>

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 새로운 가비지 컬렉터
</h4>

**ZGC:** A Scalable Low-Latency Garbage Collector (Experimental)

<br>

<span style="background: rgb(251,243,219)">성능을 향상시킨 새로운 가비지 컬렉터</span>이다. 메모리를 자동으로 정리해주는 GC는 자바의 장점 중 하나지만 GC가 동작할 때 JVM이 애플리케이션을 멈추기 때문에 어떻게 보면 단점이다. <span style="background: rgb(251,243,219)">ZGC는 이 시간을 10ms 미만으로 줄이고 15% 이하의 성능 패널티</span>를 목표로 한다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Flight Recorder
</h4>

<span style="background: rgb(251,243,219)">Flight Recorder</span>는 자바 애플리케이션과 <span style="background: rgb(251,243,219)">HotSpot JVM</span>의 문제 해결을 위한 <span style="background: rgb(251,243,219)">오버헤드가 낮은 데이터 수집 프레임워크</span>이다.

<br>

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 사라진 기능
</h3>

<br>

사라진 기능도 간단하게 살펴보겠다.

- **Java EE and CORBA Modules :** 앞으로 EE 나 CORBA 모듈이 필요한 경우 명시적으로 의존을 추가해야 합니다.
- **Web Start :** 특별한 대안 없이 삭제되었습니다.
- **Applets :** 한동안 대부분 deprecated 되었다가 완전히 삭제되었습니다.
- **JavaFX :** FX 라이브러리가 OpenJFX 프로젝트로 옮겨가면서 코어에서 삭제되었습니다.

<h3 style="color:#107896;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f4cc.png" height="30" width="30"> 기타
</h3>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> TLS 1.3
</h4>

TLS의 새로운 버전을 구현

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 람다에서의 var 변수
</h4>

자바 10에서 도입된 var 타입 추론을 업데이트

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> 새로운 표준 HTTP 라이브러리
</h4>

<span style="background: rgb(251,243,219)">HTTP Clinet(Standard). java.net.http 패키지의 새로운 모듈</span>로 <span style="background: rgb(251,243,219)"> flow 기반의 HTTP/1.1과 HTTP/2를 지원</span>합니다. 자바 9과 자바 10에서 사용되었던 jdk.incubator.http 패키지가 표준화되어 java.net.http 패키지로 추가되었습니다.

<br>

<h4 style="color:#43ABC9;  font-weight:bold">
<img class="emoji" title=":pushpin:" alt=":pushpin:" src="https://github.githubassets.com/images/icons/emoji/unicode/1f50e.png" height="20" width="20"> Nest 기반 접근 제어
</h4>

<span style="background: rgb(251,243,219)">Nest</span>는 접근 제어 컨텍스트로 논리적으로는 같은 클래스를 분리된 클래스로 컴파일할 수 있게 해줍니다. 그러면 다른 클래스의 private 멤버에 getter/setter 없이 바로 접근 가능합니다. <span style="background: rgb(251,243,219)">여러 클래스를 하나의 클래스처럼 묶어줄 수 있는 기술</span>로 보입니다.
