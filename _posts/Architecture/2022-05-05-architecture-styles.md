---
layout: post
title: Architecture Styles 14가지 정리
category: Architecture
tag: [Architecture, Architecture Style]
---

### 1. Batch Sequential Architecture Style
  - Batch 단위의 데이터를 하나의 컴포넌트에서 다른 컴포넌트로 전달한다.
  - 모든 데이터가 하나 끝나면 다음, 다음 끝나면 그 다음으로 이동한다.

  - **장점**
    1. 구성 요소를 재사용하기 쉽다.
    2. 유지 관리 및 새 구성 요소 추가 또는 교체 용이하다.
  - **단점**
    1. Interactive Interface를 제공하지 않는다.
    2. 순차 처리만 지원하기 때문에 throughput이 낮고 laytency가 높다.
    4. 사용자가 각 단계의 데이터를 넣고 뺄 수 없다.
    5. 병렬처리가 안된다.
  - **용도**
    1. 많은 양의 데이터 처리를 여러 단계로 나눌 수 있을 때
    2. 하나의 구성 요소로 전체 기능을 처리하기 어려울 때
    2. 여러 단계에서 데이터 세트를 조작해야 할 때    
    

### 2. Pipe and Filter Architecture Style
  - Steam 데이터를 처리할 수 있는 구조를 제공한다. 
  - Filter간 data의 이동은 pipes를 사용한다.
  - 여러 구성 요소가 병렬로 실행될 수 있다.

  - **장점**
    1. 병렬 처리를 통해 성능향상이 있다.
    2. 필터의 유지 보수 및 재사용이 용이하다.
  - **단점**
    1. 상태 정보를 공유하는 데 비용이 많이 들거나 유연하지 않음
    2. 필터간 데이터 이동/변환 오버헤드
    3. 에러 핸들링이 어려움
  - **용도**
    1. 데이터 스트림 작업 필요
    3. 사용자와의 상호 작용 지원


### 3. Layered Architecture Style
  - 특정 추상 레벨에 있는 모듈들을 묶어서 하나의 레이어 단위로 분류한다.
  - 상위 레이어는 하위 레이어에 서비스를 요청하고, 하위 레이어는 상위 계층에 서비스를 제공한다. 

  - **장점**
    1. 레이어 수정 및 재사용이 용이
    2. 계층을 통해 위로 이동할 때 추상화 수준 증가하여 복잡한 문제를 분할
    3. Good Separation of Concerns
    4. 레이어별 구현이 분리되어 있어 유지보수가 상대적으로 용이
  - **단점**
    1. 여러 계층의 호출로 인한 잠재적인 성능 저하 문제
    2. 적절한 추상화 수준을 찾아서 레이어를 나누기가 쉽지 않다.


### 4. Model View Controller (MVC) Architecture Style
  - 어플리케이션을 Model View Controller 세개의 컴포넌트로 구분하는 아키텍쳐

  - **장점**
    1. 여러 View가 단일 모델과 연결될 수 있다.
    2. 모델의 변경은 각 뷰에게 옵저버형태로 전달될 수 있다.
  - **단점**
    1. 간단한 프로그램일경우 복잡도가 증가한다.
  - **용도**
    1. 사용자 인터페이스의 여러 구현이 필요할 때
    2. GUI 응용 프로그램이 필요할 때


### 5. Blackboard Architecture Style
  - 명확하게 정의된 문제 해결 방법이 존재하지 않을 때 사용
  - Blackboard: Solution 정보와 데이터를 관리
  - Knowledge Source (KS): 부분 문제를 판단하고 결과를 도출하여 Blackboard 에 Update
  - Control: Blackboard 모니터링 중 KS 가 종료되면, 다음 Source 로 변경

  - **장점**
    1. 정확한 접근법이 존재하지 않을 때 다양한 알고리즘을 적용
    2. Knowledge Source 의 재사용이 가능
  - **단점**
    1. 결과값이 바뀔 수 있으며, 완벽한 해결책을 보장하지 않음
    2. 개발 및 테스트가 힘듦


### 6. Shared Repository Architecture Style
  - 모든 데이터는 중앙 데이터 저장소에서 관리되며, 여러 모듈이 접근

  - **장점**
    1. 여러 모듈이 데이터를 공유하기 쉽다.
    2. 데이터를 저장하기 편하고 무결성이 높다. 
  - **단점**
    1. 데이터 구조 변경이 어렵다. 
    2. 여러 클라이언트에서 접근하기 때문에 오버헤드가 발생한다.


