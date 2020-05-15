---
layout: post
title: 대화 시스템(Dialogue System) - 아키텍쳐
category: NLP
tag: [NLP, Dialogue System]
---

## 대화 시스템(Dialogue System) - 아키텍쳐

**Task-Oriented Dialogue System** 대화 시스템의 아키텍쳐는 보통 아래와 같이 3개의 모듈로 구성되어 있습니다. 더 똑똑한 대화 시스템을 구현하기 위해서 각 모듈이 합쳐지거나 더 세분화 되기도 합니다.

<p align="center">
  <img width="80%" height="80%" src="/assets/2020-05-16-dialog-system-01/simple-architecture-2.png">
</p>


***
**NLU (Natural Language Understanding)**

사용자의 발화를 이해하기 위한 모듈입니다. 입력으로 들어온 발화는 분석되어 정형화된 데이터로 변환됩니다. 

- **사용자** > "내일 서울 날씨 알려줘"
	-  **NLU 결과**: intent(Search-Weather), location(Seoul), date(2020-05-17)


***
**DM (Dialogue Manager)**

사용자와 시스템이 주고 받는 대화의 흐름을 관리합니다. 크게 두 가지 모듈로 구성되어 있는데, **Dialog State Tracker** 는 현재 대화 상태를 관리합니다. 아래의 예를 보면 NLU 결과로부터 Dialog State 를 업데이트 하면서 대화를 진행하고 있습니다. 실제로는 NLU 결과 뿐 아니라 더 많은 데이터를 유지합니다. **Policy Manager**는 시스템이 사용자에게 전달할 **Action** 을 결정합니다. Action 은 NLG 에게 바로 전달되기도 하고 Database로부터 응답에 필요한 정보를 가져오는데 사용되기도 합니다. 아래의 예에서 *내일 서울의 날씨*를 사용자에게 알려주기 위해서는 외부 Database로부터 정보를 가져와야 합니다.


- **사용자** > "내일 날씨 알려줘"**  
	- **NLU 결과**: intent(Search-Weather), location(Seoul), date(2020-05-17)
	- **Dialog State**: intent(Search-Weather), date(2020-05-17) 
- **시스템** > "어느 지역 날씨를 알려드릴까요?"
	- **Action**: REQUEST_LOCATION
- **사용자** > "서울"  
	- **NLU 결과**: location(Seoul), date(2020-05-17) 
	- **Dialog State**: intent(Search-Weather), location(Seoul), date(2020-05-17)


***
**NLG (Natural Language Generation)**

DM 으로부터 받은 데이터를 입력으로 받아서 사람이 쉽게 이해할 수 있는 시스템의 응답을 생성합니다. 응답은 각 시스템의 페르소나를 결정할 수 있기 때문에 매우 주의 깊게 다루어져야 합니다. 예를 들어서 성적 농담이나 인종차별과 같은 민감한 질문에 우스꽝스러운 응답을 한다면 대화 시스템의 신뢰에 나쁜 영향을 미칠 수 있습니다.
