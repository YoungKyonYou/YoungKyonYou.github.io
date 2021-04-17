---
layout: post
title: Springboot에서 Coolsms API를 사용해서 SMS 보내기
date: 2021-04-03 19:00:00 0000
tags: [Intellij, SpringBoot, Coolsms]
categories: [SpringBoot]
description: Coolsms API 사용하기
---

<br><br>

# <center>Coolsms API Testing 하기</center>

<br>

프로젝트를 하나 진행하다가 갑자기 좋은 아이디어가 떠올랐다. 프로젝트 내용을 자세하게 알려줄순 없지만 대략적으로 설명하면 어떠한 정보를 웹에서 사람들에게 핸드폰 메시지를 보내는 것이다.

<br>

그래서 구글링을 해서 방법을 찾아보았다. 방법은 바로 Coolsms API를 사용하는 것이다.

![](/images/SpringBoot/post10/2021-04-03-19-16-47.png)

<br>

일단 먼저 회원가입을 하면 기본적으로 주는 포인트가 얼마 있다. 문자 한통당 20원이며 긴 문자(LMS)는 좀 더 비싸다.

![](/images/SpringBoot/post10/2021-04-03-19-21-36.png)

<br>

로그인을 하고 나면 아마 송신 번호를 등록하는 등 몇가지 인증을 해야 됐던 걸로 기억한다. 그렇게 각종 절차를 마치고 왼쪽을 보면 개발/연동->API Key 관리 에 들어가면

![](/images/SpringBoot/post10/2021-04-03-19-22-23.png)

<br>

위 사진과 같이 **API Key**와 **API Secret**를 볼 수 있는데 이 두 개를 메모장에 붙여놓기 해놓는다.

<br>

자 이제 스프링부트 프로젝트를 하나 만들고 Test를 해본다.

```java
 @Test
    public void testSend() {
        String api_key = "API KEY";
        //사이트에서 발급 받은 API KEY
         String api_secret = "API SECRET KEY";
        // 사이트에서 발급 받은 API SECRET KEY
        Message coolsms = new Message(api_key, api_secret);

        HashMap<String, String> params = new HashMap<String, String>();
        params.put("to", "문자를 수신할 번호");
        params.put("from", "문자를 송신할 번호");

        params.put("type", "SMS");
        //문자 내용이 들어갈 부분
        params.put("text", "문자 내용");
        //메시지 내용
        params.put("app_version", "test app 1.2");
        try {
            JSONObject obj = (JSONObject) coolsms.send(params);
            System.out.println(obj.toString());
            //전송 결과 출력
        }catch (CoolsmsException e){
            System.out.println(e.getMessage());
            System.out.println(e.getCode());
        }
    }
```

<br>

위의 코드를 조금 설명하자면 **params.put("to", "문자를 수신할 번호");** 이부분은 문자를 수신할 번호가 문자열 형태로 들어가고 **params.put("from", "문자를 송신할 번호");** 에는 문자를 송신할 번호가 문자열 형태로 들어간다. 그리고 수신할 번호는 Coolsms에 내가 로그인한 아이디에 등록된 번호여야만 한다. **params.put("type", "SMS");** 에는 타입을 지정하는데 여기서는 SMS로 되어 있으나 좀 더 긴 문자를 보내고 싶으면 **LMS**로 변경해주면 된다. 단, 돈이 좀 더 든다. 마지막으로 **params.put("text", "문자 내용");** 에는 실질적으로 문자 내용이 문자열 형태로 들어가게 된다. 이 테스트 코드를 제대로 작성하고 실행하면 제대로 작동하는 것을 볼 수 있을 것이다.
