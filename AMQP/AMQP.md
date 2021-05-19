AMQP
===============

## AMQP란?

정의 : 메세지 지향 미들 웨어를 위한 표준 응용 계층 프로토콜


## 등장 배경
- 플랫폼 종속적인 제품들 사이에서 서로 다른 이기종간에 메세지를 교환하기 위해서는 
  메세지 포멧 컨버전을 위한 메시지 브릿지(속도 느림)를 이용하거나 시스템 자체를 통일 시켜야 하는
  불편함과 비효율성이 있었다.
 
  -> 서로 다른 시스템들 간의 최대한 효율적인 방법을 교환하기 위한 AMMQ 프로토콜의 등장
  

## AMQP 특징
- 모든 broker들은 똑같은 방식으로 동작할것
- 모든 client들은 같은 방식으로 동작할것
- 네트워크상으로 전송되는 명령어들의 표준화
- 프로그래밍 언어 중립적


## AMQP Routing model

- component 구성
   - Exchange
   - Queue
   - Binding 



![AMQP](./image/AMQP.png)


- Exchange
  
  - 메세지 브로커에서 큐에 메세지를 전달하는 역할

- Queue
  
  - 메모리나 디스크에 메시지를 저장하고, 그것을 consumer에게 전달하는 역할
  - 스스로가 관심있는 메시지 타입을 지정한 Binding을 통해 exchange에 말그대로 bind된다.

- Binding
  
  - Exchange에 전달된 메세지가 어떤 큐에 저장되어야 하는지 정의
  

## Standard Exchange Type

- Direct Exchange

  - 메세지의 라우팅 키를 큐에 1:1으로 매칭 시키는 방법
  - 라운드 로빈 방으로 여러 Consumer간 task 분

- Topic Exchange  
  
  - 와일드카드를 이용해서 메세지를 큐에 매칭시키는 방법
  - MultiCast 방식에 적합  
  - 라우팅 키는 ","으로 구분된 0개 이상의 단어의 집합으로 간주 되고 와일드카드 문자들을 이용해 특정 큐에 바인딩
  - '*' : 하나의 단어
  - '#' : 0개 이상의 단어

- Fanout Exchange

  - 모든 메세지를 모든 큐로 라우팅 하는 유형
  - 1:N 방식으로 메세지를 브로드캐스트 하는 용도로 사용
  
- Headers Exchange

  - key-value로 정의된 헤더에 의해 라우팅을 결정한다.
  - 큐를 바인딩 할때 x-match라는 특별한 argument로 헤더를 어떤식으로 해석하고 바인딩 할지를 결정함 
    - all : 모두 충족 시켜야 함 (and)
    - any : 하나만 충족시키면 된다. (OR) 


## AMQP의 사용

### RabbitMQ

- 신뢰성 , 안정성
- 유연한 라우팅 (Message Queue가 도착하기 전에 라우팅 되며 플러그인을 이용해서 더 복잡한 라우팅 가능)
- 클러스터링 (로컬네트워크에 있는 여러 RabbitMQ 서버를 논리적으로 클러스터링 할수 있음)
- 관리 UI의 편리성 (관리자 페이지 및 모니터링 페이지 제공)
- 거의 모든 언어 및 운영체제 지원
- 오픈소스로서 상업적 지원 가능

### ActiveMQ

- 다양한 언어와 프로토콜 지원 (JAVA, C, C++, C#, Ruby, Peri, Python, PHP 클라이언트)
- OpenWire을 통해 고성능의 JAV, C, C++, C# 클라이언트 지원
- Stomp를 통해 C, Ruby, Peri, Python,PHP 클라이언트가 다른 인기 있는 메세지 브로커들과 마찬가지로 ActiveMQ에 접근 가능
- Message Groups, Virtual Destinations, Wildcards와 Composite Destination을 지원
- Spring 지원으로 ActiveMQ는 Spring Application에 매우 쉽게 임베딩될 수 있으며, Spring의 XML 설정 메커니즘에 의해 쉽게 설정 가능
- Geronimo, JBoss 4, GlassFish, WebLogic과 같은 인기있는 J2EE 서버들과 함께 테스트됨
- 고성능의 저널을 사용할 때에 JDBC를 사용하여 매우 빠른 Persistence를 지원
- REST API를 통해 웹기반 메시징 API를 지원


### ZeroMQ

- 분산/동시성 에플리케이션에 사용하도록 개발됨
- 라이브러리의 API는 버클릿 소켓의 API 설계와 유사
- 메세지 지향 미들웨어와 달리 메세지 브로커 없이 동작이 가능 (크로스 플랫폼으로 동작 가능)

- 뛰어난 확장성
- 훌륭한 퍼포먼스
- 단순

- 패턴
  - Request-reply : 클라이언트와 서비스의 집합을 연결하는 패터
  - Publish-subscribe : publisher와 subscriber 집합을 연결하는 패턴
  - Pipeline : Push/Pull 소켓 쌍으로 단방향 통신에 이용

- 유효한 소켓 조합
  -  

### Apache Kafka

- 대용량 실시간 로그 처리에 특화되어 있다.
- AMQP 프로토콜이나 JSM API를 사용하지 않고 단순한 메세지 헤더를 지닌 TCP 기반 프로토콜을 사용하므로서 오버헤드가 비교적 작다.
- 노드 장애에 대한 대응성을 가지고 있다.
- 프로듀서는 각 메세지를 배치로 브로커에 전달하며 TCP/IP 라운드 트립을 줄였다.
- 메세지를 기본적으로 파일 시스템에 저장하여 별도의 설정을 하지 않아도 오류 발생시 오류 지점부터 복구가 가능 (기존 메세징 시스템은 메시지를 메모리에 저장)
- 메시지를 파일 시스템에 저장하기 떄문에 메세지가 많이 쌓여도 기존 메세징 시스템에 비해 성능이 크게 감소하지 않는다.
- window 단위의 데이터를 넣고 꺼낼수 있다.

출처 : http://egloos.zum.com/killins/v/3025514
출처 : https://12bme.tistory.com/176