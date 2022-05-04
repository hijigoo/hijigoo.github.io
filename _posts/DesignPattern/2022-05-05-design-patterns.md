---
layout: post
title: 디자인 패턴 23개 요약 정리
category: Design Pattern
tag: [디자인 패턴]
---

### Behavioral
클래스와 객체들이 상호작용하는 방법 및 역할을 분담하는 방법과 관련된 패턴이다.
### Creational
객체 인스턴스 생성을 위한 패턴으로, 클라이언트와 그 클라이언트에서 생성할 객체 인스턴스 사이의 연결을 끊어주는 패턴이다.
### Structure
클래스 및 객체들을 구성(합성)을 통해서 더 큰 구조로 만들 수 있게 해주는 것과 관련된 패턴이다.


#### 1. Strategy Pattern (#알고리즘 #Family #캡슐화 #교환)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 같은 계열(familiy)의 알고리즘군을 정의하고, 각각의 알고리즘을 캡슐화하여 교환해서 사용할 수 있도록 만든 패턴 
       알고리즘 -> Strategy
    2. 컨텍스트 코드의 변경 없이 새로운 알고리즘을 독립적으로 추가할 수 있다.
    3. 같은 계열의 알고리즘군을 정의하고, 각각의 알고리즘을 캡슐화하여 교환해서 사용할 수 있도록 만든 패턴.
  - When: 
    1. Runtime에 동적으로 알고리즘을 변경하고자할 떄
    2. 관련된 클래스들에서 behavior(알고리즘) 의 차이만 있을 때
    3. 알고리즘의 여러 버전이나 다양성이 요구될 때
    4. 조건문이 복잡하고 유지하기 어려울 때


#### 2. Observer Pattern (#Subject #상태변경 #Observer #감지)
  - Type: Behavioral
  - Purpose(Benefit)
    1. Observer 가 Subject 의 상태 변경을 알 수 있도록 만든 패턴
    2. 주체(Subject)의 변경이 일어났을 때 감시자(Observer)에게 알려주어 변화되어야 하는 객체들에게 전달(Update)
  - Benefit
    1. Subject 의 변경사항을 Observer에게 알려줄 수 있다.
    2. Loose Coupling 으로 시스템이 유연하고 객체간의 의존성을 제거할 수 있다.
  - When:
    1. 객체의 변화에 관심있는 객체들이 누구인지 가정없이 통보가 이뤄져야 할 때 
    2. 커뮤니케이션을 위한 Loose Coupling 이 필요할 떄 
    3. 하나 이상의 객체의 상태 변경이 다른 객체의 동작을 트리거해야할 때
    4. Broadcasting 기능이 필요할 떄

#### 3. Template Method Pattern (#구조유지 #단계정의 #자식클래스)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 알고리즘의 구조는 유지하고, 알고리즘의 각 단계의 처리를 서브 클래스의
       Template Mathod에서 재정의할 수 있게 하는 패턴
  - When: 
    1. 알고리즘의 구조/흐름은 유지하고 각 단계의 구현의 변경이 필요할 때.
    2. 부모 클래스가 여러 자식 클래스의 behavior 를 동일하게 호출할 수 있을 때
  - 기타:
    1. "Hollywood Principle" 와 연관(부모만 자식을 호출))
    2. Template Mathod 는 inheritance, Strategy 는 delegation 을 사용
    3. Factory Method 는 Template Mathod 의 변경한 패턴

#### 4. Iterator Pattern (#내부표현 #노출X #객체순회)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 내부 표현(interface)은 노출하지 않고 어떤 객체 집합에 속한 원소들을
      Iterator 를 통해 순차적으로 접근할 수 있는 방법을 제공.
  - When: 
    1. 다양한 클래스의 객체(ArrayList, List[]) 가 순회를 위해 동일한 인터페이스가 필요할 때. 
  - 기타:
    1. "Single Responsibility Principle" 과 연관
    2. 오직 순회만을 위해 사용
    3. Aggregate 가 iterator를 생성한다.

