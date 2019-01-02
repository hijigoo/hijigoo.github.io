---
layout: post
title: 강화학습 정리 - Multi-armed Bandits (업데이트중)
category: Reinforcement Learning
tag: [강화학습, RL]
use_math: true
---



## 2. Multi-armed Bandits

강화학습이 다른 딥러닝과 구분되는 가장 중요한 특징은 선택한 action에 대해 **평가(evaluate)**를 한다는 것이다. 이런 피드백은 얼마나 좋은지에 대한 평가이지 정답인지 아닌지를 알려주는 것은 아니다. 이번 챕터에서는 단순화된 환경에서 강화학습의 평가(evaluate)에 중점을 두고 공부할 것이다. 우리가 다룰 문제는 **k-armed bandit problem**인데 이를 소개하면서 강화학습의 주요한 요소 몇가지도 함께 공부할 것이다.


***
### A k-armed Bandit Problem

A k-armed Bandit Problem은 k개의 레버가 있는 슬롯머신에서 최대의 reward를 받기 위한 문제다. 내용은 아래와 같다.

1. k개의 다른 option이나 action중에서 하나를 선택한다.
2. *stationary probability distribution*으로 부터 하나의 reward를 받는다. 
3. 최종 목표는 일정 기간 동안 전체 reward를 최대화 하는 것이다. 

위 k-armed bandit problem에서 k action을 선택할 때마다 reward를 받는데, 이때 rewards의 기댓값(expectation)을 선택된 action의 **value**라고 한다. 식으로 나타내면 아래와 같다. 

$$
q_*(a)\doteq \mathbb{E}[R_t | A_t=a]
$$

- $A_t$: time step가 $t$ 일 때 선택된 action
- $R_t$: time step가 $t$ 일 때 $A_t$에 대한 reward
- $q_*(a)$: action $a$ 가 선택됐을 때 받는 reward의 기댓값


만약 우리가 각 action에 대한 value를 알고 있다면 k-armed bandit problem을 해결하는 것은 매우 쉬울 것이다. 매번 value가 가장 높은 action을 선택하면 되기 때문이다. 그런데 처음에는 value을 알 수 없기 때문에 계속해서 **estimate**해야 한다. 이렇게 time step $t$에서 선택된 action $a$의 value를 $Q_t(a)$라고 한다. 우리는 $Q_t(a)$가  $q_*(a)$에 가까워 지도록 계속해서 estimate 해야 한다.

action value를 계속해서 estimate 한다면, time step 마다 적어도 한 개 이상의 가장 높은 value를 갖는 action이 있을 것이다. 그 action을 *greedy* action 이라고 한다. 만약 이 action들 중 하나를 선택한다면 이를 ***exploiting*** 한다고 얘기한다. 반대로 *greedy* action이 아닌 다른 action들 중 하나를 선택한다면 ***exploring***한다고 얘기한다. 당장 한 스텝만 바라봤을 때는 ***exploitation***이 value를 최대화 하는 방법일지 몰라도, 장기적인 관점에서 바라봤을 때 ***exploration***의 total reward가 더 높을 수 있다.

*exploration* 와 *exploitation* 의 균형을 맞춰 나가기 위해서 복잡한 수학적인 방법들이 존재하지만, 많은 가정들이 전제해야 하기 때문에 사실상 full reinforcment learning 문제에 적용하기는 불가능하다. 하지만, 이를 해결하기 위한 간단한 방법들이 존재하고 나중에 다룰 것이다.



***
### Action-value Methods




***
### Summary


***
### Reference
- [Reinforcement Learning: An Introduction - Richard S. Sutton and Andrew G. Barto](http://incompleteideas.net/book/the-book.html)