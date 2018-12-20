---
layout: post
title: 주사위 프로젝트 - 프로젝트 생성
category: Bixby
tag: [인공지능, 빅스비]
---

안녕하세요. 이번에는 빅스비 개발자 홈페이지에 나와있는 [Dice 프로젝트](https://bixbydevelopers.com/dev/docs/get-started/quick-start)를 만들어 보려고 합니다. 영어가 편하신분은 공식 사이트에서 보시는 것을 추천드립니다. Dice프로젝트는 사용자가 아래와 같이 말하면 그 결과를 보여주는 간단한 캡슐입니다. 아래 예제에서 숫자 4 와 2는 1~6 중에서 랜덤으로 나온 숫자입니다.


> 사용자: "**면이 6개**인 **주사위 2개**를 굴려줘!"  
> 빅스비: "4 그리고 2 가 나왔습니다. 총 합은 6입니다."


## 프로젝트 생성

그럼 프로젝트를 만들어 보겠습니다. IDE는 [공식 홈페이지](https://bixbydevelopers.com/)에서 자신이 사용하는 OS에 맞게 [다운](https://bixbydevelopers.com/) 받으시면 됩니다. IDE를 설치하시고 아래와 같은 순서로 진행합니다.


1. **Fie->New Capsule**을 선택하여 프로젝트를 생성합니다.
2. 프로젝트를 생성할 폴더를 선택합니다.
3. Capsule ID를 입력합니다. 저는 **study.dice**로 생성했습니다.
4. 마지막으로 **Create** 버튼을 누르시면 기본 구조로 프로젝트가 생성됩니다.

![image](/assets/2018-12-21-basic_tutorial_1/screenshot01.png)

처음 프로젝트를 생성하면 code와 resources폴더가 생깁니다. code폴더에는 Javascript 코드가 들어가는데 서버와 api 통신이나, 연산과 같은 각 Action이 실행될 때 필요한 로직이 들어갑니다. 그리고 resource폴더에는 언어별로 필요한 학습 데이터와 화면을 구성하는데 필요한 파일들이 들어갑니다. 


<div class="message">
캡슐에서는 사용자에게 보여지는 하나의 화면을 Moment라고 하며 여기에는 Dialog, View 그리고 Follow-Ups이 포함됩니다.
</div>
참고: [Designing Your Capsule](https://bixbydevelopers.com/dev/docs/dev-guide/design-guides/service)

그리고 **capsule.bxb** 파일을 보시면 아래와 같이 나와있는데요, 캡슐의 기본 설정 값을 입력한다고 생각하시면 됩니다. 저희는 한국어를 기본으로 할 것이기 때문에 **targets** 값을 **bixby-mobile-ko-KR** 로 변경합니다.

```
capsule {
  id (study.dice)
  version (0.1.0)
  format (3)
  targets {
    target (bixby-mobile-ko-KR)
  }
}
```
  
다음에는 Concept과 Actions를 추가하여 모델링을 해보겠습니다.
