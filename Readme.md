# Spring web socket study

## 1. Web socket end-point & message broker 구성
###  config/WebSocketConfig.class
- @Configuration / Spring bean 설정
- @EnableWebSocketMessageBroker / WebSocket 서버 활성화
- registerStompEndpoints override method
    - 클라이언트가 웹 소켓 서버에 연결하는데 사용 할 웹 소켓 엔드포인트 등록
    - 엔드포인트 구성에 withSockJS() 사용
    - SocketJS는 웹 소켓을 지원하지 않는 브라우저에 Fallback 옵션을 활성화 하는데 사용
        - Fallback?
            - 어떤 기능이 약해지거나 제대로 동작하지 않을때, 이에 대처하는 기능 또는 동작
        - Stomp?
            - Spring 프레임워크 STOMP 구현에서 제공
            - Simple Text Oriented Messaging Protocol
            - 데이터 교환의 형식과 규칙을 정의하는 메시징 프로토콜
            - Stomp를 사용하는 이유
                - WebcSocket은 통신 프로토콜 일 뿐, 특정 주제를 구독한 사용자에게만 메시지를 보내는 방법 또는 특정 사용자에게 메시지를 보내는 방법과 같은 내용은 정의하지 않는다. 이러한 기능을 위해 STOMP가 필요함.
- configureMessageBroker override method
    - 한 클라이언트에서 다른 클라이언트로 메세지를 라우팅 하는데 사용될 메시지 브로커 구성
    - registry.setApplicationDestinationPrefixes
        - `/app` 시작되는 메세지가 message-handilng methods으로 라우팅되어야 하는것을 명시
    - registry.enableSimpleBroker
        - `/topic` 시작되는 메세지가 메세지 브로커로 라우팅 되도록 정의
        - 메세지 브로커는 특정 주제를 구독 한 연결된 모든 클라이언트에게 메세지를 broadcast
        - broadcast?
            - 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전송하는 방식을 의미
            - 현재 예제에서는 인메모리 메세지 브로커 활성해서 사용
            - RabbitMQ, ActiveMQ 메세지 브로커 연습 할 것!

## 2. domain/vo 구성
- enum class?
    - `Enumeration Type` 열거타입 이라고 하며 열거 타입에 들어가는 값들을 `Enumeration Constant` 열거 상수라고 한다.
