---
layout: post
title: Java Class 타입 List를 자바스크립트에서 데이터를 뽑아 사용하기
date: 2021-04-03 19:00:00 0000
tags: [Intellij, SpringBoot, Coolsms]
categories: [SpringBoot]
description: Passing class type list to javascript
---

<br><br>

# <center>클래스 타입의 리스트 데이터 사용하기</center>

<br>

졸업작품을 거의 다 만든 상태에서 계속 여러 버그를 찾고 고치고를 반복하던 중 highchart의 선 그래프 x축 데이터가 정렬이 제대로 안 되어 있는 것을 보게 되었다. 원래 날짜 순으로 보여줘야 하는데 날짜가 뒤죽박죽 되어 있었던 것이다.
아래 사진은 다시 정렬을 제대로 한 사진이고 제대로 안 된 사진은 찍지 못했다....

~~포스팅 할 줄 몰랐거든..~~

![](/images/SpringBoot/post11/2021-05-06-10-46-06.png)

<br>

원인은 일단 내가 hashmap에 대해서 기억이 왜곡되어 있었기 때문이다. 내가 처음에 알기론 일단 key값이 중복된 value가 들어가게 되면 가장 마지막에 들어간 데이터만 남게 되고 순서는 key값으로 정렬된다고 알고 있었기 때문이다. 전자는 맞으나 후자는 틀리다. 왜 이렇게 기억하고 있었는지는 모르지만 hashmap은 내부적으로 정렬을 전혀 해주지 않는다...

~~이 바보야!!~~

<br>

그래서 이 버그를 알기 전에는 그냥 hashmap형태로 프론트로 보내고 데이터 순서가 뒤죽박죽인 상태로 쓴 것이였다. 이제 원인을 찾았으니 정렬을 해주고 다시 보내줘야 하는데 일단 생각해본 것은 pair를 쓰는 것이였다. 그래서 자바에서 pair를 쓰는 방법을 검색했으나...

**자바에서는 Pair를 따로 제공하지 않는다..**

~~갑자기 C++ 그립네...~~

<br>

자바에서 pair는 제공하지 않지만 class 형태로 구현하면 된다는 것을 알고 그대로 시행했다. 그렇게 List를 써서 class 타입으로 만든 다음 컨트롤러에서 model.addAttribute()으로 넘겨줬는데 문제는 아래 사진과 같았다.

![](/images/SpringBoot/post11/2021-05-06-10-53-44.png)

<br>

자바스크립트에서 배열 변수로 받고 찍어보니 이런 형태로 나온다..

~~내가 실력이 부족해서... 처음엔 당황스러웠다...~~

<br>

자 이것을 이제 어떻게 날짜 별로 날짜 배열 변수에 담고 온도 별로 온도 배열 변수에 담을 수 있을 까 고민했다...

음.. 중괄호는 객체를 의미하고 지금 각 인덱스 0~6까지 객체들을 각각 담고 있다. 일단 forEach문을 이용해서 각각을 임시 배열에 넣은 다음 분리해보자고 생각했다.

```javascript
var dateData = [];
var temperatureData = [];
var tempData = [];
var i = 0;
console.log(classList);
classList.forEach(function (element) {
  Object.keys(element).forEach(function (key) {
    tempData[i++] = element[key];
  });
});
```

<br>

위 코드를 보면 일단 forEach문으로 각 객체를 분리하고 그 분리된 객체를 Object.key를 이용해서 각 변수에 담겨진 값을 뽑아 낸다.

이렇게 tempData를 console로 찍어내면 아래와 같이 된다.

![](/images/SpringBoot/post11/2021-05-06-10-59-13.png)

<br>

완벽하다. 보니까 짝수 인덱스엔 날짜 데이터가 들어가 있고 홀수 인덱스에는 온도 데이터가 들어가 있으니 이것을 이제 if문으로 분리 시켜주면 되겠다.

```javascript
for (var j = 0; j < tempData.length; j++) {
  if (j % 2 === 0) {
    dateData[didx++] = tempData[j];
    console.log("짝수:" + tempData[j]);
  } else {
    temperatureData[tidx++] = tempData[j];
    console.log("홀수:" + tempData[j]);
  }
}
```

<br>

이렇게 하면 분리 성공!!!

이 배열 변수를 그대로 쓰기만 하면 되는 것이다.

사실 내가 실력이 부족해서 LocalDateTime 타입의 날짜 정렬을 하는데 무지 애먹었다... 왜 애먹었는지에 대해서는 기회가 되면 포스팅 하겠다.

~~Comparator 너무 어려워!!~~
