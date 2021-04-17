---
layout: post
title: Intellij(인텔리제이)와 AWS의 RDS(MySql)와 S3 연동-01
image: /Program/post-2/main.jpg
date: 2021-01-21 19:00:00 0000
tags: [Intellij, AWS, RDS, S3, MySql, MySql Workbench]
categories: program
description: Intellij와 AWS의 RDS와 S3 연동
---

<br><br>
<br><br>

# <center>인텔리제이와 AWS의 RDS-MySql Workbench 연동하기</center>

<br><br>
AWS에서는 AWS 클라우드에서 관계형 데이터베이스를 더 쉽게 설치, 운영 및 확장할 수 있는 웹 서비스를 제공한다. 이 서비스는 산업 표준 관계형 데이터베이스를 위한 경제적이고 크기 조절이 가능한 용량을 제공하고 공통 데이터베이스 관리 작업을 관리한다.

![packed](..\images\Program\post-2\RDS.png){: width="400" height="700"}

---

학교에서 프로젝트하면서 데이터베이스 연동할 일이 참 많았는데 팀 프로젝트 할 때 이 RDS 서비스를 이용하면 서로 DB 수정한 것이 바로 업로드되서 참 편리했던 기억이 있다. 그때는 이클립스와 MySql를 써서 했었는데 이번에는 Intellij를 써서 MySql RDS를 연동하는 방법을 익혀보겠다.

---

일단 기본적으로 AWS 사이트에서 회원가입을 해야 한다.(링크 참고)

- [AWS 사이트](https://aws.amazon.com/ko/)
  그냥 가입해서 쓰면 요금이 조금 나갈 수가 있다.
  <u>옛날에 가입해서 잘 기억이 안 나는데 내 기억으로는 카드를 등록해야 됐던 것 같다.</u>
  그리고 다행히 대학교 학생들에게는 1년 프리티어를 제공함으로 용량이 적은 서비스들을 무료로 한정된 금액 안에서 쓸 수 있다.
  자신이 대학교 학생이라면 학생 인증을 통해 프리티어를 제공받자!

---

그렇게 로그인하고 나면 이러한 페이지가 나온다.
바로 화면에 DashBoard가 뜨게되는데 여기서 스크롤을 조금 밑으로 내리면
<u>데이터 베이스-RDS</u> 항목이 보일 것이다.
이것을 클릭한다.

![RDS_category](..\images\Program\post-2\RDS_category.PNG)
<br><br><br><br><br><br>

그러고 나면
RDS 창이 뜨게 되고 데이터베이스 생성하는 버튼이 있다.
그것을 누르자.

![RDS](..\images\Program\post-2\rds_dashboard.PNG)
<br><br><br><br><br><br>

누르면 이제 데이터베이스 설정하는 페이지가 나온다 차근차근 체크를 해보자
**여기서 잘못 체크하면 요금이 대폭 나올 수도 있으니 잘 따라해야 한다.**

### **데이터베이스 생성 방식 선택에서는 표준 생성을 체크한다.**

![RDS standard](..\images\Program\post-2\standard.PNG)
<br><br><br><br><br><br>

엔진 옵션에서는 어떤 데이터베이스 유형을 사용할 건지 선택한다.

### **우리는 엔진 옵션에서 MySQL를 선택한다.**

버전은 자신의 mysql workbench에 맞게 설정해주면 된다.

![RDS option](..\images\Program\post-2\engine_option.PNG)
<br><br><br><br><br><br>

### **템플릿으로 우리는 프로덕션이 디폴트로 되어 있지만 개발/테스트로 체크를 한다.**

**만약 프리티어를 등록했다면 프리 티어로 한다!!!**
여기서 나는 프리티어 등록을 했기 때문에 프리 티어로 등록하지만 프리티어가 아니라면 개발/테스트를 체크해도 무방하다.

![RDS template](..\images\Program\post-2\template.PNG)
<br><br><br><br><br><br>

### **설정 정보 입력**

DB 식별자로는 rdsDB로 설정하고
마스터 사용자 이름은 admin으로 하고 마스터 암호로는 admin!!!로 설정한다. 암호확인은 마스터 암호와 동일하게 쓰면 된다.

![RDS configuraton](..\images\Program\post-2\configuration.PNG)
<br><br><br><br><br><br>

# **DB 인스턴스 크기로는 버스터블 클래스-db.t3.micro로 설정한다!!**

여기는 일부로 위에 글과 달리 글자를 크게한 <u>이유</u>가 있다.
여기서 실수로 **micro가 아닌 xlarge로 설정한다면 요금이 크게 나올 수가 있기 때문이다!!** 실수하지 말고 체크하자!!
지금은 간단하게 연동 방법을 알려주고 있기 때문에 제일 작은 데이터베이스 인스턴스를 사용하지만 추후에 큰 프로젝트를 할 땐 더 큰 사이즈로 변경해야 한다.(물론 요금이 더 비쌈)

![RDS instance size](..\images\Program\post-2\instance_size.PNG)
<br><br><br><br><br><br>

### **범용 SSD 체크와 할당된 스토리지는 20 그리고 최대 스토리지 임계값은 30으로 한다.**

여기서는 개별적으로 설정해줘도 된다.

![RDS storage](..\images\Program\post-2\storage.PNG)
<br><br><br><br><br><br>

가용성 및 내구성은

### **'대기 인스턴스를 생성하지 마십시오'에 체크한다.**

![RDS availability](..\images\Program\post-2\availability.PNG)
<br><br><br><br><br><br>

연결 부분에서는
VPC 설정, 서브넷 그룹은 디폴트로 두고 퍼블릭 액세스 가능은 예를 체크하자. 그리고 보안 그룹 은 기존 항목 선택에 두고 기존 VPC 보안 그룹도 디폴트로 두고 가용 영역은 기본 설정 없음으로 둔다.

![RDS connection](..\images\Program\post-2\connection.PNG)
<br><br><br><br><br><br>

### **데이터베이스 생성을 누른다**

이러면 클라우드기반 데이터베이스가 생성이 된다.

![RDS database_creation](..\images\Program\post-2\database_creation.PNG)
<br><br><br><br><br><br>

### **결과**

![RDS result](..\images\Program\post-2\result.PNG)
<br><br>

---

다음 편에서는 인텔리제이와 RDS를 연동하는 것을 해보자
