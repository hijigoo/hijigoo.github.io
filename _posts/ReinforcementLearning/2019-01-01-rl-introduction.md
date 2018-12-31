---
layout: post
title: 강화학습 정리 - Introduction
category: Reinforcement Learning
tag: [강화학습, RL]
---



## 1. Introduction

우리가 배움의 본질에 대해 생각할 때 가장 먼저 떠올리는 것 중 하나는 **환경(environment)**과 상호작용 하면서 배우는 것이다. 예를 들어서 아기들은 가르쳐주는 사람이 없더라도 스스로 팔을 흔들고, 노는 행동을 하고, 주위를 바라보는 방법 등을 터득한다. 아기는 자신과 연결된 환경(environment)과 상호작용하며 배우는데 필요한 정보를 습득하는 것이다.


***
### Reinforcement Learning

Reinforcement learning은 현재 자신에게 주어진 환경에서 어떤 **행동(action)**을 해야 하는지 배우는 것이다. 그리고 이 행동(action)은 **보상(reward)**을 최대로 얻을 수 있는 방법을 따른다.

여기서 흥미로운 점은 내가 선택하는 행동(action)이 당장 받을 보상(immediate reward)뿐 아니라 다음 상황(state)과 나중에 받을 보상(subsequent rewards)에도 영향을 미친다는 것이다. 즉, 행동(action)을 선택할 때 나중에 받을 보상도 고려를 해야 하는 것이다.

또한, reinfocement learning이 받는 challenge 중 하나는 **exploitation** 과 **exploration**의 trade-off 이다. 행동(action)을 선택할 때 두 가지 접근 방법 중에서 하나를 선택해야 하기 때문이다.

- **exploitation**: 이미 학습한 정보를 토대로 최대 reward를 얻는 action을 선택한다.
- **exploration**: 새로운 정보를 학습하기 위해서 여러가지 action을 선택해본다.

아래는 교재에서 설명된 내용이다.
>The agent has to *exploit* what it has already experienced in order to obtain reward, but it also has to *explore* in order to make better action selections in the future.

마지막으로, reinforcement learning에서 **학습하는 대상(agent)**은 **목표 지향적(goal-directed)**이며 불확실한 환경(uncertain environment)에서도 모든 문제를 고려해야 한다.


***
### Elements of Reinforcement Learning

위에서 설명 했듯이 reinforcement learning에서는 **agent**는 **environment**와 상호작용 하면서 학습하는데, 이 시스템에서 중요한 네가지 요소를 아래와 같이 정의할 수 있다. 

- **Policy**: 주어진 environment의 state에서 agent가 선택해야 할 action을 정의
- **Reward signal**: agent가 action을 선택했을 때 environment로 부터 받는 값
- **Value function**: agent가 특정 state에서 앞으로 받을 모든 rewards의 합에 대한 기댓값을 정의
- **Model**: environment의 동작(behavior)에 대해 정의

**Policy**는 현재의 내 상태(states of the environment)에서 취해야 할 action을 정의 하는데, 간단한 function이나 lookup table 일 수도 있다. 일반적으로 확률론(stochastic)적 이며 각 action에 대한 확률(probabilities)를 가지고 있다. 

**Reward signal**은 agent가 action을 선택 했을 때 즉각적으로 environment로 부터 받는 보상 값으로, reinforcement learning에서 agent의 유일한 목표는 이 reward의 총 합을 최대화하는 것이다. reward는 policy를 정의하기 위한 기본 요소다. 

**Value function**은 길게 보았을 때 agent가 특정 state에서 받을 reward의 총 합에 대한 기댓값을 정의한다. agent가 주어진 state에서 특정 action을 선택했을 때 당장 받을 reward는 다른 action을 취했을 때 보다 상대적으로 낮더라도 최종적으로 누적될 reward는 가장 높을 수도 있다.

**Model**은 environment의 동작(behavior)에 대해 정의한다. 즉, model을 알고 있으면 state와 action이 주어졌을 때의 가능한 결과를 미리 예상할 수 있다. model은 agent가 직접 경험해 보기도 전에 *계획(planning)*을 세우는데 사용된다. 문제를 해결하기 위해서 model과 planning을 사용하는 방법을 *model-based*라고 한다. 반대로 agent가 model을 모르는 상태에서 *경험을 하면서(trial-and-error)* 문제를 해결하는 방법을 *model-free*라고 한다.


***
### Summary

Reinforcement learning은 agent가 environment와 상호작용 하면서 학습한다는 점에서 다른 학습 방법과는 구분된다. 그리고 states, actions, rewards를 포함한 environment와 agent의 관계를 정의하기 위해서 **[Markov decision processes(MDP)](https://en.wikipedia.org/wiki/Markov_decision_process)**라는 framework 를 사용한다. **value** 와 **value function** 컨셉은 reinforcement learning에서 매우 중요한 요소다. agent는 policy에 따라서 action을 취하는데, value는 policy를 정의하는 기본 요소이기 때문이다.


***
### Reference
- [Reinforcement Learning: An Introduction - Richard S. Sutton and Andrew G. Barto](http://incompleteideas.net/book/the-book.html)