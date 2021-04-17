---
layout: post
title: Springboot WebSocket를 이용한 채팅 어플리케이션 만들기-01
date: 2021-03-12 19:00:00 0000
tags: [Intellij, SpringBoot, WebSocket, STOMP]
categories: [SpringBoot]
description: WebSocket과 STOMP.js를 이용해서 채팅 앱 만들기
---

<br><br>

# <center>WebSocket를 이용한 채팅 앱 만들기-01</center>

<br>

졸업 작품을 스프링부트를 이용해서 만들고 있는 도중에 실시간으로 데이터베이스로부터 업데이트된 정보를 받아서 차트에 띄워주는 기능을 구현하려고 여러 자료들을 찾아봤더니 나온 답이 websocket를 이용하는 것이였다. 물론 다른 방법도 있었지만 그나마 보편적으로 쓰이는 게 이 방법인 것 같아서 websocket를 사용하여 앱을 만드는 연습을 해보려고 한다.

<br>

**_"해당 앱은 'https://ratseno.tistory.com/71'의 블로그를 보면서 따라하며 공부하기 위한 것임을 알립니다. 해당 링크에 아래에 걸어 놓겠습니다._"**

**[블로그 링크](https://ratseno.tistory.com/71)**

<br>

사실 세 가지 방법 중에서 고민을 하고 있었다.

1. Firebase
2. Ajax
3. WebSocket

<br>

아 그리고 절대 쓰고 싶지 않은 방법인 주기적인 새로고침... 이건 절대 하지 말아야 겠다고 생각을 했었다. 왜냐면 내 자존심이 허락을 안 해줄뿐만 부하도 크기 때문이다.

<br>

시작하기에 앞서 인텔리제이 프로젝트를 생성해야 한다. 나는 학생 인증을 받아서 인텔리제이 Ultimate 버젼을 쓰고 있다.

<br>

Group 이름은 com.techlead로 하고 Artifact는 websocketpractice로 한다. 영상에서는 Maven과 Jar를 썼지만 나는 Gradle를 War로 설정해서 진행한다. (사실 Maven으로 해도 무방하다)

![](../images/SpringBoot/websocket/2021-03-12-22-43-37.png)

<br>

그리고 의존성 설정을 해준다.

- WebSocket
- Lombok
- Spring Boot DevTools

<br>

패키지와 자바 파일 구성은 아래 사진과 같다.

![](../images/SpringBoot/websocket/2021-03-10-22-02-59.png)

<br>

프로젝트를 생성했으면 자바 코드부터 생성한다. 우리는 백엔드와 프론트엔드를 만들지만 백엔드부터 만들어보자, 백엔드를 만드는 것이 더 쉽기 때문이다. 아래 사진과 같이 패키지와 프로젝트를 만든다.

![](../images/SpringBoot/websocket/2021-03-12-22-45-31.png)

<br>

config 패키지에 있는 자바 파일부터 코드를 생성해보자. WebSocketMessageBrokerConfigurer 인터페이스는 디폴트 메서드가 있기 때문에 **registerStompEndpoints**와 **configureMessageBroker**를 오버라이딩 해준다.

**WebsocketConfiguration.java**

```java
package com.techlead.websocketpractice.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.messaging.simp.config.MessageBrokerRegistry;
import org.springframework.web.socket.config.annotation.EnableWebSocketMessageBroker;
import org.springframework.web.socket.config.annotation.StompEndpointRegistry;
import org.springframework.web.socket.config.annotation.WebSocketMessageBrokerConfigurer;


@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        System.out.println("end point 연결!!!***");
        registry.addEndpoint("/ws").withSockJS();
    }

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {

        System.out.println("confiureMessageBroker 연동!!**");
        registry.setApplicationDestinationPrefixes("/app");
        registry.enableSimpleBroker("/topic");
    }

}


```

<br>

**@Configuration** 어노테이션은 해당 클래스가 Bean의 설정을 할 것이라는 것을 나타내며 **@EnableWebSocketMessageBroker**는 WebSocket 서버를 활성화시킨다. **WebSocketMessageBrokerConfigurer** 인터페이스는 웹 소켓 연결을 구성하기 위한 메서드를 제공한다. 나중에 프론트엔드에서 sockJS 객체를 생성하기 위해서 엔드포인트를 설정해야 하는데 이 엔드포인트 설정을 **registerStompEndpoints** 메서드에서 설정한다. 즉 이 메서드에서는 클라이언트에서 websocket에 접속하는 endpoint를 등록한다. **configureMessageBroker** 메서드는 한 클라이언트에서 다른 클라이언트로 메시지를 라우팅 할 때 사용하는 브로커를 구성한다. 여기서 **/app**으로 시작되는 메시지만 메시지 핸들러로 라우팅한다고 정의한다. **/topic**으로 시작하는 주제를 가진 메시지를 핸들러로 라우팅하여 해당 주제에 가입한 모든 클라이언트에게 메시지를 방송한다.
이 경로는 차후에 아래와 같이 쓰일 것이다.

```javascript
stompClient.subscribe("/topic/public", onMessageReceived);
stompClient.send(
  "/app/chat.addUser",
  {},
  JSON.stringify({ sender: username, type: "JOIN" })
);
```

<br>

이제 model 패키지의 파일들에 코드를 추가해보자. ChatMessage 클래스는 메시지 타입, 메시지 내용 그리고 송신자로 이루어져 있다. MessageType Enum클래스는 메시지 타입을 명시한다.

**ChatMessage.java**

```java
package com.techlead.websocketpractice.model;

import lombok.Data;

@Data
public class ChatMessage {
    private MessageType type;
    private String content;
    private String sender;

}

```

<br>

@Data 어노테이션은 해당 필드들의 setter와 getter를 만들어주는 아주 편리한 롬복 어노테이션이니 알아두도록 하자.

**MessageType Enum**

```java
package com.techlead.websocketpractice.model;

public enum MessageType {
    CHAT,
    JOIN,
    LEAVE
}

```

<br>

메시지 타입은 말 그대로 채팅 할때, 새롭게 채팅 방에 들어올 때 그리고 마지막으로 채팅방을 떠날 때로 이루어져 있다.

controller 패키지의 WebSocketEventListener 자바 클래스에 코드를 추가해보자.

**WebSocketEventListener.java**

```java
package com.techlead.websocketpractice.controller;

import com.techlead.websocketpractice.model.ChatMessage;
import com.techlead.websocketpractice.model.MessageType;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.context.event.EventListener;
import org.springframework.messaging.simp.SimpMessageSendingOperations;

import org.springframework.messaging.simp.stomp.StompHeaderAccessor;
import org.springframework.stereotype.Component;

import org.springframework.web.socket.messaging.SessionConnectedEvent;
import org.springframework.web.socket.messaging.SessionDisconnectEvent;


@Component
public class WebSocketEventListener {
    private static final Logger logger = LoggerFactory.getLogger(WebSocketEventListener.class);

    @Autowired
    private SimpMessageSendingOperations messagingTemplate;
    @EventListener
    public void handleWebSocketConnectListener(SessionConnectedEvent event) {
        System.out.println("connected listener");
        logger.info("Received a new web socket connection");
    }


    @EventListener
    public void handleWebSocketDisconnectListener(SessionDisconnectEvent event) {
        System.out.println("disconnected listener");
        StompHeaderAccessor headerAccessor = StompHeaderAccessor.wrap(event.getMessage());

        String username = (String) headerAccessor.getSessionAttributes().get("username");
        if(username != null) {
            logger.info("User Disconnected : " + username);

            ChatMessage chatMessage = new ChatMessage();
            chatMessage.setType(MessageType.LEAVE);
            chatMessage.setSender(username);

            messagingTemplate.convertAndSend("/topic/public", chatMessage);
        }
    }
}

```

<br>

스프링 4.2부터는 이벤트 리스너가 ApplicationListener 인터페이스를 구현하는 Bean일 필요가 없어졌다. **@EventListener** 주석을 통해서 관리되는 Bean의 모든 public 메소드에 등록 할 수 있게 되었고 해당 어노테이션은 Bean으로 등록된 Class의 메서드에서 사용할 수 있다. **handleWebSocketConnectListener** 메소드는 클라이언트가 웹소켓에 연결되었을 때 호출된다. 여기서는 채팅방에 참여하고 있는 클라이언트에게 새로운 클라이언트가 채팅방에 연결됨을 방송해야 하나 우리는 좀 있다가 ChatController에서 addUser() 메소드를 통해 사용자 참여 이벤트를 broadcast할 것임으로 여기서는 별다른 동작없이 로깅 처리만 한다. **handleWebSocketDisconnectListener** 메소드는 클라이언트와 연결이 끊겼을 때 호출이 되는 메서드이다. 여기서는 웹 소켓 세션에서 사용자 이름을 추출하고 연결된 모든 클라이언트에게 사용자 퇴장 이벤트를 방송(broadcast)하는 코드를 작성한다.

<br>

이제 ChatController 클래스를 구성해보자.

**ChatController.java**

```java
package com.techlead.websocketpractice.controller;

import com.techlead.websocketpractice.model.ChatMessage;
import org.springframework.messaging.handler.annotation.MessageMapping;
import org.springframework.messaging.handler.annotation.Payload;
import org.springframework.messaging.handler.annotation.SendTo;
import org.springframework.messaging.simp.SimpMessageHeaderAccessor;
import org.springframework.stereotype.Controller;



@Controller
public class ChatController {
    @MessageMapping("/chat.sendMessage")
    @SendTo("/topic/public")
    public ChatMessage sendMessage(@Payload ChatMessage chatMessage){
        System.out.println("sendMessage method!!!***");
        return chatMessage;
    }

    @MessageMapping("/chat.addUser")
    @SendTo("/topic/public")
    public ChatMessage addUser(@Payload ChatMessage chatMessage, SimpMessageHeaderAccessor headerAccessor){
        headerAccessor.getSessionAttributes().put("username", chatMessage.getSender());
        System.out.println("addUser method!!!***");
        return chatMessage;
    }
}

```

<br>

이 클래스에서는 한 클라이언트에게서 message를 수신한 다음 다른 client에게 Broadcast한다. **sendMessage** 메소드부터 살펴보면 **/app** 으로 시작하는 대상이 있는 클라이언트에서 보낸 모든 메시지가 **@MessageMapping** 어노테이션이 달린 메서드로 라우팅된다. 즉 **"/app/chat.sendMessage"** 인 메시지는 sendMessage()로 라우팅되며 **"/app/chat.addUser"** 인 메시지는 addUser()로 라우팅된다. 이 메서드로 들어온 메시지는 파라미터로 되어 있는 chatMessage 변수에 매핑이된다. **addUser** 메서드에서는 사용자 참여 이벤트를 방송한다. heaerAccessor 변수를 통해서 세션에 username를 저장하고 있다.

---

다음 게시물에서 프론트엔드를 구성해 보자.
