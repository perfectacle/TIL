---
title: HTTP/2와 Websocket, SSE
date: 2018-11-18 23:47:21
tags: [Websocket]
---

## HTTP
기본적으로 HTTP는 정보 공유를 위해 설계된 프로토콜이다.  
따라서 최대한 많은 사람의 접속을 허용해야한다.  
하지만 서버의 자원은 한정적이고, 한정적인 자원은 효율적으로 써야한다.  
돈이 많다면 서버의 스펙을 늘리거나, 서버의 장비를 늘리거나 돈으로 때려박으면 되지만...  
여튼 클라이언트와 계속 커넥션을 맺어놓으면 해당 클라이언트와 다시 커넥션을 맺을 필요가 없어서 비용 낭비는 줄일 수 있겠지만  
idle connection이 많아지면 많아질 수록 이 또한 비용 낭비 문제로 이어지고,  
idle connection이 많아져서 생기는 비용이 해당 클라이언트와 다시 커넥션을 맺는 비용 보다는 더 클 것이다.  
만약 동접 100명만 허용하는 서버가 있는데, idle connection을 가차없이 짤라버린다고 하면 동접을 10000명까지 늘릴 수도 있을 것이다.

이런 식으로 최대한 많은 사람을 수용하도록 하다보니 idle connection은 가차없이 짤라버린다.  
그럼 idle의 기준은 무엇일까?  
바로 요청에 대한 응답이 이뤄졌으면 바로 idle이라고 생각하고 커넥션을 바로 끊어버리는 것이다.  
따라서 유저가 페이지에 접속했을 때 3개의 요청이 **연달아** 있다면 3번의 커넥션(3 Way Handshake)이 이뤄져야한다.  

위와 같이 유저가 페이지에 접속했을 때 3개의 요청을 **연달아** 하는동안 3번의 커넥션이 이뤄지는 건 비용낭비 측면에서 좋지 않다.
물론 유저가 1명있을 때는 체감하지 못하겠지만 많아진다면...  
여튼 이런 경우를 대비해 **Connection 헤더에 Keep-Alive 값(Connection: Keep-Alive)**을 줘서 이 요청에 대해서 **바로 연결을 끊지 말라**라는 지시를 내리게 된다.  
또한 **Keep-Alive 헤더에 조건을 줘서 해당 조건일 때만 커넥션을 끊지 말라(Keep-Alive: timeout=5, max=1000 => 커넥션은 최소 5초간, 1000개의 요청까지 유지)**고 지시할 수도 있다.

## HTTP 1.0의 한계  
하지만 HTTP 1.0에서는 지속적인 연결에 대한 고려가 되어있지 않았고, Keep-Alive 헤더가 표준이 아니다보니 서버/클라이언트마다 동작이 제각각이었다.  
또한 요즘 많이 사용하는 progressively render(응답이 다 오기 전까지 기다리는 게 아니라, 응답이 온 만큼만 뿌려주는 방식)를 위해 사용하는
**Transfer-Encoding 헤더의 chunked**를 사용하기 위해서는 Content-Length 헤더가 필수이다. (표준이 아니다보니 어쩔 수 없나보다.)  
그 Content-Length를 토대로 각 응답을 구분하는 모양이다. 

## HTTP 1.1의 한계
HTTP 1.1에서는 [Keep-Alive](https://tools.ietf.org/html/rfc7230#appendix-A.1.2), [Transfer-Encoding](https://tools.ietf.org/html/rfc7230#section-3.3.1)이 표준으로 자리잡아서  
위에서 제시한 문제들은 해결이 되었다.  
하지만 여전히 문제는 존재했다.  
1. 커넥션(3 Way Handshake)만 다시 맺지 않는다 뿐이지, 매번 요청을 날리긴 해야한다.  
2. Keep-Alive의 조건이 끝난 경우에는 추후에 또 다시 커넥션을 맺어야한다.  
3. 서버에서 클라이언트로 메세지를 푸시할 수 없다.  

## HTTP/2 vs Websocket vs SSE(Server-Sent Events)
1. HTTP/2  
위에 제시한 1번과 3번의 문제를 해결했다.  
static file을 주로 서빙한다고 생각하면 된다.  
json을 주고받는 api는 Websocket이나 SSE가 담당한다고 보면 될 듯...  
2. Websocket  
위에 제시한 1, 2, 3번의 문제를 해결했다.  
클라 <-> 서버 쌍방향 통신이 가능하다.  
Websocket은 굉장히 정보가 적고 Low Level이다.  
따라서 Websocket은 확장성을 고려해 [sub-protocol](https://tools.ietf.org/html/rfc6455#section-1.9)에 대한 내용이 있고,  
Websocket의 High Level인(sub-protocol인) [STOMP](https://stomp.github.io/)와 같은 걸 사용해보면 좀 더 사용하기가 쉬울 것이다.  
Websocket은 간단한 메세지만 주고 받아야지 file의 전송은 무리일 것이다.
3. SSE  
위에 제시한 1, 2, 3번의 문제를 해결했다.  
하지만 클라 <- 서버 단방향 통신이다.  
서버에서 보내기만 할 수 있다.  
SSE는 간단한 메세지만 push해야지 file의 전송은 무리일 것이다.
