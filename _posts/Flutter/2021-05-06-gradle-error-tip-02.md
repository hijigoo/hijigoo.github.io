---
layout: post
title: Flutter - 안드로이드 gradle 4.0.0 이상 빌드에러 대응
category: Flutter
tag: [Flutter, Error]
---

안드로이드에서 gradle 4.0.0 이상 버전으로 빌드 시 에러가 발생하게 됩니다. Gradle 버전을 3.5.0 으로 낮추면 해결되지만 4.0.0 버전을 유지하고 싶을 때는 아래 순서로 빌드하면 해결됩니다.

***

## 해결 방법
```
flutter build apk --debug
flutter build apk --profile
flutter build apk --release

cd build/app/outputs/flutter-apk/
abd install ./app-release.apk
```

***
### 출처
- [Reinforcement Learning: An Introduction - Richard S. Sutton and Andrew G. Barto](https://stackoverflow.com/questions/62394034/flutter-can-not-build-android-apk)