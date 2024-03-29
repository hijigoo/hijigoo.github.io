---
layout: post
title: Flutter Clean Architecture
category: Architecture
tag: [Flutter, Architecture]
---

## Clean Architecture

Robert C. Martin (Uncle Bob) 아저씨의 클린코드를 보면 Dependency 가 밖에서 안으로 들어가는 것을 볼 수 있다. 그리고 제일 안쪽에는 Entities가 존재한다. 하지만 Entity 를 얻기 위해서는 Repository(Gateway) 를 사용해서 DB 에 접근해야 하는데 이러면 Dependency 규칙이 어긋난다. 이를 방지하기 위해 Interface 를 제공해줌으로써 Dependency Inversion 을 시킨다.

아래 그림을 보면 Control Flow 와 반대로 Dependency Inversion 된 것을 확인할 수 있다.

![image](/assets/2022-04-19-flutter-clean-architecture/figure01.png)

#### Data Layer
-  Domain 레이어의 Repository 를 Imprementation 한다.
-  Domain 레이어의 Entity 를 상속해서 Model 을 만든다.  

#### Domain Layer
- 다른 Layer 에 의존하지 않는다.
- 가장 중요한 부분으로 중요 정책을 결정한다.
- Usecase 하나는 여러개의 Repository 를 사용할 수 있다.

#### Presentation Layer
- Entity 를 사용한다.
- Usecase 를 사용한다.
- Bloc 는 여러개의 Usecase 를 사용할 수 있다.


***
### Reference
- [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [clean-code-architecture-flutter - RashmiRanganathan](https://github.com/RashmiRanganathan/clean-code-architecture-flutter)
- [flutter clean architecture - devmuaz](https://devmuaz.medium.com/flutter-clean-architecture-series-part-1-d2d4c2e75c47)
