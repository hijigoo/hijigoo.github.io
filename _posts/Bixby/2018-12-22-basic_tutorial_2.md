---
layout: post
title: 주사위 프로젝트 - Concept과 Action 추가 (수정중)
category: Bixby
tag: [인공지능, 빅스비]
---

## Concepts과 Actions 추가

이번 포스트에서는 Concept과 Action을 추가하여 모델링하는 과정을 설명드리겠습니다. Concept는 우리가 사용 할 변수라고 보시면 되고, Action은 함수라고 생각하면 조금 더 이해하기 편하실 겁니다.

>Concepts explain what Bixby knows, while actions determine what Bixby can do. 

프로젝트에서는 총 다섯개의 Concept과  한개의 Action을 사용합니다. 각 의미는 아래와 같습니다. 

- **Concept**
	- **NumDice.model.bxb** : 주사위의 개수를 의미하는 primitive concept 입니다. 
	- **NumSides.model.bxb** : 주사위 면의 개수를 의미하는 primitive concept 입니다. 
	- **Roll.model.bxb** : 주사위 하나에서 나온 숫자를 의미하는 primitive concept 입니다. 
	- **Sum.model.bxb** : 모든 주사위에서 나온 숫자의 합을 의미하는 primitive concept 입니다. 
	- **RollResult.model.bxb** : 최종 결과이며 Roll과 Sum을 포함하는 structure concept 입니다.

- **Action**
	- **RollDice.model.bxb** : NumDice와 NumSides를 입력으로 받아서 RollResult를 생성하는 action입니다.

위에서 primitive는 integer나 text 같은 기본 자료형을 의미합니다. 이제 models 폴더 아래에 concepts 폴더를 생성하고 위에 있는 Concept 파일들을 만들어줍니다. RollResult를 제외한 모든 Concept의 데이터 타입은 모두 integer 입니다. 위에서도 설명드렸듯이 RollResult는 Roll과 Sum을 포함하고 있는 strucutre 타입입니다. 아래는 각 파일 경로와 코드입니다.

***

*/model/concepts/Numdice.model.bxb*
```
integer (NumDice) {
  description (The number of dice.)
}
```


*/model/concepts/NumSides.model.bxb*
```
integer (NumSides) {
  description (The number of sides to the dice.)
}
```


*/model/concepts/Roll.model.bxb*
```
integer (Roll) {
  description (The result of a dice roll.)
}
```


*/model/concepts/Sum.model.bxb*
```
integer (Sum) {
  description (The total sum of all the dice rolled.)
}
```


*/model/concepts/RollResult.model.bxb*
```
structure (RollResult) {
  description (The result object produced by the RollDice action.)
  property (sum) {
    type (Sum)
    min (Required)
    max (One)
  }
  property (roll) {
    type (Roll)
    min (Required)
    max (Many)
  }      
}
```

***

위의 RollResult에서 roll은 주사위의 개수만큼 있기 때문에 리스트로 받아야 합니다. **max값이 Many이면 값을 리스트로 받습니다.** Concept을 정의했으니 이제 Action을 만들어보겠습니다. Action은 models 폴더 아래에 actions 폴더를 생성하고 RollDice.model.bxb 파일을 만듭니다.


***

*/model/actions/RollDice.model.bxb*
```
action (RollDice) {
  type (Calculation)

  collect{
    input (numDice) {
      type (NumDice)
      min (Required)
      max (One)
    }

    input (numSides) {
      type (NumSides)
      min (Required)
      max (One)
    }
  } 

  output (RollResult)
}
```

***

위의 코드를 보시면 입력(collect)으로는 numDice와 numSides를 각각 하나씩 받고 아웃풋으로는 RollResult가 생성되도록 정의했습니다. type은 선택사항으로 [링크](https://bixbydevelopers.com/dev/docs/reference/type/action.type)를 참고하여 넣어주시면 됩니다. 여기까지 기본적인 모델링을 했다고 생각하시면 됩니다. Bixby는 우리가 모델링한 Action과 Concept를 참고해서 실행 될 그래프를 만들어 줄 겁니다. 

이제 RollDice의 함수를 만들어야 합니다. 앞서 만든 RollDice의 Action이 interface라면, 이제 만들 함수는 implementation이라고 생각하시면 됩니다. 코드는 다음과 같습니다. code 폴더 아래에 RollDice.js 함수를 생성합니다. 


***

*/model/code/RollDice.js*
```
// Main entry point
module.exports.function = function rollDice(numDice, numSides) {

  var sum = 0;
  var result = [];

  // Generate random roll number (1~numSides)
  for (var i = 0; i < numDice; i++) {
    var roll = Math.ceil(Math.random() * numSides);
    result.push(roll);
    sum += roll;
  }

  // RollResult
  return {
    sum: sum, // required Sum
    roll: result // required list Roll
  }
}
```

***

위의 함수를 보시면 RollDice.model.bxb 에 정의한 내용과 같게 numDice와 numSides를 입력으로 받고 RollResult를 리턴합니다. 마찬가지로 반환되는 JSON도 RollResult.model.bxb 와 같은 구조입니다. 

이제 Bixby가 실행될 때 Javascript 함수에도 접근할 수 있도록 endpoint를 정의 해주어야 합니다. resources 폴더 아래에 다시 ko 폴더를 만들고 endpoints.bxb 파일을 추가합니다.


***

*/resources/ko/endpoints.bxb*
```
endpoints {
   authorization {
     none
   }
   action-endpoints {
     action-endpoint (RollDice) {
       accepted-inputs (numDice, numSides)
       local-endpoint ("RollDice.js")
     }
   }
}
```

***

<!-- 지금까지 구현한 프로젝트의 구조는 아래와 같습니다.

![image](/assets/2018-12-22-basic_tutorial_2/screenshot05.png){: width="30%" height="30%"}
 -->

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

![image](/assets/2018-12-22-basic_tutorial_2/screenshot02.png)


이제 빅스비가 실행 그래프(execution graph)가 어떻게 만들었는지 확인해봅시다. simulator에서 왼쪽 위에 Reset 버튼 옆에 있는 두개의 버튼 중 **Debug** 버튼을 눌러서 Debug Console을 실행하면 아래와 같은 화면을 보실 수 있을겁니다.  

<!-- ![image](){: width="50%" height="50%"} -->
![image](/assets/2018-12-22-basic_tutorial_2/screenshot04.png)

위의 그래프를 보면 intent에서 두 개의 value 값이 concept으로 맵핑되고 goal인 RollResult를 얻기 위해서 RollDice로 연결되었습니다. 그리고 그래프가 실행되면서 RollDice Action에 도달했을 때는 endpoint에서 연결 된 RollDice.js 를 실행시켜 최종 아웃풋인 RollResult를 결과로 얻습니다.

다음 포스트에서는 RollResult를 화면에 보여주는 방법에 대해서 정리하겠습니다. 
