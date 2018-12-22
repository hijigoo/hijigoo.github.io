---
layout: post
title: 주사위 프로젝트 - Capsule 테스트
category: Bixby
tag: [인공지능, 빅스비]
---

## Capsule 테스트


이제 아래와 같은 순서로 실행해볼 수 있습니다.

1. **View > Open Simulator** 로 가서 Simulator를 실행합니다.
2. 팝업창이 뜨면 **Confirm**을 눌러서 컴파일 하고 학습된 데이터를 준비합니다.
3. 아직 자연어 학습을 하지 않았기 때문에 아래의 intent를 직접 입력합니다.
```
intent {
  goal: RollResult
  value: NumSides (6)
  value: NumDice (2)
}
```
4. **Run NL** 을 선택하여 실행합니다.

간단하게 설명드리면, 사용자는 RollResult를 얻기를 원하며, NumSides값을 6으로, NumDice값을 2로 빅스비에게 알려준 것입니다. 

<div class="message">
자연어를 학습시키면 "면이 6개인 주사위 2개를 굴려줘!" 라는 발화가 위의 intent로 변환되어 실행됩니다. 이 부분은 맨 마지막에 다룰 예정입니다.
</div>


지금까지 잘 따라오셨다면 아래와 같은 화면을 보실 수 있을 겁니다. 현재는 따로 화면(Moment)을 만들지 않았기 때문에 리턴된 output 데이터를 테이블형식으로 보여줍니다. 

<div class="message">
빅스비에서는 사용자에게 보여주는 응답, 즉 화면 자체를 Moment라고 지칭합니다.
</div>

![image](/assets/2018-12-23-basic_tutorial_3/screenshot02.png)


이제 빅스비가 실행 그래프(execution graph)가 어떻게 만들었는지 확인해봅시다. simulator에서 왼쪽 위에 Reset 버튼 옆에 있는 두개의 버튼 중 **Debug** 버튼을 눌러서 Debug Console을 실행하면 아래와 같은 화면을 보실 수 있을겁니다.  

<!-- ![image](){: width="50%" height="50%"} -->
![image](/assets/2018-12-23-basic_tutorial_3/screenshot03.png)

위의 그래프를 보면 intent에서 두 개의 value 값이 concept으로 맵핑되고 goal인 RollResult를 얻기 위해서 RollDice로 연결되었습니다. 그리고 그래프가 실행되면서 RollDice Action에 도달했을 때는 endpoint에서 연결 된 RollDice.js 를 실행시켜 최종 아웃풋인 RollResult를 결과로 얻습니다.

다음 포스트에서는 RollResult를 화면에 보여주는 방법에 대해서 정리하겠습니다. 
