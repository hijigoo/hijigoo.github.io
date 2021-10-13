---
layout: post
title: Flutter - 작은 공간에 글씨 짤리는 것 방지하기
category: Flutter
tag: [Flutter, CI]
---

사용자의 단말 기본 텍스트 크기 때문에, 생각했던 것보다 글씨 크기가 커져서 overflow 에러가 발생하는 경우가 있습니다. 이런 경우 **FittedBox** 를 사용하면 글씨가 공간보다 커질 때 공간에 맞춰서 크기를 조절할 수 있습니다.
***

```
FittedBox(
  fit: BoxFit.scaleDown,
  child: Text(
    '공간을 많이 차지하는 텍스트'
    style: TextStyle(fontSize: 16),
  ),
);
```