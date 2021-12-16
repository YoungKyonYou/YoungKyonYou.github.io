---
layout: post
title: 디자인 패턴-Chain of Responsibility Pattern
date: 2021-12-16 12:00:00 0000
tags: [Design Pattern, Chain of Responsibility Pattern]
categories: [Interview]
description: 책임 연쇄 Pattern에 대해 알아보자
---

<br><br>

_**오늘보다 발전된 내일의 나를 위해...**_

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

# <center>Design Pattern-Wrapper Pattern</center>

<br>

_해당 내용은 POCU 아카데미 COMP_2500에서 배운 내용을 공부하기 위해 작성된 글입니다_

<br>

### Proxy Pattern

<br>

책임 연쇄라는 말은 다소 추상적으로 들린다. 위키에서 책임 연쇄 패턴에 대해 찾아보면 아래와 같은 코드를 볼 수 있다.

<br>

![](/images/Interview/post5/2021-12-16-14-22-01.png?style=centerme)

<br>

하지만 이는 복잡하면서도 잘못된 책임 연쇄 패턴이다. 위키에 나온 예를 이해하기 쉽도록 구성해보자.

<br>

**Logger Class**

```java
public abstract class Logger{
  private EnmSet<LogLevel> logLevels;
  private Logger next;

  public Logger(LogLevel[] levels){
    this.logLevels=EnumSet.coptOf(Arrays.asList(levels));
  }

  public Logger setNext(Logger next){
    this.next=next;
    return this.next;
  }
  
  public final void message(String msg, LogLevel severity){
    if(logLevels.contains(severity)){
      log(msg);
    }

    if(this.next!=null){
      this.next.message(msg, severity);
    }
  }
  protected abstract void log(String msg);
}
```

<br>

위 코드를 살펴보면 멤버 변수로 next를 가지고 있는데 이는 자기 자신을 참조하기 위함이다. message 메서드에서의 if문은 만약 내가 severity 즉, 로그 레벨을 처리할 수 있다면(Enum<Set>에 안에 있음) msg를 로그 처리한다. 

<br>

**ConsoleLogger Class**

```java
public class ConsoleLogger extends Logger{
  public ConsoleLogger(LogLevel[] levels){
    super(levels);
  }

  @Override
  protected void log(String msg){
    System.err.println("Writing to console: " +msg);
  }
}
```

<br>

**EmailLogger Class**

```java
public class EmailLogger extends Logger{
  public EmailLogger(LogLevel[] levels){
    super(levels);
  }

  @Override
  protected void log(String msg){
    System.err.println("Sending via email: "+msg);
  }
}
```

<br>

**FileLogger Class**

```java
public class FileLogger extends Logger{
  public FileLogger(LogLevel[] levels){
    super(levels);
  }
  @Override
  protected void log(String msg){
    System.err.println("Writing to log file: "+msg);
  }
}
```

<br>

**Enum LogLevel**

```java
public enum LogLevel{
  INFO,
  DEBUG,
  WARNING,
  ERROR,
  FUNCTIONAL_MESSAGE,
  FUNCTIONAL_ERROR;

  public static LogLevel[] all(){
    return values();
  }
}
```

<br>

이제 실제로 로거를 써보자

**Main Class**

```java
Logger logger=new ConsoleLogger(LogLevel.all());
logger.setNext(new EmailLogger(new LogLevel[]{LogLevel.FUNCTIONAL_MESSAGE, LogLevel.FUNCTIONAL_ERROR})).setNext(new FileLogger(new LogLevel[]{LogLevel.WARNING, LogLevel.ERROR}));

// consoleLogger에서 처리 (consoleLogger는 모든 로그 레벨을 처리)
logger.message("Entering function ProcessOrder().", LogLevel.DEBUG);
logger.message("Order record retrieved.", LogLevel.INFO);

//consoleLogger와 emailLogger에서 처리한다
//(emailLogger는 Functional_Error과 Functional_Message 로그 레벨을 처리)
logger.message("Unable to Process Order ORD1 Dated D1 For Customer C1.", LogLevel.FUNCTIONAL_ERROR);
logger.message("Order Dispatched.", LogLevel.FUNCTIONAL_MESSAGE);

//consoleLogger와 fileLogger에서 처리 (fileLogger는 Warning과 Error 로그 레벨을 처리)
logger.message("Customer Address details missing in Branch DataBase.",LogLevel.WARNING);
logger.message("Customer Address details missing in Organization DataBase.",LogLevel.ERROR);
```

