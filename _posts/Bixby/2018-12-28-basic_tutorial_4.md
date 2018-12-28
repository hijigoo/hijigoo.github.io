---
layout: post
title: 주사위 프로젝트 - View 및 Dialog 작성
category: Bixby
tag: [인공지능, 빅스비]
---

## View 작성

안녕하세요! 이전 포스트에서는 View를 작성하지 않아 테이블 형태로 결과를 보여주었는데요, 이번 포스트에서는 View를 작성해서 사용자에게 결과 화면을 더 이쁘게(?!) 보여주겠습니다. 자 그럼 아래와 같이 파일을 생성하고 코드를 작성합니다.

***

*/resources/ko/RollResult.view.bxb*
```
result-view {
 match {
   RollResult (rollResult)
 }

 render {
   layout {
     section {
       content {
         single-line {
           text {
             style (Detail_M)
             value ("Sum: #{value(rollResult.sum)}")
           }
         }
         single-line {
           text {
             style (Detail_M)
             value ("Rolls: #{value(rollResult.roll)}")
           }
         }
       }
     }
   }
 }
}
```

***

<div class="message">
'ko' 폴더는 단말에서 빅스비 언어를 한국어로 설정했을 때 반영됩니다. 현재는 전체 코드를 나눠놨지만 전체 구조는 공유하고 단어나 문장이 출력되는 부분만 template으로 따로 빼서 Localization을 할 수 있습니다.
</div>

위 코드에서 **match** 부분은 action의 output과 연결됩니다. 코드를 풀이해보면 어떤 action의 output이 RollResult라면 현재 view에서 보여주겠다는 뜻입니다. 자세한 [**match patterns**](https://bixbydevelopers.com/dev/docs/dev-guide/developers/customizing-plan.match-patterns) 는 공식 홈페이지에서 확인하실 수 있습니다.


그리고 아래 **render**에 화면에 표시해주는 코드를 작성합니다. 화면에 따라서 용도에 맞는 component를 사용해서 작성하실 수 있습니다. 지금은 깊게 다루지 않기 때문에 전체 흐름만 파악하시면 될 것 같습니다. 자세한 내용은 공식 홈페이지의 [**Building Views**](https://bixbydevelopers.com/dev/docs/dev-guide/developers/building-views) 를 참고 부탁드립니다. 


코드 중간에 보면 **#{value(rollResult.sum)}**와 같이 **#{}**로 작성된 부분을 볼 수 있는데요. 이 부분은 빅스비의 [**Expression Language**](https://bixbydevelopers.com/dev/docs/dev-guide/developers/customizing-plan.using-el)로 다양한 연산자를 View의 String 내부에서 사용할 수 있게 도와줍니다.

이제 아래와 같이 intent를 보내서 화면에 어떻게 나오는지 확인할 수 있습니다.

```
intent {
  goal: RollResult
  value: NumSides (6)
  value: NumDice (2)
}
```

다음은 결과 화면입니다.
![image](/assets/2018-12-28-basic_tutorial_4/result.png){: width="50%" height="50%"}

현재는 기본 Dialog로 ***"검색 완료! 확인해보세요."*** 라고 나옵니다. 




## Dialog 작성

이제 기본 Dialog를 변경해서 원하는 문장을 출력해봅시다. 결과물을 보여주는 화면을 만들기 전에 아래와 같이 Dialog 파일을 생성하고 코드를 작성합니다.

***

*/resources/ko/NumSides.dialog.bxb*
```
dialog (Concept) {
 match {
   // Look for this type
   NumSides
 }
 // Use the following template text with this type
 template("면의 수")
}
```


*/resources/ko/NumDice.dialog.bxb*
```
dialog (Concept) {
 match {
   // Look for this type
   NumDice
 }
 // Use this template text with this type
 template("주사위 수")
}
 ```

***


 참고로, 위의 두 dialog 모드(mode) concept입니다. 이 모드는 [Dialog Fragment](https://bixbydevelopers.com/dev/docs/reference/ref-topics/dialog-modes.dialog-fragments#concept-fragment)중 하나로, 필요한 concept을 intent에 넣지 않고 보냈을 경우 아래와 같이 응답을 생성하는데 사용됩니다. 

> 계속하려면 **주사위 수**가 필요해요

다음과 같이 NumDice를 제외한채 intent를 보내다보면 확인하실 수 있습니다.

```
intent {
  goal: RollResult
  value: NumSides (6)
}
```

자, 이제 최종 결과물을 보여주는 Dialog를 작성합시다. 아래와 같이 파일을 만들면 됩니다.

***

*/resources/ko/RollResult.dialog.bxb*
```
dialog (Result) {
 // bind the variable "rollResult" to the result and "rollOutput" to
 // the action of which it was output
 match {
   RollResult (rollResult) {
     from-output: RollDice (rollOutput)
   }
 }
 // define a condition that changes the dialog depending on whether there
 // is one or more dice
 if (rollOutput.numDice == 1) {
   template ("주사위의 번호는 ${value(rollResult.roll)}입니다!")    
 }
 if (rollOutput.numDice > 1) {
   choose (Random) {
     template ("주사위의 총 합은 ${value(rollResult.sum)}입니다.")
     template ("각 주사위의 번호는 ${list(rollResult.roll, 'value')}입니다.")    
   }
 }
}
```

***


전체적으로 View코드와 유사한데요, 조금 다른 점이 있습니다. 바로 ***from-output*** 인데요. RollDice의 output인 RollResult와 매칭을 시키겠다는 뜻입니다. 사실 이 프로젝트에서는 action이 유일하기 때문에 view와 매칭은 되는데요, 아래 보면 RollDice의 변수로 지정한 **rollOutput**을 이용하는 코드가 존재하기 때문에 유지해야합니다. rollOutput을 을 이용해서 RollDice의 input 값에 접근할 수 있습니다. **choose(Random)** 는 template 중 한가지를 임의 선택합니다.

<div class="message">
같은 질문에 매번 같은 대답만 한다면 인공지능처럼 느껴지지 않을 것입니다. 또한 사용자 입장에서 재미도 없을 겁니다. 그래서 다양한 응답 varidation을 주기 위해서 choose(Random)은 자주 사용하는 키워드입니다.
</div>

이제 다시 아래 intent를 보내면 최종 결과물을 확인할 수 있습니다. 

```
intent {
  goal: RollResult
  value: NumSides (6)
  value: NumDice (2)
}
```

다음은 View와 Dialog가 적용된 화면입니다.
![image](/assets/2018-12-28-basic_tutorial_4/result2.png){: width="50%" height="50%"}


여기까지 진행 하셨으면 Capsule의 기본적인 부분은 완성되었습니다. 다음 포스트에서는 Default Value 넣는 방법에 대해 다루겠습니다. 감사합니다.
