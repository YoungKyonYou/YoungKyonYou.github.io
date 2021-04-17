---
layout: post
title: Springboot WebSocket를 이용한 채팅 어플리케이션 만들기-02
date: 2021-03-12 22:00:00 0000
tags: [Intellij, SpringBoot, WebSocket, STOMP]
categories: [SpringBoot]
description: WebSocket과 STOMP.js를 이용해서 채팅 앱 만들기
---

<br><br>

# <center>WebSocket를 이용한 채팅 앱 만들기-02</center>

<br>

이전 게시물에서 백엔드를 다뤘다면 이제 프론트엔드를 작성해보자. 파일 구성은 아래 사진과 같다.

![](../images/SpringBoot/websocket/2021-03-12-23-34-25.png)

<br>

우리의 목적은 웹소켓을 다루는 것이기 때문에 프론트엔드에 대해 자세하게 설명하진 않는다. 일단 css와 html 코드를 작성하자.

**main.css**

```css
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

html,
body {
  height: 100%;
  overflow: hidden;
}

body {
  margin: 0;
  padding: 0;
  font-weight: 400;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 1rem;
  line-height: 1.58;
  color: #333;
  background-color: #f4f4f4;
  height: 100%;
}

body:before {
  height: 50%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: #128ff2;
  content: "";
  z-index: 0;
}

.clearfix:after {
  display: block;
  content: "";
  clear: both;
}

.hidden {
  display: none;
}

.form-control {
  width: 100%;
  min-height: 38px;
  font-size: 15px;
  border: 1px solid #c8c8c8;
}

.form-group {
  margin-bottom: 15px;
}

input {
  padding-left: 10px;
  outline: none;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin-top: 20px;
  margin-bottom: 20px;
}

h1 {
  font-size: 1.7em;
}

a {
  color: #128ff2;
}

button {
  box-shadow: none;
  border: 1px solid transparent;
  font-size: 14px;
  outline: none;
  line-height: 100%;
  white-space: nowrap;
  vertical-align: middle;
  padding: 0.6rem 1rem;
  border-radius: 2px;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  min-height: 38px;
}

button.default {
  background-color: #e8e8e8;
  color: #333;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12);
}

button.primary {
  background-color: #128ff2;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12);
  color: #fff;
}

button.accent {
  background-color: #ff4743;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12);
  color: #fff;
}

#username-page {
  text-align: center;
}

.username-page-container {
  background: #fff;
  box-shadow: 0 1px 11px rgba(0, 0, 0, 0.27);
  border-radius: 2px;
  width: 100%;
  max-width: 500px;
  display: inline-block;
  margin-top: 42px;
  vertical-align: middle;
  position: relative;
  padding: 35px 55px 35px;
  min-height: 250px;
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  margin: 0 auto;
  margin-top: -160px;
}

.username-page-container .username-submit {
  margin-top: 10px;
}

#chat-page {
  position: relative;
  height: 100%;
}

.chat-container {
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
  background-color: #fff;
  box-shadow: 0 1px 11px rgba(0, 0, 0, 0.27);
  margin-top: 30px;
  height: calc(100% - 60px);
  max-height: 600px;
  position: relative;
}

#chat-page ul {
  list-style-type: none;
  background-color: #fff;
  margin: 0;
  overflow: auto;
  overflow-y: scroll;
  padding: 0 20px 0px 20px;
  height: calc(100% - 150px);
}

#chat-page #messageForm {
  padding: 20px;
}

#chat-page ul li {
  line-height: 1.5rem;
  padding: 10px 20px;
  margin: 0;
  border-bottom: 1px solid #f4f4f4;
}

#chat-page ul li p {
  margin: 0;
}

#chat-page .event-message {
  width: 100%;
  text-align: center;
  clear: both;
}

#chat-page .event-message p {
  color: #777;
  font-size: 14px;
  word-wrap: break-word;
}

#chat-page .chat-message {
  padding-left: 68px;
  position: relative;
}

#chat-page .chat-message i {
  position: absolute;
  width: 42px;
  height: 42px;
  overflow: hidden;
  left: 10px;
  display: inline-block;
  vertical-align: middle;
  font-size: 18px;
  line-height: 42px;
  color: #fff;
  text-align: center;
  border-radius: 50%;
  font-style: normal;
  text-transform: uppercase;
}

#chat-page .chat-message span {
  color: #333;
  font-weight: 600;
}

#chat-page .chat-message p {
  color: #43464b;
}

#messageForm .input-group input {
  float: left;
  width: calc(100% - 85px);
}

#messageForm .input-group button {
  float: left;
  width: 80px;
  height: 38px;
  margin-left: 5px;
}

.chat-header {
  text-align: center;
  padding: 15px;
  border-bottom: 1px solid #ececec;
}

.chat-header h2 {
  margin: 0;
  font-weight: 500;
}

.connecting {
  padding-top: 5px;
  text-align: center;
  color: #777;
  position: absolute;
  top: 65px;
  width: 100%;
}

@media screen and (max-width: 730px) {
  .chat-container {
    margin-left: 10px;
    margin-right: 10px;
    margin-top: 10px;
  }
}

@media screen and (max-width: 480px) {
  .chat-container {
    height: calc(100% - 30px);
  }

  .username-page-container {
    width: auto;
    margin-left: 15px;
    margin-right: 15px;
    padding: 25px;
  }

  #chat-page ul {
    height: calc(100% - 120px);
  }

  #messageForm .input-group button {
    width: 65px;
  }

  #messageForm .input-group input {
    width: calc(100% - 70px);
  }

  .chat-header {
    padding: 10px;
  }

  .connecting {
    top: 60px;
  }

  .chat-header h2 {
    font-size: 1.1em;
  }
}
```

