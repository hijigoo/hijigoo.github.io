---
layout: post
title: 기본 AppBar 만들기
category: Flutter
tag: [Flutter, AppBar]
---

Flutter 에서 가장 기본으로 사용할 수 있는 AppBar 입니다. 

- **AppBar.leading**: AppBar에서 왼쪽에 위치한 아이콘 버튼
- **AppBar.actions**: AppBar에서 오른쪽에 위치한 아이콘 버튼

## 메인 화면 구성
### /lib/main.dart
```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Home(title: 'AppBar Title'),
    );
  }
}
```

## AppBar 및 Body 구성
### /lib/main.dart
```
class Home extends StatelessWidget {
  final String title;

  const Home({
    Key key,
    @required this.title,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
        centerTitle: true,
        leading: IconButton(
          color: Colors.grey[800],
          icon: Icon(Icons.menu),
          iconSize: 30,
          onPressed: () => print('Menu'),
        ),
        actions: [
          IconButton(
            color: Colors.grey[800],
            icon: Icon(Icons.add),
            iconSize: 30,
            onPressed: () => print('Add'),
          ),
        ],
      ),
      body:
          Container(),
    );
  }
}
```

***
### Reference
- [Flutter > material > AppBar class
](https://api.flutter.dev/flutter/material/AppBar-class.html)