---
layout: post
title: 강화학습 정리 - Finite Markov Decision Processes (업데이트중)
category: Reinforcement Learning
tag: [강화학습, RL]
use_math: true
---


## 3. Finite Markov Decision Processes

이번 챕터에서는 앞으로 계속 다룰 finite **Markov decision processes (MDPs)** 에 대해서 소개한다. 그런데 이전 챕터에서 다룬 bandits problem 과는 다르게, 상황에 따라서 다른 action을 취해야 하는 *associative task* 이다. MDPs는 [순차적 의사 결정(sequential decision making)](https://en.wikipedia.org/wiki/Sequential_decision_making)을 하는 고전적인 공식인데, 여기서 선택된 action은 immediate reward 에만 영향을 미치는 것이 아니라, 나중의 상황(situation)이나 **state** 그리고 **future reward** 에도 영향을 미친다. 그렇기 때문에 MDPs는 **delayed reward** 라는 개념을 가지고 있으며, immediate reward 와 tradeoff 해야 하는 필요성도 수반하고 있다. Badit problem 에서는 각 action $a$ 의 value로 **$q_\*(a)$** 를 estimate했지만, MDPs에서는 action $a$ 와 각 state $s$ 의 value로 **$q_\*(s,a)$** 를 estimate한다.  


***
### The Agent–Environment Interface

MDPs는 상호 작용하면서 학습하는 문제를 간단하게 정의한다. 학습하고 의사 결정하는 것을 ***agent*** 라고 하며, 이 agent와 상호작용 하며 agent외부에 존재하는 모든 것을 ***environment*** 라고 한다. agent가 action을 선택하면 environment는 새로운 상황(situation)을 제시한다. 또한 environment는 reward를 제공하는데, agent는 이 reward가  최대가 되도록 action을 선택해 나아가야 한다.

<div class="message">
situation과 state 단어가 나오는데요, 여기서는 situation을 state를 포함한 개념으로 사용합니다. 중요한 키워드는 state와 reward입니다. 
</div>

![image](/assets/2019-01-15-rl-finite-mdps/figure3_1.png)

위 그림처럼 각 time step($t$ = 0, 1, 2, 3, ...)마다 **agent**와 **environment**는  상호작용 한다. time step $t$ 에서 agent는 environment로부터 **state** ($ S_t \in \mathscr{S}$ )를 받으며 이를 고려해서 **action** ($ A_t \in \mathscr{A}(s)$ )을 선택한다. 그리고 한 time step 이후에 action에 대한 결과로 **reward** ($ R_{t+1} \in \mathscr{R} \subset \mathbb{R} $)와 새로운 state ($ S_{t+1} $)를 받는다. 이를 순서대로 나타내면 아래와 같다. 

$$
\begin{align*}
S_0, A_0, R_1, S_1, A_1, R_2, S_2, A_2, R_3, ... && (3.1)
\end{align*}
$$

이전 time step 에서 state $s$와 action $a$이 주어졌을 때, $s^\prime$ 와 $r$이 나올 확률은 아래와 같이 표현할 수 있다.

$$
\begin{align*}
p(s^\prime,r \mid s,a) \doteq \operatorname{Pr}\left\{ S_t=s^\prime, R_t=r  \mid  S_{t-1}=s, A_{t-1}=a \right\} && (3.2)
\end{align*}
$$

함수 $p$는 MDP의 *dynamics*를 정의한다. 또한, $p$는 확률 분포이기 때문에 아래와 같이 정의할 수 있다. 

$$
\sum_{s^\prime \in \mathscr{S}}\sum_{r \in \mathscr{R}}p(s^\prime,r \mid s,a) = 1, \text{  for all }s \in \mathscr{S}, a \in \mathscr{A}(s)
$$

$S_t$와 $R_t$의 값은 바로 직전의 $S_{t-1}$와 $A_{t-1}$에 의해서만 결정된다. state는 이전에 발생한 agent 와 environment의 상호작용에 대한 모든 정보를 내포하고 있어야 하는데, 여기서는 이 state를 ***[Markov property](https://en.wikipedia.org/wiki/Markov_property)***라고 한다.  

다음과 같이 함수 $p$으로부터 environment에 대해서 알고 싶은 정보를 계산할 수 있다.

- ***state-transition probabilities***


$$
p(s^\prime \mid s,a) \doteq \operatorname{Pr}\left\{ S_t=s^\prime  \mid  S_{t-1}=s, A_{t-1}=a \right\} = \sum_{r \in \mathscr{R}}p(s^\prime,r \mid s,a)
$$

- ***state-action***의 **reward 기댓값(expected reward)**

$$
r(s,a) \doteq  \mathbb{E}\left[R_t  \mid  S_{t-1}=s, A_{t-1}=a\right] = \sum_{r \in \mathscr{R}}r\sum_{s^\prime \in \mathscr{S}}p(s^\prime,r \mid s,a) 
$$

- ***state-action-next-state***의 **reward 기댓값(expected reward)**

$$
r(s,a,s^\prime) \doteq  \mathbb{E}\left[R_t  \mid  S_{t-1}=s, A_{t-1}=a, S_t=s^\prime\right] = \sum_{r \in \mathscr{R}}r\frac{p(s^\prime,r \mid s,a)}{p(s^\prime \mid s,a)}
$$


MDP framework는 다양한 방법으로 다양한 문제에 적용할 수 있다. 예를 들어서, time step은 꼭 고정된 간격이 아니여도 되고, action은 로보트 팔에 적용될 volatage 처럼 low-level 컨트롤 이거나 학교에서 점심을 먹을지 말지에 대한 선택이여도 된다. 또한 state는 sensor에 대한 정보나 방(room)에 있는 물체들에 대한 설명일 수 있다. 

**MDP framework**는 상호작용으로부터 목표 지향적인(goal-directed) 학습 문제를 추상화한 것이다. 목표 지향적인(goal-directed) 행동을 취하는 어떤 문제에서도, agen와 environment 사이를 오가는 신호를 세가지로 요약할 수 있다.  agent가 선택하는 신호를 **action**이라고 하고, 선택이 이루어지는 기본이 되는 신호를 **state**라고 하며, agent의 목표인 신호를 **reward**라고 한다. MDP framework가 모든 decision-learning problem을 표현하기에는 충분하지 않을 수 있으나, 지금까지 상당히 유용하게 사용되어왔다.

물론 특정 state와 action은 작업마다 크게 다르며, 어떻게 표현 되느냐에 따라 성능에 크게 영향을 줄 수 있다.



***
### Goals and Rewards

Reinforcement Learning 에서 agent의 **목표(goal)**는 environment로 부터 받는 특별한 신호인 ***reward**를 공식 하는 것이다. 각 time step에서 reward는 단순한 숫자다. 조금 더 간단하게 얘기하면 agent의 목표(goal)는 reward의 총 합을 최대화 하는 것이다. 총 합이라는 것은 즉시 받는(immediate) reward뿐 아니라, 장기적으로 봤을 때 받을 모든 reward의 누적값이 라는 의미다. 

>That all of what we mean by goals and purposes can be well thought of as the maximization of the expected value of the cumulative sum of a received scalar signal (called reward).

reward는 reinforcement learning에서 가장 두드러지는 특징 중 하나다. 

reward에 대해서 goal을 공식화하는 것이 한계가 있어 보이지만, 유용하고 넓은 범위에서 사용 가능하다는 것을 증명해왔다. 예를 들어서, 로봇(agent)이 미로를 탈출하는 방법을 학습 시킬때 time step 마다 **-1** reward를 주었더니 이 agent는 더 빨리 탈출 하는 방법을 학습했다. 또한 재활용 로봇이 빈 캔을 찾고 수집하는 방법을 학습할 수 있도록 캔을 수집할 때마다 **+1** reward를 주어 학습시키디도 했다. 

위의 예에서 보면, agent는 항상 reward를 최대화 하기 위해서 학습한다. 만약 agent가 우리가 원하는 것을 학습하기 원한다면 agent가 reward를 최대화 하면서 목표(goal)를 달성할 수 있도록 reward를 제공해야 한다. 따라서 우리가 설정한 reward는 달성하고자 하는 목표(goal)을 확실하게 가리키도록 해야 한다. Reward는 agent와 ***how*** 가 아닌 ***what*** 을 communication하는 방법이다.



***
### Returns and Episodes

agent의 목표는 장기적으로 누적은 reward를 최대화 하는 것이다. 바로 이 누적된 reward를 $G_t$ 로 아래와 같이 표현할 수 있다. 이 값을 ***expected return*** 이라고 한다.

$$
\begin{align*}
G_t \doteq R_{t+1} + R_{t+2} + R_{t+3} + \dots + R_T && (3.7)
\end{align*}
$$

위 식에서 $T$를 final time step 이라고 한다. agent-envirionment 사이에서 이뤄지는 상호작용을 **episode** 개념으로 나눌 수 있다. 이 episode는 마치 게임에서 한 번 플레이 하는 것과 같은데, 여기서 final time step의 개념이 있는 것은 자연스러운 접근이다. 또한, 각 episode 에서 마지막 state를 **terminal state**라고 한다. episode가 게임에서 승패와 같이 특정 결과로 끝나더라도 다음 episode는 이전의 결과와 상관없이 새로 시작된다. 이런 episode로 이루어진 task를 *episodic task*라고 한다. episodic task에서 ternminal state의 존재 여부에 따라서 state set을 아래와 같이 구분한다.

- $\mathscr{S}$  : terminal state가 포함되지 않는 모든 state set
- $\mathscr{S}^+$: terminal state이 포함된 모든 모든 state set

반면에 하나의 episode가 끝나지 않는 경우가 있는데. 이를 **continuing task**라고 한다. 이런 경우 final time step 은 $T=\infty$로 무한이기 때문에, 최대화 하려고 했던 return 식 (3.7)에 문제가 생긴다. 그렇기 때문에 앞으로 다른 return 식을 사용한다. 여기에 **discounting** 라는 컨셉이 추가된다.

$$
\begin{align*}
G_t \doteq R_{t+1} + \gamma R_{t+2} + \gamma^2R_{t+3} + \dots =  \sum_{k=0}^\infty \gamma^kR_{t+k+1} && (3.8)
\end{align*}
$$

- $\gamma$: discount rate ($ 0 \le \gamma \le 1 $)

**discount rate** 는 미래(future) reward의 현재 가치을 정의한다. 미래 시점인 $k$ time step 에서 받을 reward의 현재 가치는 $\gamma^{k-1}$ 배 만큼 줄어든다. 만약 $\gamma < 1$ 이면 (3.8) 식은 finite value를 가지게 될 것이고, $\gamma = 0$이라면 agent는 즉시 받을(immediate) reward $R_{t+1}$ 만 고려해서 action $A_t$를 선택할 것이다. 하지만 이렇게 immediate reward만 고려해서 action을 선택한다면 전체 return 값은 감소할 수 있다. $\gamma$ 가 1에 가까울 수록 전체 return은 future reward를 더 많이 받아들이는데 agent가 미래에 받을 reward를 신뢰한다고 볼 수 있다.

식 (3.8)은 아래와 같이 전개할 수 있다.

$$
\begin{align*}
G_t &\doteq R_{t+1} + \gamma R_{t+2} + \gamma^2R_{t+3} + \gamma^2R_{t+4} +\dots \\
	&= R_{t+1} + \gamma (R_{t+2} + \gamma R_{t+3} + \gamma^2 R_{t+4} + \dots) \\
	&= R_{t+1} + \gamma G_{t+1} & (3.9)
\end{align*}
$$

return 식 (3.8) 에서 만약 reward가 0이 아니고 $\gamma < 1$ 이라면 식(3.8)은 finite하다. 예를 들어서 reward가 1이라고 가정하면 return은 아래와 같다. 

$$
G_t = \sum_{k=0}^\infty \gamma^k = \frac{1}{1 - \gamma}
$$



***
### Unified Notation for Episodic and Continuing Tasks
