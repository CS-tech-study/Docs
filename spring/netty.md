# Tomcat vs. Netty

## Tomcat 간단 비교

- Spring MVC에서 사용
- 서블릿 API 기반
- 동기 방식으로 요청/응답 처리

## Netty

- WebFlux에서 사용
- 이벤트 기반
- 비동기 및 논블로킹 방식으로 동작

### 이벤트기반
![](/spring/images/event-loop-hierachy.png)

**#### EventLoopGroup**

- 여러 개의 이벤트 루프를 포함하는 컨테이너
- 일반적으로 두 개의 이벤트 루프 그룹을 사용합니다
    - **부모 그룹 (BossGroup):** 클라이언트의 연결 요청을 수락하고, 새로운 채널을 생성합니다.
    - **자식 그룹 (WorkerGroup):** 생성된 채널에 할당되어 실제 I/O 작업과 이벤트 처리를 담당합니다.

**#### EventLoop**

- 네트워크 이벤트를 처리하기 위한 단일 스레드
- N개의 채널에 할당되어 할당된 채널에서 발생하는 모든 이벤트를 처리합니다. 이를 통해 스레드 간 컨텍스트 스위칭을 최소화하고, 이벤트 처리의 순서를 보장합니다.
    
    ![](/spring/images/netty-eventloop.png)

**#### Channel**

- 네트워크 소켓 또는 연결을 추상화한 객체