#### 5. State Pattern (#State변경 #Behavior변경)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 객체의 내부 상태의 변환에 따라서 객체의 행동(Behavior)를 바꾸는 패턴.
  - When: 
    1. 각 상태간의 전환이 명확하고 해당 상태에 따라 각기 다른 행동(Behavior)이 런타임에 결정될 때.
  - 기타:
    1. State Pattern: (하나의 클래스 객체 안에서 )상태에 의존적인 behavior 를 캡슐화, 주로 if 문대체
    2. Strategy Pattern : (클래스마다 분기되는) 알고리즘을 캡슐화, 주로 subclassing을 대체
    3. 둘 다 Compositon/Delegation 사용

#### 6. Mediator Pattern (#Colleague #상호작용 #Mediator #정리)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 객체들(Colleague) 간의 상호작용 행위를  Mediator 객체를 따로 두어 관라히는 디자인 패턴
    2. 객체들 간 참조하지 않도록 함으로써 객체를 수정하지 않고 관계를 수정할 수 있습니다.
    3. 객체들간의 관계의 복잡도, 의존성 및 결합도를 감소시킵니다.
    4. 한 집합에 속해있는 객체들의 상호작용을 캡슐화하는 객체를 정의하는 패턴.
  - When:
    1. 객체간의 상호작용이 복잡하고, 객체들간의 의존성을 이해하기 어려울 때
    2. 많은 관계가 존재하고 관계들을 제어하는 중제자가 필요할 때.
  - 기타:
    1. GUI 에서 많이 사용된다.

#### 7. Chain of Responsibility Pattern (#Handler #요청처리 #요청전달)
  - Type: Behavioral
  - Purpose(Benefit)
    1. Handler chain에 따라 요청을 전달할 수 있는 디자인 패턴입니다.
    2. 요청을 수신한 각 핸들러는 요청을 처리하거나 다음 핸들러로 전달할지 결정
    3. 요청을 처리할 수 있는 기회를 하나 이상의 객체에게 부여하여 요청을 보내는 객체와 그 요청을 받는 객체 사이의 결합을 피하는 패턴.
        요청을 받을 수 있는 객체를 연쇄적으로 묶고, 실제 요청을 처리할 객체를 만날 때까지 객체 고리를 따라서 요청을 전달.
  - When:
    1. 유사한 이벤트를 처리하지만 이벤트의 타입, 속성, 기타 항목에 따라 달라지는 객체 그룹이 있을 때 사용
    2. 클라이언트는 최종으로 누가 요청을 처리해야할지 알 수 없을 때

#### 8. Command Pattern (#요청 #객체로캡슐화 #전달)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 요청을 객체로 캡슐화하는 패턴
    2. 요청을 객체의 형태로 캡슐화할 수 있으며 매개변수를 사용해서 서로 다른 요청을 넣을 수 있음.
        또한, 요청 내역 저장 또는 로그 기록, 그리고 작업 취소(Undo)를 지원하게 만드는 패턴.
  - When:
    1. request자체를 객체로 만들어서 관리하자
    2. 요청을 모아두고 필요할 때 실행할 수 있다
    3. 히스토리 관리를 할 수 있다
    4. 요청을 하는 쪽과 요청을 받는 쪽을 분리하고 싶을 때
  - 기타:
    1. Invoker - 요청을 보내는 쪽
    2. Receiver - 요청을 받는 쪽
    3. Command - 요청
    4. Command 를 저장, 수행, 실행, 취소 등 별도 관리 가능

#### 9. Interpreter Pattern (#언어 #컴파일역할 #해석정의)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 컴파일러 역할을 하며 해결하고자 하는 것을 미니 언어로 표현
    2. 주어진 언어에 대해, 그 언어의 문법을 위한 표현 수단을 정의하고,
        그 표현 수단을 사용하여 해당 언어로 작성된 문장을 해석하는 해석기를 정의하는 패턴.
  - When:
    1. 정의할 언어의 문법이 간단할 때

  - 기타:

