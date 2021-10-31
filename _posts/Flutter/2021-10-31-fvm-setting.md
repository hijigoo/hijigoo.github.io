---
layout: post
title: Flutter - VSCode에서 fvm셋팅하기
category: Flutter
tag: [Flutter]
---

fvm(Flutter Version Management)을 사용하면 프로젝트 별로 Flutter SDK 버전관리를 할 수 있습니다. 이미 개발환경 및 프로젝트가 생성된 상태에서 fvm만 적용하는 것을 가정으로 작성했습니다.

***

### Release 된 Flutter SDK 버전 확인하기
```
fvm release
```

### 설치되어 있는 Flutter SDK 확인
```
fvm list
```

### 새로운 Flutter SDK Version 설치
```
fvm install 2.5.3
```

### 프로젝트에서 사용할 버전 선택
```
fvm use 2.5.3
```

### VSCode에 Flutter SDK 위치 지정
프로젝트 폴더에 **.vscode/settings.json** 를 생성후 아래와 같이 경로 지정
'''
{
  "dart.flutterSdkPaths": [".fvm/flutter_sdk"]
}
'''