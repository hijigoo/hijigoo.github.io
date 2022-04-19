---
layout: post
title: Clear intent does not mean familiar!
category: Clean Code
tag: [Clean Code]
---

## Clear intent does not mean familiar!

나에게 익숙한 코드가 항상 명확한 의도를 가지진 않는다. 더 코드를 읽기 쉽게 작성해야 한다. 아래 두 개 중에 당연 두 번째가 더 Clean 하고 Simple 하다.

```java
Integer find(List<Integer> ints) {
  int count = 0; int ans = 0;
  for (Integer num : ints) {
    if (num % 2 == 0) {
      if (num > 7) {
        count++;
        if (count == 2) {
          ans = num * num;
          break;
        }
      }
    }
  }
  return ans;
}
```

```java
Optional<Integer> find(List<Integer> ints) {
  return (
    ints.stream()
        .filter(n -> n % 2 == 0)
        .filter(n -> n >7 )
        .skip(1)
        .map(n -> n * n)
        .findFirst()
  );
}
```