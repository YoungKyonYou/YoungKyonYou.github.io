---
layout: post
title: Python3과 PyPy3의 차이
date: 2021-05-30 14:00:00 0000
tags: [Python, CPython, Jython, PyPy3, JIT]
categories: [Python]
description: PyPy3에 대하여
---

<br><br>

# <center>PyPy3</center>

<br>

어제 파이썬으로 백준 문제를 풀다가 Python3 언어로 제출했는데 시간 초과가 났다. 하지만 설마? 라는 마음에 PyPy3로 돌려봤는데 문제가 맞았다!! 왜 그런 것일까?... PyPy3가 뭔지 궁금해 졌다. 그래서 구글링해서 **stackoverflow**에 올라온 답변에 대해서 해석하는 시간을 가지려 한다.

<br>

**~~발해석 주의..~~**

<br>

[StackOverflow 링크](https://stackoverflow.com/questions/59050724/whats-the-differences-python3-and-pypy3)

<br>

우리가 일반적으로 파이썬 프로그래밍 언어에 대해서 말할 때 파이썬 그 언어 자체를 의미하기도 하지만 그 실행 방식를 의미하기도 한다. 파이썬은 다양한 방식으로 구현할 수 있는 언어 사양이다.

<br>

---

파이썬 프로그래밍 언어의 디폴트 실행은 **Cpython**이다(python3에 대해 말하는 것은 Cpython를 의미하는 것과 같다). Cpython은 C 언어로 만들어졌다는 의미이다. Cpython은 파이썬 소스 코드를 **intermediate bytecode**로 컴파일하는데 이것은 Cpython 가상 머신으로부터 실행된다.

<br>

**Jython**은 자바 플랫폼에서 실행가능한 파이썬 프로그래밍 언어의 구현이다. Jython 프로그램은 파이썬 모듈을 사용하는 대신 자바 클래스들을 사용한다. Jython은 자바 바이트 코드로 컴파일하게 되는데 이는 자바 가상 머신에 의해 실행될 수 있다.

<br>

**PyPy**, 우리가 만약 우리의 코드가 더 빨리 실행되길 원한다면 사용해야 한다 **-Guido can Rossum** (파이썬의 창시자). 파이썬은 다이나믹 프로그래밍 언어이다. 파이썬은 디폴트로 Cpython 실행으로 인해 파이썬 소스코드를 바이트 코드로 컴파일 해주는데 이는 기계 코드(원시 코드, native code)와 비교해서 느리다. 여기에 PyPy가 빛을 바랜다.

<br>

**PyPy**는 파이썬으로 만들어진 파이썬 프로그래밍 언어의 구현이다. 인터프리터는 RPython(파이썬의 한 언어)으로 만들어졌다. PyPy는 **Just In Time (JIT)** 컴파일 작업을 한다. 쉽게 말해서, **JIT**은 컴파일 도구를 사용하여 인터프리터 시스템을 더 효율적이고 빠르게 만든다. 그래서 기본적으로 JIT은 소스코드를 원시코드(native code)로 컴파일하는 작업을 더 빠르게 만든다. PyPy는 거대한 병렬처리를 지원하는 마이크로 쓰레드를 제공하는 stackless 모드 대한 기본 지원도 제공한다. Python은 대략 CPython보다 7.5배 빠른 것으로 알려져 있다.

---


