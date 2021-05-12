---
layout: post
title: Java Comparator를 이용한 정렬 및 중복 없애기
date: 2021-05-06 10:00:00 0000
tags: [Intellij, SpringBoot, Coolsms]
categories: [SpringBoot]
description: Sorting with multiple fields
---

<br><br>

# <center>LocalDateTime 타입과 Double 타입 정렬하기</center>

<br>

바로 이전 포스팅에서 나는 그래프의 X축에 표시된 날짜 데이터가 정렬되어 있지 않아서 매우 애먹었었다. 내 실력이 부족한 탓도 있고 잘못된 기억으로 인해 피해를 본 것이었다....

이번 포스팅은 Comparator를 이용한 정렬 방식이다. 하나를 정렬하는 것은 쉬우나 여러 필드를 정렬하는 것은 좀 헷갈릴 수 있다.

일단 우리가 정렬하게 될 데이터를 먼저 살펴보자.

![](/images/SpringBoot/post12/2021-05-06-12-47-03.png)

<br>

위에 사진은 mysql workbench에 들어 있는 데이터들이다. member_mno는 각 사람마다 고유한 번호를 가지고 있는 것이고 state는 출입 상태이고 거기서 regdate는 출입한 시간이다.

내가 표시하려고 하는 그래프는 아래와 같다. 날짜가 정렬되어 있고 온도는 그 날짜 중 가장 큰 온도를 채택한다.

![](/images/SpringBoot/post12/2021-05-06-12-43-04.png)

<br>

데이터베이스 데이터를 보면 알겠지만 하루에 한 사람 여러 빌딩을 왔다갔다 하고 그로인해 많은 데이터가 축적되는 것을 볼 수 있다. 우리가 해야 할것은 특정한 사람이 출입한 날짜와 그에 해당하는 온도를 가져와서 날짜별로 가장 높은 온도로 구분 시켜주는 것이다. 지금 당장 member_mno 28번만 보더라도 2021년 5월 4일부터 2021년 5월 6일까지의 데이터가 들어가 있다.

<br>

정리하면

1. '2021년 5월 4일' 이라는 데이터와 그날 가장 높은 온도
2. '2021년 5월 5일' 이라는 데이터와 그날 가장 높은 온도
3. '2021년 5월 6일' 이라는 데이터와 그날 가장 높은 온도

<br>

가 필요한 것이다.

---

처음에 내가 실수했던 부분을 먼저 짚어보자. 나는 일단 Query Method으로 정렬하기 위해서 아래와 같이 사용했다.

```java
  @Query("select s.regDate, s.temperature from Status s where s.member.mno=:mno order by s.regDate ASC, s.temperature ASC")
  List<Object[]> getMemberDailyTemperatureStatus(Long mno);
```

<br>

위 코드는 일단 status 테이블로부터 날짜와 온도를 가져오 돼 날짜를 오름차순으로 정렬하고 날짜가 같으면 온도도 오름차순으로 정렬하게끔 만들었다.

하지만 여기에 치명적인 오류가 있다.....

위에 데이터베이스 데이터를 보면 알겠지만 regdate 데이터는 날짜와 시간으로 이루어져 있다... 즉 날짜와 시간, 분, 초 그리고 미리초까지 일치해야 2차 정렬인 온도가 되는 것이다... 이것을 간과했던 것이다. 그리고 처음엔 이대로 hashmap에 넣어주면 되겠다고 생각했으나...

hashmap은 전 포스팅에서도 말했지만 순서 유지가 되지 않는다..

~~아니.. LinkedHashMap 사용하면 됐잖아.... 사실 지금 쓰는 시점에서 알게됨...~~

<br>

---

**<h3>해결책</h3>**

<br>

```java
 class Pair implements Comparable<Pair>{

        private LocalDateTime ldt;
        private double temperature;
        public Pair(LocalDateTime x, double y){
            this.ldt=x;
            this.temperature=y;
        }

        public LocalDateTime getX(){
            return ldt;
        }

        public double getY(){
            return temperature;
        }

        @Override
        public int compareTo(Pair o) {
            boolean isAfter= this.ldt.isAfter(o.getX());


            if(isAfter){
                return 1;
            }else if(this.ldt.isEqual(o.getX())){
                if(this.temperature>o.temperature)
                    return 1;
            }
            return -1;
        }
    }
    class Data implements Comparable<Data>{

        private String ldt;
        private double temperature;
        public Data(String x, double y){
            this.ldt=x;
            this.temperature=y;
        }

        public String getX(){
            return ldt;
        }

        public double getY(){
            return temperature;
        }

        @Override
        public int compareTo(Data o) {
            if(this.ldt.compareTo(o.ldt)>0?true:false){
                return 1;
            }else if(this.ldt.equals(o.ldt)){
                if(this.temperature>o.temperature)
                    return 1;
            }
            return -1;
        }
    }
```

<br>