#### 10. Memento Pattern (#상태저장 #복원)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 객체의 상태 정보를 저장하고 사용자의 필요에 의하여 원하는 시점의 데이터를 복원 할 수 있는 패턴
  - When:
    1. 이전의 상태를 기억해야 할 때
  - 기타:
    1. Caretaker: 상태 정보가 저장되어 있는 Memento 들을 관리하는 클래스
    2. Memento: 특정 시점의 상태를 저장하는 클래스
    3. Originator : Caretake의 요청을 받아 Memento 객체를 생성하는 클래스

#### 11. Visitor Pattern (#Element방문 #Visitor #로직처리)
  - Type: Behavioral
  - Purpose(Benefit)
    1. 실제 로직을 가지고 있는 객체(Visitor)가 로직을 적용할 데이터 객체(Element)를 방문하면서 실행하는 패턴이다
    2. 객체 구조를 이루는 원소에 대해 수행할 연산을 표현하는 패턴.
        새로운 연산을 적용할 원소의 클래스를 변경하지 않고도(구조 변경 없이) 새로운 연산을 정의(새로운 기능 추가)할 수 있게 한다.
  - When:
    1. 로직과 구조를 분리해야 할 때
    2. Visitor 가 처리를 담당한다. 
    3. 새로운 로직을 추가하고 싶으면 새로운 방문자(Visitor) 필요.
  
#### 12. Factory Method Pattern (#객체생성 #subclass담당)
  - Type: Creational
  - Purpose(Benefit)
    1. 객체 생성 프로세스를 서브 클래스로 분리하여 캡슐화하는 패턴.
    2. Method 를 통해서 new 키워드 없이 객체를 생성 할 수 있다.
    3. 객체 생성 메서드 인터페이스는 부모 클래스에서 정의하지마 실제 생성하는 객체는 자식 클래스에서 결정.
    4. 객체를 생성하는 인터페이스는 미리 정의하되, 인스턴스를 만들 클래스의 결정은 서브클래스 쪽에서 내리는 패턴. 
  - When:
    1. 부모 클래스가 아닌 자식클래스가 어떤 객체를 생성해야할지 알고 있을 때
    2. 객체 생성의 세부 내용을 노출하고 싶지 않을 때.
  - 기타:
    1. Template method 패턴의 변형이라고도 한다.

#### 13. Abstract Factory Pattern (#객체Family #생성)
  - Type: Creational
  - Purpose(Benefit)
    1. 관련이 있는 객체들의 집합(familiy)을 생성해야 할 때 사용하는 패턴. 
    2. 구체적인 클래스를 지정하지 않고 관련성을 갖는 객체들의 집합, 서로 독립적인 객체들의 집합을 생성할 수 있는 인터페이스를 제공하는 패턴.
  - When:
    1. 다양한 종류의 객체들의 집합(famillies)이 있으며 객세 생성이 상황에 따라 바뀌어야 할 때.
    2. 객체 생성의 세부 내용을 노출하고 싶지 않을 때.
  - 기타:
    1. Factory method - inheritance 사용
    2. Abstract factory - composition 사용
  
#### 14. Builder Pattern (#복잡한객체 #동일한절차 #구성요소 #다른표현 #생성방법)
  - Type: Creational
  - Purpose(Benefit)
    1. 여러가지 빌더가 같은 구성 요소 가지고 서로 다른 방법으로 구축할 떄 사용하는 패턴
    2. 구조를 가진 인스턴스를 쌓아 올리는 패턴
    3. 복합 객체의 생성과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴.
  - When:
    1. 같은 구성 요소 (part)를 가지지만, 각 구성 요소가 다른 방법으로 구축되는 경우 적용.
    2. 런타임에 생성 프로세싱이 결정
    3. 각 생성 프로세싱에 다양한 알고리즘이 필요.
    4. 객체 생성 알고리즘이 시스템과 디커플링되어야 할 때 필요
    5. 핵심 코드를 변경하지 않고 새로운 생성 기능을 추가할 때 필요.

