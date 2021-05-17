---
layout: post
title: Java Comparator를 이용한 정렬 및 중복 없애기
date: 2021-05-06 10:00:00 0000
tags: [Intellij, SpringBoot]
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

위에 데이터베이스 데이터를 보면 알겠지만 regdate 데이터는 날짜와 시간으로 이루어져 있다. 즉 날짜와 시간, 분, 초 그리고 미리초까지 일치해야 2차 정렬인 온도가 되는 것이다... 이것을 간과했던 것이다. 그리고 처음엔 이대로 hashmap에 넣어주면 되겠다고 생각했으나...

hashmap은 전 포스팅에서도 말했지만 순서 유지가 되지 않는다..

~~아니.. LinkedHashMap 사용하면 됐잖아.... 사실 지금 쓰는 시점에서 알게됨... 바보~~

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

먼저 Pair 클래스에서 구현하는 Comparable 인터페이스에 대해서 알아보자. Comparable 인터페이스는 compareTo()라는 함수를 구현하도록 하는데 여기서 실질적으로 정렬 조건문을 작성해서 사용자가 원하는 정렬을 구현해 낼 수 있다.

먼저 기본적인 조건들을 알아보자

---

> 1. 현재 객체 < 파라미터로 넘어온 객체: 음수 리턴
> 2. 현재 객체 == 파라미터로 넘어온 객체: 0 리턴
> 3. 현재 객체 > 파라미터로 넘어온 객체: 양수 리턴
> 4. 음수 또는 0이면 객체의 자리가 그대로 유지되며, 양수인 경우에는 두 객체의
>    자리가 바뀐다.

<br>

- 사용방법

  **Arrays.sort(array)**
  **Collections.sort(list)**

**참고**

## Arrays.sort()와 Collections.Sort()의 차이

**Arrays.sort()**

- 배열 정렬의 경우
- Ex) byte[], char[], double[], int[], Object[], T[] 등 \* Object Array에서는 TimSort(Merge Sort + Insertion Sort)를 사용
- Object Array: 새로 정의한 클래스에 대한 배열 \* Primitive Array에서는 Dual - Pivot QuickSort(Quick Sort + Insertion Sort)를 사용
- Primitive Array: 기본 자료형에 대한 배열

**Collections.sort()**

- List Collection 정렬의 경우
- Ex) ArrayList, LinkedList, Vector 등 \* 내부적으로 Arrays.sort()를 사용

<br>

현재 객체와 파라미터로 넘어온 객체를 비교할 때 리턴되는 값에 대해 이해를 돕기 위해서 아래 예제를 참고하자

```java

public class CompareToTest{

    public static void main(String[] args){

        Integer x = 4;
        Integer y = 5;
        Double z = 2.0;

        System.out.println( x.compareTo(y) );  // -1
        System.out.println( x.compareTo(4) );  //  0
        System.out.println( x.compareTo(2) );  //  1
        System.out.println( z.compareTo(3.7) );  //  -1

    }

}
```

<br>

긴 설명보다는 위와 같은 간단한 예제로 어떤 식으로 리턴이 되는 지 한 눈에 볼 수 있다.

다시 제시한 문제로 돌아와보자 내가 하려는 것은 날짜를 오름차순으로 정렬한 다음 날짜가 같으면 온도를 오름차순으로 정렬하려는 것이다. 내가 이것을 하기 위해서 택한 방법은 비효율적일 수 있다. 지금 생각해보면 왜 저렇게 했을까 라는 의문밖에 안 남지만.. 그래도 이러지 말아야겠다는 의미에서 기록해 본다.

실질적으로 정렬 함수로는 **Collections.sort()**라는 함수를 쓸 것이다. 클래스 list로 된 변수를 파라미터로 이 함수에 주게 되면 클래스에 오버라이딩되어 있는 compareTo()함수가 호출되어 정렬이 된다.

```java
@Override
    public List<Data> getList(Long mno) {
        List<Object[]> result = statusRepository.getMemberDailyTemperatureStatus(mno);
        HashMap<String, Double> dailyStatus = new HashMap<String, Double>();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy MM-dd");
        DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("yyyy MM-dd HH:mm:ss");
        String hhMMSS=" 00:00:00";
        List<Pair> pairList=new ArrayList<>();
        List<Data> dataList=new ArrayList<>();
        LocalDateTime stringToLdt;
        for (Object[] a : result) {
            if(a[0]!=null){
                String temp=((LocalDateTime) a[0]).format(formatter);
                temp+=hhMMSS;
                stringToLdt=LocalDateTime.parse(temp, formatter2);
                Pair pair=new Pair(stringToLdt,(double)a[1]);
                pairList.add(pair);
            }
        }
        Collections.sort(pairList);
        for(Pair p:pairList){
            dailyStatus.put(p.getX().format(formatter), p.getY());
        }


        dailyStatus.forEach((key, value)
                -> dataList.add(new Data(key,value)));
        Collections.sort(dataList);

        return dataList;
    }
```

<br>

위 코드를 보면 무언가 복잡하다... 일단 첫 번째 for문에서 데이터베이스로부터 받아온 날짜와 온도를 Pair List에 넣고 Collections.sort()로 정렬한다. 그렇게 날짜와 온도가 둘다 오름차순으로 정렬된 list를 HashMap에 넣게 되는데 이때 넣으면서 LocalDateTime 타입을 String 타입으로 포매팅 한다. 우리가 표에 날짜를 보여줄 때는 시간, 분, 초가 필요없으므로 날려버린다. 이미 정렬되어 있는 상태에서 HashMap에 넣을 때 key값이 같으면 가장 마지막으로 들어간 값만 남게 된다.

가령 현재 데이터가

2021/5/13 36.6
2021/5/13 36.7
2021/5/13 36.8
2021/5/13 36.9

<br>

이런식으로 정렬되어 있을 때 HashMap에서 우리는 키값으로 날짜를 줄 것이기 때문에 키값이 4번이나 겹친다. 이때 마지막으로 들어간 value값만 남게 되는게 결론적으로 **2021/5/13 36.9**만 남게 되는 것이다. 이런 식으로 모든 List에 있는 데이터를 HahsMaP에 넣고 나면 각 특정 날짜에 대한 제일 높은 온도만이 unique하게 남게 된다. 여기서 끝난 것이 아니다. HashMap에 들어갈 때 List가 정렬됐다고 해서 HashMap에서 뽑아 낼때도 정렬되어 있는 것이 아니다..

<br>

**HashMap 내부의 데이터 순서는 뒤죽박죽으로 되어 있다!!**

그럼으로 다시 뽑아내서 정렬을 해줘야 한다. 사실 이렇게 되어 있는 데이터를 날짜순으로만 정렬하기만 하면 되는데 왜 Data 클래스를 정의할 때 둘다 다시 정렬하게끔 짰는지 모르겠다.

~~무지성 코딩...~~

<br>

그래서 다시 Data 클래스를 정의해준 이유는 localDateTime 타입이 String 타입으로 바뀌어졌기 때문에 다시 정의를 해주고 정렬을 해준 것이다.

그래서 코드를 보면 Collections.sort()를 두 번해주는 것인데...
이렇게 코드를 짤 필요가 전혀 없었다. 진짜 말 그대로 LinkedHashMap으로 했으면 Data class를 따로 정의할 필요도 없고 Collections.sort()를 두번 쓸 필요가 없었다. 왜냐면 LinkedHashMap은 넣은 순서를 유지시켜 주기 때문이다.

<br>

실수로부터 배우는 것도 좋지만 좀 찾아보고 코딩을 하는 습관을 들여야 겠다.