<br>

**index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, minimum-scale=1.0"
    />
    <title>Spring Boot WebSocket Chat Application</title>
    <link rel="stylesheet" href="/css/main.css" />
  </head>
  <body>
    <div id="username-page">
      <div class="username-page-container">
        <h1 class="title">username을 입력하세요</h1>
        <form id="usernameForm" name="usernameForm">
          <div class="form-group">
            <input
              type="text"
              id="name"
              placeholder="Username"
              autocomplete="off"
              class="form-control"
            />
          </div>
          <div class="form-group">
            <button type="submit" class="accent username-submit">
              채팅 시작하기
            </button>
          </div>
        </form>
      </div>
    </div>

    <div id="chat-page" class="hidden">
      <div class="chat-container">
        <div class="chat-header">
          <h2>Spring WebSocket Chat Demo</h2>
        </div>
        <div class="connecting">연결중...</div>
        <ul id="messageArea"></ul>
        <form id="messageForm" name="messageForm">
          <div class="form-group">
            <div class="input-group clearfix">
              <input
                type="text"
                id="message"
                placeholder="Type a message..."
                autocomplete="off"
                class="form-control"
              />
              <button type="submit" class="primary">보내기</button>
            </div>
          </div>
        </form>
      </div>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/sockjs-client/1.4.0/sockjs.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stomp.js/2.3.3/stomp.min.js"></script>
    <script src="/js/main.js"></script>
  </body>
</html>
```

<br>

마지막으로 웹소켓에서 sockJS 객체를 생성하고 실질적으로 메시지를 송신하고 수신하는 자바스크립트 부분이다.

**main.js**

```javascript
"use strict";

var usernamePage = document.querySelector("#username-page");
var chatPage = document.querySelector("#chat-page");
var usernameForm = document.querySelector("#usernameForm");
var messageForm = document.querySelector("#messageForm");
var messageInput = document.querySelector("#message");
var messageArea = document.querySelector("#messageArea");
var connectingElement = document.querySelector(".connecting");

var stompClient = null;
var username = null;

var colors = [
  "#2196F3",
  "#32c787",
  "#00BCD4",
  "#ff5652",
  "#ffc107",
  "#ff85af",
  "#FF9800",
  "#39bbb0",
];

function connect(event) {
  username = document.querySelector("#name").value.trim();

  if (username) {
    usernamePage.classList.add("hidden");
    chatPage.classList.remove("hidden");

    var socket = new SockJS("/ws");
    stompClient = Stomp.over(socket);

    stompClient.connect({}, onConnected, onError);
  }
  event.preventDefault();
}

function onConnected() {
  // Subscribe to the Public Topic
  stompClient.subscribe("/topic/public", onMessageReceived);

  // Tell your username to the server
  stompClient.send(
    "/app/chat.addUser",
    {},
    JSON.stringify({ sender: username, type: "JOIN" })
  );

  connectingElement.classList.add("hidden");
}

function onError(error) {
  connectingElement.textContent =
    "Could not connect to WebSocket server. Please refresh this page to try again!";
  connectingElement.style.color = "red";
}

function sendMessage(event) {
  var messageContent = messageInput.value.trim();
  if (messageContent && stompClient) {
    var chatMessage = {
      sender: username,
      content: messageInput.value,
      type: "CHAT",
    };
    stompClient.send("/app/chat.sendMessage", {}, JSON.stringify(chatMessage));
    messageInput.value = "";
  }
  event.preventDefault();
}