#### 15. Singleton Pattern (#시스템 #오직하나)
  - Type: Creational
  - Purpose(Benefit)
    1. 시스템에서 클래스의 한 인스턴스만 허용되도록 합니다.
    2. 어떤 클래스의 인스턴스는 오직 하나임을 보장하며, 이 인스턴스에 접근할 수 있는 전역적인 접촉점을 제공하는 패턴.
  - When:
    1. 클래스의 정확히 하나의 인스턴스가 필요할 때 
    2. 단일 개체에 대한 제어된 액세스가 필요합니다.

#### 16. Prototype Pattern (#기존객체 #복사)
  - Type: Creational
  - Purpose(Benefit)
    1. 기존존재하는 객체를 복사해서 새로운 객체를 만들는 패턴.
    2. 클래스 안에 자신을 복사하는 메소드를 두자.
    3. 생성할 객체의 종류를 명시하는 데에 원형이 되는(Prototypical) 객체를 이용하고,
        그 원형을 복사함으로써 새로운 객체를 생성하는 패턴.
  - When:
    1. 동일한 객체를 복사해야 할 때 사용
  - 기타:

#### 17. Decorator Pattern (#상속X #Wrapping #Responsiblity #Behavior #추가덧붙임)
  - Type: Structure
  - Purpose(Benefit)
    1. 기존 책임(responsibility)과 동작(behavior)을 수정하기 위해 개체를 동적으로 래핑(dynamic wrapping)할 수 있습니다.
    2!. 주어진 상황 및 용도에 따라 어떤 객체에 책임을 덧붙이는 패턴.
        기능 확장이 필요할 때 서브클래싱 대신 쓸 수 있는 유연한 대안이 될 수 있습니다.
  - When:
    1. subclassing 으로 추가가 거의 불가능할떄
    2. 객체 책임과 행동은 동적으로 수정 가능해야 할 때
    3. 구체적인 구현(implementation)은 책임과 행동에서 분리되어야 할 떄
    4. 구체적인 구현을(implementation)) 둘러싼 많은 작은 개체가 허용되어야 할 때
  - 기타:
    1. Composite 패턴은 트리 구조
    2. Decorator는 둘러 쌓는 구조
    3. Composition 과 Delegation 을 모두 사용
    4. mirrors: 장식자와 장식대상이 같은 최상위 부모를 가짐으로써 인터페이스가 같다. 타입이 같다.

#### 18. Adapter Pattern (#서로다른 #Coller #Collee #인터페이스 #맞춤)
  - Type: Structural
  - Purpose(Benefit)
    1. 서로 다른 인터페이스가 있는 클래스가 통신하고 상호 작용할 수 있는 공통 개체를 만들어 함께 작동하도록 허용
  - When:
    1. 사용할 클래스가 인터페이스 요구 사항을 충족하지 않을 때
    2. caller 객체와 callee 객체가 사용하려는 인터페이스가 mismatch 날 때 맞춰주기 위해 사용한다.
  - 기타:
    1. Object Adapter: Composition을 이용한 일반적인 사용 방법
    2. Class Adapter: Target과 Adaptee 를 상속

#### 19. Composite Pattern (#부분-전체 #계층 #표현 #트리구조)
  - Type: Structural
  - Purpose(Benefit)
    1. 객체들이 하이라키를 가져서 트리 구조로 만들 때 사용
    2!. 객체들의 관계를 트리구조로 구성하여 부분-전체 계층을 표현하는 패턴.
        사용자가 단일 객체와 복합 객체 모두 동일하게 다루도록 허용
  - When:
    1. 객체의 계층적 표현이 필요합니다.
    2. Object와 Object 의 compositions들이 동일하게 다루어야 한다
  - 기타:
    1. composite iterator 는 DFS로 동작한다.
    2. Component가 함수를 모두 가지고 있기 때문에 리프에 필요 없는 기능도 호출할 수 있는 위험이 있다.

