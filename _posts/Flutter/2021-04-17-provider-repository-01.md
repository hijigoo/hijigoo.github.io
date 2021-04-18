---
layout: post
title: Flutter - Provider, Repository 동시에 등록하기
category: Flutter
tag: [Flutter, Provider, Repository]
---

Flutter에서 **Provider** 와 **Repository** 를 사용하려면 트리의 상위 노드에 등록해주어야 합니다. Repository는 Provider 안에서 사용할 수 있기 때문에 Repository를 먼저 등록하고 Provider를 등록할 때 Inject 해주어야 합니다. 

**Bloc** 사용시에도 마찬가지입니다. 단, Provider 와 Repository 는 **runApp()** 호출할 때 등록하고 Bloc는 **MaterialApp** 호출할 떄 등록하기 때문에 본 예에서는 다루지 않았습니다.

<div class="message">
Bloc를 runApp()에서 호출하는 경우 동작하기는 하였으나, MaterialApp 함수 호출 시 등록하는 localizationsDelegates, supportedLocales 등의 국가/언어를 초기화하는 일부 기능이 적용되지 않았기 때문에 MaterialApp 에서 별도로 등록해주었습니다.
</div>


### Provider, Repository 등록
~~~dart
void main() {
  // set timezone - for notification
  tz.initializeTimeZones();
  tz.setLocalLocation(tz.getLocation('Asia/Seoul'));

  Bloc.observer = DefaultObserver();
  WidgetsFlutterBinding.ensureInitialized();

  runApp(MultiRepositoryProvider(
    // provide Repository
    providers: [
      RepositoryProvider<AuthenticationRepository>(
        create: (context) => AuthenticationRepository(),
      ),
      RepositoryProvider<UserRepository>(
        create: (context) => UserRepository(),
      ),
      RepositoryProvider<ConnectRepository>(
        create: (context) => ConnectRepository(),
      ),
    ],
    child: MultiProvider(
      // provide Provider
      providers: [
        ListenableProvider<LayoutFont>(create: (context) => LayoutFont()),
        ListenableProvider<Alarm>(create: (context) => Alarm()),
        ListenableProvider<LockSetting>(create: (context) => LockSetting()),
        ListenableProvider<Couple>(
          create: (context) => Couple(
              RepositoryProvider.of<UserRepository>(context),
              RepositoryProvider.of<ConnectRepository>(context)),
        ),
      ],
      child: App(),
    ),
  ));
}
~~~