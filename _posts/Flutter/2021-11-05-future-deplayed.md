---
layout: post
title: Flutter - Future.delayed()
category: Flutter
tag: [Flutter]
---

Network 와 통신하는 동안 Loading Spinner 를 보여주는 UI 를 테스트하고 싶은 경우가 매우 많이 발생합니다. 하지만 실제로 외부 서버와 통신하는 것으로 테스트 코드를 작성하는 것은 좋지 않습니다. 이럴 때 외부 서버와 통신하는 **척** 하는 방법을 사용하는데, 이를 **Mock** 혹은 **Mocking** 한다고 표현합니다. 위와 같이 UI 를 테스트하기 위해서 **Future.delayed** 를 사용하면 같은 효과를 낼 수 있습니다.

***
```
final myFuture = Future.delayed(
  Duration(seconds: 5),
  () => 12,
)
```