---
layout: post
title: 주사위 프로젝트 - Concept과 Action 추가
category: Bixby
tag: [인공지능, 빅스비]
---

## Concepts과 Actions 추가

프로젝트를 생성하고 간단하게 폴더 구조를 봤으면, 이제 Concept과 Action을 추가하여 모델링을 시작할 차례입니다. Concept는 우리가 사용 할 변수라고 보시면 되고, Action은 함수라고 생각하면 조금 더 이해하기 편하실 겁니다.

>Concepts explain what Bixby knows, while actions determine what Bixby can do. 

프로젝트에서는 총 5개의 Concept과  1개의 Action을 사용합니다.

### Concept
- **NumDice.model.bxb** : 주사위의 개수를 의미하는 primitive concept 입니다. 
- **NumSides.model.bxb** : 주사위 면의 개수를 의미하는 primitive concept 입니다. 
- **Roll.model.bxb** : 주사위 하나에서 나온 숫자를 의미하는 primitive concept 입니다. 
- **Sum.model.bxb** : 모든 주사위에서 나온 숫자의 합을 의미하는 primitive concept 입니다. 
- **RollResult.model.bxb** : 최종 결과이며 Roll과 Sum을 포함하는 structure concept 입니다.

### Action
- **RollDice.model.bxb** : NumDice와 NumSides를 입력으로 받아서 RollResult를 생성하는 action입니다. Concept에서도 설명드렸듯이 RollResult는 Roll과 Sum을 포함하고 있는 strucutre 입니다


Concept과 Action 파일을 넣을 폴더를 아래와 같이 생성합니다.  
![image](/assets/2018-12-21-basic_tutorial_1/screenshot02.png)
- <project_folder>/models/actions/  
- <project_folder>/models/concepts/