<br>

실제 로거는 하나만 만들고 그 로거에 메시지를 쏴주면 알아서 다 호출해주는 것이다. 이 logger가 연쇄적으로 다음 애들을 호출하는 방식이다. 

<br>

**Logger Class**

```java
public abstract class Logger{
  (...)
  
  public final void message(String msg, LogLevel severity){
    (...)

    if(this.next!=null){
      this.next.message(msg, severity);
    }
  }
  (...)
}
```

<br>

위 코드에서 if 문을 통해 다음을 호출한다. 하지만 여기서 질문을 해야 한다.

<br>

<span style="color:orange; font-weight:bold">왜 이런 쓸데없는 짓을 할까??</span>

<br>

훨씬 더 직관적인 방법을 살펴보자.

**LogManager Class**

```java
public final class LogManager{
  private static LogManager instance;

  private ArrayList<Logger> loggers=new ArrayList<Logger>();

  public static LogManager getInstance(){
    if(instance==null){
      instance=new LogManager();
    }

    return instance;
  }

  public void addHandler(Logger logger){
    this.loggers.add(logger);
  }

  public void mesage(String msg, LogLeve severity){
    for(Logger logger : this.loggers){
      logger.message(msg, severity);
    }
  }
}
```

<br>

**Logger Class**

```java
public abstract class Logger{
  private EnumSet<LogLevel> logLevels;

  public Logger(LogLevel[] levels){
    this.logLevels=EnumSet.copyOf(Arrays.asList(levels));
  }

  public final void message(String msg, LogLevel severity){
    if(logLevels.contains(severity)){
      log(msg);
    }
  }

  protected abstract void log(String msg);
}
```

<br>

**ConsoleLogger Class**

```java
public class ConsoleLogger extends Logger{
  public ConsoleLogger(LogLevel[] levels){
    super(levels);
  }

  @Override
  protected void log(String msg){
    System.err.println("Writing to console: " +msg);
  }
}
```

<br>

**EmailLogger Class**

```java
public class EmailLogger extends Logger{
  public EmailLogger(LogLevel[] levels){
    super(levels);
  }

  @Override
  protected void log(String msg){
    System.err.println("Writing to console: " +msg);
  }
}
```

<br>

**FileLogger Class**

```java
public class FileLogger extends Logger{
  public FileLogger(LogLevel[] levels){
    super(levels);
  }
  @Override
  protected void log(String msg){
    System.err.println("Writing to console: " +msg);
  }
}
```

<br>

**Main Class**

```java
LogManager logManager=LogManager.getInstance();

logManager.addHandler(new ConsoleLogger(LogLevel.all()));
logManager.addHandler(new EmailLogger(new LogLevel[]{LogLevel.FUNCTIONAL_MESSAGE,LogLevel.FUNCTIONAL_ERROR}));
logManager.addHandler(new FileLogger(new LogLevel[]{LogLevel.WARNING, LogLevel.ERROR}));

logManager.message("Entering function processOrder().", LogLevel.DEBUG);
logManager.message("Order record retrieved.", LogLevel.INFO);

logManager.message("Unable to Process Order ORD1 Dated D1 For Customer C1.", LogLevel.FUNCTIONAL_ERROR);
logManager.message("Customer Address details missing in Branch DataBase.",LogLevel.WARNING);
logManager.messagE("Customer Address details missing in Organization DataBase.",LogLevel.ERROR);
```

<br>

위키피디아에 있는 잘못된 코드보다 훨씬 더 낫다. 올바른 책임 연쇄 패턴은 어떤 메시지를 처리할 수 있는 여러 개체가 있을 때 이 개체들은 차례대로 메시지를 처리할 수 있는 기회를 받는다. 만약 그중 한 개체가 메시지를 처리하면 그거에 대한 책임을 진다. 즉 다음 개체는 메시지를 처리할 기회를 받지 못한다. 이래서 책임 연쇄란 이름이 붙었다. 그래서 맨 앞의 에의 올바른 구현은 아래와 같다.

<br>

![](/images/Interview/post5/2021-12-16-15-26-24.png?style=centerme)

<br>