#### 20. Bridge Pattern (#추상계층 #구현게층 #분리)
  - Type: Structural
  - Purpose(Benefit)
    1. abstract 계층과 implementation 계층이 분리 되어 클라이언트는 abstract 계층을 보고 동작시킨다.
    2. abstraction 과 implementation이 디커플링이 된다.
    3. !구현부에서 추상층을 분리하여 각자 독립적으로 변형할 수 있게 하는 패턴.
        추상적 개념과 이에 대한 구현 사이의 지속적인 종속 관계를 피하고 싶을 때 사용.
        추상적 개념과 구현 모두가 독립적으로 서브클래싱을 통해 확장되어야 할때 사용.
  - When:
    1. 추상화 및 구현은 컴파일 타임에 바인딩되어서는 안 될 때
    2. 추상화 및 구현은 독립적으로 확장 가능해야 할 때
    3. 추상화 구현의 변경 사항은 클라이언트에 영향을 미치지 않아야 할 때
    4. 구현 세부 정보는 클라이언트에서 숨겨야 할 떄 

#### 21. Facade Pattern (#복잡한Subsystem #하나의Interface)
  - Type: Structural
  - Purpose(Benefit)
    1. 시스템에 인터페이스가 여러개 있을 때 하나의 인터페이스로 정리(창구) 해주는 패턴
    2. 서브시스템에 있는 인터페이스 집합에 대해서 하나의 통합된 인터페이스를 제공하는 패턴.
        서브시스템을 좀 더 사용하기 편하게 만드는 상위 수준의 인터페이스를 정의합니다.
  - When:
    1. 너무 많은 인터페이스가 존재할 떄 초보자가(?) 쉽게 사용할 수 있도록 만든다
    2. 서브시스템의 내부 구조는 숨겨주는 역활을 한다.
    3. 클라이언트와 내부의 서브 시스템의 커플링이 약해진다.
    4. 복잡한 내부 인터페이스 접근을 막는건 아니다/ 새로운 기능을 추가하는 것도 아니다.
    5. Facade 객체를 하나 만들어서 사용하기 쉽게 바꾼다.
  - 기타:

#### 22. Flyweight Pattern (#대량의객체 #공유)
  - Type: Structural
  - Purpose(Benefit) 
    1. 공유(Sharing)'를 통하여 대량의 객체들을 효과적으로 지원하는 패턴
    2. 이미 만들어진 객체를 공유해서 불 필요한 객체 생성을 막는 패턴
    3. 크기가 작은 객체가 여러 개 있을 때, 공유를 통해 이들을 효율적으로 지원하는 패턴.
  - When:
  - 기타:

#### 23. Proxy Pattern (#RealObject #가상ProxyObject #흐름제어)
  - Type: Structural
  - Purpose(Benefit)
    1. 실제 기능을 수행하는 Real Object 대신 가상의 Proxy Object를 사용해 로직의 흐름을 제어하는 디자인 패턴
    2. 어떤 다른 객체로 접근하는 것을 통제하기 위해서 그 객체의 대리자(Surrogate) 또는 Placeholder를 제공하는 패턴.
  - When:
    1. 가상 프록시: 생성하기 힘든, 비용이 많이 드는 객체를 캐시해 놓았다가 용
    2. 원격 프록시: 표현되는 객체가 시스템 외부에 있을 때, 내부에 있는 것처럼 사용할 때
    3. 보호 프록시: 원본 개체에 대한 액세스 제어가 필요할 때
  - 기타:
    1. caller와 callee가 decoupling 되어 있기 때문에, callee 객체가 변경되더라도 caller가 영향받지 않는다.
    2. caller로 부터 callee identity를 감출 수 있다.
    3. 어댑터: 서브젝트에 대한 인터페이스 차이를 극복 (새로운 객체에 다른 인터페이스를 랩핑)
    4. 데코레이터: 같은 인터페이스에 기능이 추가(additional behavior)
    5. 프록시: 인터페이스는 똑같다, (다른 객체를 랩핑해서 접근을 컨트롤)
