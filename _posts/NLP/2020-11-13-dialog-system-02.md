---
layout: post
title: 대화 시스템(Dialogue System) - External Knowledge Based
category: NLP
tag: [NLP, Dialogue System, Chatbot]
---

## 대화 시스템(Dialogue System) - External Knowledge Based

**External Knowledge Based Dialogue System** 은 단어 그대로 외부에서 사용자 발화와 관련된 정보를 가져와서 응답을 생성합니다. 정보는 Wikipidea, News 혹은 댓글 등이 될 수 있습니다. [Task-Oriented Dialogue System](https://hijigoo.github.io/nlp/2020/05/16/dialog-system-01/) 에서는 Chatbot이 처리할 수 있는 Intent와 응답에 필요한 Slot 값을 미리 정의해두어야 했었습니다. 하지만 사용자의 모든 발화에 대해서 Intent와 필요한 Slot 정보를 정의하는 것은 사실상 거의 불가능한 일입니다. **External Knowledge** 를 이용하면 Intent나 Slot을 미리 정의하지 않고도 사용자에게 관련된 응답을 할 수 있습니다.


<p align="center">
  <img width="90%" height="90%" src="/assets/2020-11-13-dialog-system-02/simple-architecture.png">
</p>

***
**Knowledge**

외부에 저장되어 있는 정보입니다. Wikipedia, News, 혹은 댓글이 될 수도 있습니다.


***
**IR (Information Retrieval)**

필요한 외부 정보(Knowledge)를 검색하기 위한 모듈입니다. 응답 생성에 필요한 사용자 발화와 가장 관련된 정보(Knowledge)를 가져오는데 사용됩니다. 시스템에 따라서 **Ranker** 라고도 합니다.

- **사용자** > "미국 대통령은 누구야?"
	-  **IR 결과**: [미국의 대통령 검색 결과](https://ko.wikipedia.org/wiki/%EB%AF%B8%EA%B5%AD%EC%9D%98_%EB%8C%80%ED%86%B5%EB%A0%B9)


***
**Reranker**

IR 결과 중에서 가장 연관된 정보를 추출합니다. 검색된 결과가 여러 개라면 그중에서 하나의 정보를 선택할 수도 있고, 결과가 한 개라면 해당 정보 안에서 가장 관련된 문장을 추출할 수도 있습니다. 핵심은 IR에서 검색된 결과를 가지고 한 번 더 가장 연관된 정보를 찾는 것입니다.

- **IR 결과**: [미국의 대통령 검색 결과](https://ko.wikipedia.org/wiki/%EB%AF%B8%EA%B5%AD%EC%9D%98_%EB%8C%80%ED%86%B5%EB%A0%B9)
	- **Reranker 결과**: *'현재 미국의 대통령은 2016년 미국 대통령 선거에서 당선된 45대 도널드 트럼프(공화당)로서, 2017년 1월 20일 정오[7](한국시각으로는 1월 21일 오전 2시)에 공식 취임하였다.'*


***
**NLG (Natural Language Generation)**

Reranker 로부터 데이터를 기반으로 사용자에게 친숙한 응답을 생성합니다.

- **Reranker 결과**: *'현재 미국의 대통령은 2016년 미국 대통령 선거에서 당선된 45대 도널드 트럼프(공화당)로서, 2017년 1월 20일 정오[7](한국시각으로는 1월 21일 오전 2시)에 공식 취임하였다.'*
	- **NLG** > "현재 미국의 대통령은 '도널트 트럼프'로 공화당 소속이네요!"

***
### Reference
- [Beyond Domain APIs: Task-oriented Conversational Modeling with Unstructured Knowledge Access](https://arxiv.org/abs/2006.03533)
- [Wizard of Wikipedia: Knowledge-Powered Conversational agents](https://arxiv.org/abs/1811.01241)