### 7. Microkernel Architecture Style
  - 시스템의 핵심적이고 공통적인 기능을 코어에 구현하고 각 기능 모듈은 Plugin 시키는 아키텍쳐

  - **장점** 
    1. 새로운 기능들을 유연하게 추가할 수 있다.
  - **단점**
    1. 호환성을 위한 Plugin 검증 필요
    2. 복잡한 설계 구현
  - **용도**
    1. Eclipse 처럼 Plugin 으로 모듈이 추가되어야 할 때


### 8. Microservice Architecture Style
  - 하나의 큰 시스템을 독립적으로 동작 가능한 여러개의 작은 어플리케이션으로 나누어 변경과 조합이 가능하도록 만든 아키텍쳐
  - 필요한 컴포넌트들이 이미 마이크로 서비스로 존재할 때 사용
  
  - **장점**
    1. 개발 테스트 및 유지보수에 드는 시간과 비용이 절감
    2. 개별 모듈을 병렬로 개발
  - **단점**
    1. 네트워크 통신으로 인한 오버헤드 발생
    2. 마이크로 서비스 하나의 오류가 전체 시스템으로 전파


### 9. Dispatcher Architecture Style
  - Dispatcher 가 서버정보를 클라이언트에게 전송해서 클라이언트가 직접적으로 서버를 호출하는 구조

  - **장점**
    1. 문제가 있는 노드는 제외하고 작업을 요청한다.
    2. 가용성과 학장성이 좋아진다.
    3. High availability, reliability, scalability
  - **단점**
    1.  Single dispatcher 구조일때 failure가 발생하면 전체 이슈로 연결
  - **용도**
    1. 분산처리 환경에서 여러 대의 서버에서 서비스를 받고자 할 때
    2. 로드밸런싱에 사용

  
### 10. Broker Architecture Style
  - Broker 에 등록된 서버와 클라이언트 사이에서 통신을 중계한다.
  - 독립적으로 통신을 핸들링한다.
  - 같은 서버를 복사해서 사용한다.

  - **장점**
    1. 클라이언트와 서버를 Decoupling 시켜 확장이 가능하다.
    2. 런타임에 서버 변경이 가능하다.
  - **단점**
    1. Broker 에 문제가 발생하면 전체 통신에 영향을 준다.
    2. 클라이언트와 서버의 통신에 관여하기 때문에 비효율이 있으며 오버헤드가 발생할 수 있다.
    3. Lower fault tolerance
  - **용도**
    1. 하둡에서 Mapper Reduce 방식으로 동일한 데이터를 최소한 세곳에 복사를 해두고 병렬처리 해서 다시 취합한다.


### 11. Client Server Architecture Style
  - 서비스를 요청하는 클라이언트와 서비스를 제공하는 서버로 구성되어 있다.
  - 커뮤니케이션은 클라이언트에서 시작된다.
  
  - **장점**
    1. 기능을 서버와 클라이언트로 분리하여 독립적인 기능을 할 수 있다.
    2. 복잡하거나 민감한 처리를 중앙집중화할 수 있다.
  - **단점**
    1. 서버의 fault가 통신하는 전체 클라이언트에게 영향을 준다.


### 12. Master-Slave Architecture Style
  - Master 에 함수를 요청하면 Slaver 노드에게 각각 일을 맡기고 취합해서 리턴해준다.
  - Slave 노드는 Replication이 아니다. 각각의 고유 로직이 있다.
  
  - **장점**
    1. 분산 컴퓨팅이 가능하다.
    2. 모든 Slave는 병렬로 실행 가능하다.
    3. 부정확한 결과는 다수의 Voting 전략으로 쉽게 제외할 수 있다

### 13. Edge-Based Architecture Style
  - Edge들이 동적으로 식별하여 일을 엣지들에게 나눠서 요청한다.
  - 퍼블릭으로는 힘드나 인트라넷 내에서는 사용할 수 있다.

### 14. Publish and Subscribe Architecture Style
  - 특정 이벤트가 발생할 경우 다른 서비스에게 알린다.
  - Observer 패턴과 유사하나 중간에 Message Broker 또는 Event Bus 가 있다

  - **장점**
    1. 게시자와 구독자는 서로 Decoupling 된다
    2. Message Broker 가 Queue 역할을 하여 Subscriber는 Publisher 의 상태를 확인하지 않아도 된다.