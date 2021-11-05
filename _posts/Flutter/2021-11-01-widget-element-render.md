---
layout: post
title: Flutter - Widget, Element, RenderObject
category: Flutter
tag: [Flutter]
---

Flutter 에는 3개의 **Widget Tree**, **Element Tree**, **RenderObject Tree** 가 있습니다. 그리고 이 3개의 트리를 이용해서 화면을 구성합니다.

***

## Widget Tree
Widget 을 구성하는 트리입니다. Widget 은 화면을 구성하는 속성을 포함하고 있으며 **immutable** 이기 때문에 변경이 불가능합니다. Widget 은 **Element** 와 **RenderObject** 를 생성합니다. **StatefulWidget**의 경우 **State Object**가 별도로 존재합니다.  Widget 은 Element 를 생성하기 위한 Blueprint(청사진) 이라고 볼 수 있습니다.

***

## Element Tree
Element를 구성하는 트리입니다. Widget이 생성되면 Element가 생성되며 또한 Element 는 Widget 이 RenderObject 를 생성하게끔 합니다. **BuildContext** 는 Element에 담겨있습니다. 실제 화면에 붙는 것은 이 Element 라고 볼 수 있습니다.

***

## RenderObject Tree
RenderObject 를 구성하는 트리입니다. RenderObject 는 화면을 그리기 위한 정보를 가지고 있습니다. Flutter 에서 화면을 그릴 때 이 RenderObject 를 참고합니다. **StatefulWidget** 에서 **setState()** 를 호출하면 RenderObject 를 업데이트합니다.

***

## Reference
- [Layouts in Flutter](https://flutter.dev/docs/development/ui/layout#videos)
- [플루터는 어떻게 위젯을 렌더링할까](https://medium.com/@kimdohun0104/%ED%94%8C%EB%9F%AC%ED%84%B0%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9C%84%EC%A0%AF%EC%9D%84-%EB%A0%8C%EB%8D%94%EB%A7%81%ED%95%A0%EA%B9%8C-%EB%B0%9C%ED%91%9C-%EC%98%81%EC%83%81-70a726f4e53e)
- [Keys! What are they good for?](https://medium.com/flutter/keys-what-are-they-good-for-13cb51742e7d)

