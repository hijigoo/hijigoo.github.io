---
layout: post
title: Flutter - Github에서 Action으로 APK 빌드하기
category: Flutter
tag: [Flutter, CI]
---

*build-release* 브랜치에 Push를 하거나 PR을 보내면 APK를 빌드하는 스크립트 입니다. 파일은 대상으로 하는 *build-release* 브랜치의 **.github/workflows/build.yml** 경로에 생성하면 됩니다. 

***

## APK 빌드 .yml 스크립트
```

name: Flutter Build APK

on:
  push:
    branches:
      - build-release
  pull_request:
    branches:
      - build-release

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-java@v1
        with:
          java-version: '12.x'

      - name: Get current date
        id: date
        run: echo "::set-output name=date::$(date +'%Y-%m-%d')"
        
      - name: Set up Flutter
        uses: subosito/flutter-action@v1
        with:
          flutter-version: '2.2.3'
          
      - name: Install Dependencies
        run: flutter pub get
      
      - name: Run Test
        run: flutter test
      
      - name: Build APK
        run: flutter build apk --release

      - name: Upload APK
        uses: actions/upload-artifact@v2
        with:
          name: app-release
          path: build/app/outputs/flutter-apk/app-release.apk
```