function onMessageReceived(payload) {
  var message = JSON.parse(payload.body);

  var messageElement = document.createElement("li");

  if (message.type === "JOIN") {
    messageElement.classList.add("event-message");
    message.content = message.sender + " joined!";
  } else if (message.type === "LEAVE") {
    messageElement.classList.add("event-message");
    message.content = message.sender + " left!";
  } else {
    messageElement.classList.add("chat-message");

    var avatarElement = document.createElement("i");
    var avatarText = document.createTextNode(message.sender[0]);
    avatarElement.appendChild(avatarText);
    avatarElement.style["background-color"] = getAvatarColor(message.sender);

    messageElement.appendChild(avatarElement);

    var usernameElement = document.createElement("span");
    var usernameText = document.createTextNode(message.sender);
    usernameElement.appendChild(usernameText);
    messageElement.appendChild(usernameElement);
  }

  var textElement = document.createElement("p");
  var messageText = document.createTextNode(message.content);
  textElement.appendChild(messageText);

  messageElement.appendChild(textElement);

  messageArea.appendChild(messageElement);
  messageArea.scrollTop = messageArea.scrollHeight;
}

function getAvatarColor(messageSender) {
  var hash = 0;
  for (var i = 0; i < messageSender.length; i++) {
    hash = 31 * hash + messageSender.charCodeAt(i);
  }
  var index = Math.abs(hash % colors.length);
  return colors[index];
}

usernameForm.addEventListener("submit", connect, true);
messageForm.addEventListener("submit", sendMessage, true);
```

> #### **line 3~9:** html에서 명시된 id의 엘리먼트를 반환한다.<br>
>
> #### **line 11~12:** stompClient와 username를 전역변수로 선언한다.<br>
>
> #### **line 25:** line 120에서 html의 form에서 submit 버튼을 누르면 실행되는 함수이다.<br>
>
> #### **line 32:** SockJs 객체를 생성한다. 이때 우리가 WebSocketConfig.java에서 설정했던 엔드포인트를 넘겨준다.<br>
>
> #### **line 33:** 해당 SockJs 타입의 객체를 넘겨줌으로서 stompClient를 초기화한다. stomp<br>
>
> #### **line 35:** 연결이 성공적이면 onConnected 함수를 실행시키고 연결에 실패하면 onError 함수를 실행시킨다.<br>
>
> #### **line 42:** /topic/public으로 구독을 신청한다. 그리고 해당 경로로 메시지가 올 경우 onMessageReceived 함수를 실행시킨다.<br>
>
> #### **line 45:** 클라이언트가 새로 입장한 것이므로 컨트롤러에서 설정했던 /app/chat.addUser 경로를 통해 클라이언트 입장을 브로드캐스트한다.<br>
>
> #### **line 60:** line 121를 보면 브라우저에서 메시지를 보내는 버튼을 누를 경우 이 함수가 실행된다. <br>
>
> #### **line 61:** html에서 input 값을 가져온다.<br>
>
> #### **line 62~67:** 백엔드의 model 패키지에 있는 chatMessage 필드를 input값과 유저이름, 그리고 알맞는 메시지 타입으로 초기화한다.<br>
>
> #### **line 68:** 해당 경로로 그 메시지를 보낸다.<br>
>
> #### **line 71:** 새로고침을 방지하는 코드다.<br>
>
> #### **line 74:** /topic/public를 구독하는 클라이언트에게 메시지가 왔을 때 실행되는 함수이다.<br>

<br>

자 이제 앱을 실행해 보자. 아래 사진과 같이 Username를 입력하게 되면 채팅방에 참여하고 있는 모든 클라이언트들에게 방송된다.

![](../images/SpringBoot/websocket/2021-03-12-23-52-31.png)

<br>

username를 입력하고 채팅 시작하기를 누른다.

![](../images/SpringBoot/websocket/2021-03-12-23-53-30.png)

<br>

채팅방에 들어왔음을 볼 수 있다.

![](../images/SpringBoot/websocket/2021-03-12-23-53-42.png)

<br>

이제 새로운 탭을 키고 다시 접속해서 다른 username으로 접속해보자.

![](../images/SpringBoot/websocket/2021-03-12-23-54-21.png)

<br>

username이 Young인 클라이언트가 메시지를 보내는 화면이다.

![](../images/SpringBoot/websocket/2021-03-12-23-55-42.png)

<br>

username이 Sung인 클라이언트의 화면에 Young이 보낸 메시지가 보인다.

![](../images/SpringBoot/websocket/2021-03-12-23-56-06.png)

<br>

반대로 Sung에서 메시지를 보낸다.

![](../images/SpringBoot/websocket/2021-03-12-23-56-31.png)

<br>

다시 Young에서 확인해본다.

![](../images/SpringBoot/websocket/2021-03-12-23-56-49.png)

<br>

자 이렇게 간단한 채팅 프로그램을 만들어보았다.
나는 이제 이것을 응용해서 어떻게 실시간으로 데이터베이스의 상태를 확인하고 데이터가 업데이트될 때마다 바로 그래프에 표시하는 것을 고민 해봐야 한다. 좀 더 공부가 필요할 것 같다. 만약 해결책을 찾게 되면 그것에 관해 게시물을 올려봐야겠다.
