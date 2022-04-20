---
layout: post
title: Clean Architecture
category: Architecture
tag: [Architecture]
---

## Clean Architecture

Clean Architecture 에 대해 찾아보면 맥락에 따라 용어가 다르게 사용되기 때문에 한번에 모아보았다. Layer 를 구분하는 경계가 달라지는 경우도 있으며, Domain Layer 는 상황에 따라서 Application Layer 와 Domain Layer 로 다시 나눠지기도 한다. 하지만 중요한 부분은 Domain Layer 가 시스템의 중요 정책/로직 을 포함하며, Presentation Layer 나 Infrastructure Layer 의 변화에 영향을 받지 않는 다는 것이다. 그리고 이를 위해서 동심원 안에서 밖으로 호출이 이뤄질 때는 Dependency Inversion 이 적용된다. 

***

![image](/assets/2022-04-20-clean-architecture/figure01.png)

#### Framework / Driver (Infrastructure)
-  모든 I/O Component 가 있으며 가장 변하기 쉬운 부분이다.

#### Interface Adapter (Adapter)
- Framework / Driver 와 Application Business Logic 사이를 연결한다.
- MVC Model 에서 Presenter, View, Controller 가 모두 여기에 포함된다.

#### Application Business Logic (Domain)
- 어플리케이션에서 가장 핵심적인 부분으로 High Level 의 정책과 로직을 갖는다.
- 시스템의 모든 UseCase 가 구현되어 있다.


***
### Reference
- [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
