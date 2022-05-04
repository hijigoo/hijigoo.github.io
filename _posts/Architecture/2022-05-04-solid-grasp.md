---
layout: post
title: SOLID & GRASP
category: Architecture
tag: [SOLID, GRASP]
---

# SOLID
### 0. SOLID 장점
  - 시스템에 새로운 요구사항이나 변경사항이 있을 때, 영향을 받는 범위가 적은 구조로 만든다.
  - 소프트웨어를 설계함에 있어 이해하기 쉽고, 유연하고, 유지보수가 편하도록 도와준다.
  - 시간이 지나도 유지 보수와 확장이 쉬운 시스템을 만들고자 할 때 이 원칙들을 함께 적용할 수 있다.

### 1. Single-Responsibility Principle (SRP)
  - **정의**
    - A class should have one, and only one, reason to change
    - 각 모듈은 하나의 책임만 가진다, 즉 소프트웨어 모듈은 변경의 이유가 단 하나여야만 한다.
  - **장점**
    - 한 책임의 변경에서 다른 책임의 변경으로의 연쇄작용에서 자유로울 수 있다.
    -  책임을 적절히 분배함으로써 코드의 가독성 향상, 유지보수가 용이해진다.

### 2. Open-Closed Principle (OCP)
  - **정의**
    - Software entities (classes, modules, functions, etc.) should be open for extension 
      but closed for modification.
    - 소프트웨어 엔티티들은(클래스, 모듈, 함수, 등) 신규 기능의 확장에는 열려 있어야 하고 기존 코드 수정에는 닫혀있어야 한다.
  - **장점**
    - 유연성, 재사용성, 유지보수성 등 많은 장점이 있다.

### 3. Liskov Substitution Principle (LSP)
  - **정의**
    - Subtypes must be substitutable for their base types
    - 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다
  - **장점**
    - 새로운 기능을 확장할때 구현체만 변경함으로써 나머지 부분은 그대로 가져갈 수 있다.

### 4. Interface Segregation Principle (ISP)
  - **정의**  
    - Clients should not be forced to depend on methods they do not use
    - 사용하지 않는 인터페이스에 의존해서는 안된다.
    - 인터페이스를 작은 단위로 분리시킴으로써 한 클래스가 다른 클래스에 종속될 때 가능한 최소한의 인터페이스만을 사용한다.
    - 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다
  - **장점**
    - 본인의 관심 영역에 해당하지 않는 interface에 의존관계가 생기지 않기 때문에 Loose Copuling이 된다.

### 5. Dependency Inversion Principle (DIP)
  - **정의** 
    - High-level modules should not depend on low-level modules. Both should depend on abstractions
    - 고수준 정책(High Level)을 구현하는 모듈은 저수준(Low Level)의 모듈에 의존해서는 안 된다. 추상화에 의존해야지, 구체화에 의존하면 안된다.
    - 상위 계층이 하위 계층에 의존하는 전통적인 의존 관계를 반전시킴으로써 상위 계층이 하위 계층의 구현으로부터 독립되게 하는 원칙.
    
  - **장점**
    - 고수준 정책을 가지는 모듈이 자주 변경되는 모듈에 의해서 변경되지 않아도 된다.


# GRASP
### 0. GRASP 란?
  - General Responsibility Assignment Software Patterns
  - Object-Oriented 디자인의 핵심은 각 객체에 책임을 부여하는 것.
  - 책임을 부여하는 원칙들을 말하고 있는 패턴.

### 1. Information Expert
  - 책임을 수행할 수 있는 데이터를 가지고 있는 객체에 책임을 부여하는 것.
  - 객체는 데이터와 처리로직이 함께 묶여 있는 것.
  - 정보 은닉을 통해 자신의 데이터를 감추고 오직 Method로만 데이터를 처리하고, 외부에는 그 기능(책임)만을 제공한다.

### 2. Creator
  - 객체의 생성은 생성되는 객체의 컨텍스트를 알고 있는 다른 객체가 있다면, 컨텍스트를 알고 있는 객체에 부여.
  - A 객체와 B 객체의 관계의 관계가 다음 중 하나라면 A의 생성을 B의 책임로 부여.
    - B 객체가 A 객체를 포함하고 있다.
    - B 객체가 A 객체의 정보를 기록하고 있다.
    - A 객체가 B 객체의 일부이다.
    - B 객체가 A 객체를 긴밀하게 사용하고 있다.
    - B 객체가 A 객체의 생성에 필요한 정보를 가지고 있다

### 3. Controller
  - 시스템 이벤트(사용자의 요청)를 처리할 객체를 만들자.
  - 만약 어떤 서브시스템안에 있는 각 객체의 기능을 직접 사용한다면?
    - 직접적으로 각 객체에 접근하게 된다면 서브시스템과 외부간의 Coupling이 증가되고
    - 서브시스템의 어떤 객체를 수정할 경우, 외부에 주는 충격이 크게 된다.
    - 서브시스템을 사용하는 입장에서 보면, 이 Controller 객체만 알고 있으면 되므로 사용하기 쉽다.

### 4. Low Coupling
  - Low Coupling은 각 객체, 서브시스템의 재 사용성을 높이고, 시스템 관리에 편하게 한다.
  - 모듈의 변경에 의해 다른 모듈이 받는 영향이 적어진다.
  - 커플링이 심하다면?
    - 의존하는 모듈의 변경에 영향을 받는다.
    - 독립적을 이해하기 힘들어진다.
    - 재사용이 힘들어진다.

### 5. High Cohesion
  - 각 객체가 밀접하게 연관된 책임들만 가지도록 구성.
  - 한 객체, 한 시스템이 자기 자신이 부여받은 책임만을 수행하도록 짜임새 있게 구성되어 있다면?
    - 코드 재사용성이 높아진다.
    - 코드 유지보수가 편해진다.

### 6. Polymorphism
  - 하나의 객체에 여러 가지 타입을 대입할 수 있다는 것을 의미
  - 객체의 종류에 따라 Behavior 가 바뀐다면, Polymorphism 기능을 사용하여 처리할 수 있다.
  - Bahavior의 varaition이 있을 때 처리 다형성을 이용하하여 객체에 각각의 책임을 할당.
  - 관련된 대안이나 행동이 유형(클래스)에 따라 다를 때, 
    행동이 변하는 유형에 다형성 연산을 사용하여 행동에 대한 책임을 할당합니다.

### 7. Pure Fabrication
  - 도메인에 관련된 문제를 대표하는 것이 아니라면 기능적인 책임을 별도로 한 곳으로 관리하는 객체를 만들자.
  - 데이터베이스 정보를 저장하거나, 로그 정보를 기록하는 책임에 대해 생각해 보자. 각 정보는 각각의 객체들이 가지고 있을 것이다.
    - Information Expert 패턴을 적용하면?
    - 각 객체들이 정보를 저장하고, 로그를 기록하는 책임을 담당해야 하지만, 실제로 그렇게 사용하는 사람들은 없다.

### 8. Indirection
  - 두 객체 사이의 직접적인 Coupling을 피하고 싶으면, 그 사이에 다른 매개체를 통해 전달하는 것.
  - 주로 다른 매개체는 인터페이스인 경우가 많다.
    - 그런 특별한 경우는 아래에 설명된 Protected Variations 패턴이라고 부를 수 있다.

### 9. Protected Variations
  - 변경될 여지가 있는 곳에 안정된 인터페이스를 정의해서 사용하자.
  - 기존 코드 및 디자인 변경에 대한 보호할 수 있다.
