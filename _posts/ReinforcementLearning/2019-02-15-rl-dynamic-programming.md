---
layout: post
title: 강화학습 정리 - Dynamic Programming
category: Reinforcement Learning
tag: [강화학습, RL]
use_math: true
---


## 4. Dynamic Programming

**[Dynamic programing (DP)](https://en.wikipedia.org/wiki/Dynamic_programming)** 은 알고리즘 범주 중 하나로, MDP 에서 완벽한 environment 의 model 이 주어졌을 때 optimal policy 를 계산할 수 있다. DP 는 reinforcement learning 에서 위의 조건을 만족하지 못하는 경우가 많기 때문에 사용에는 한계가 있지만, 여전히 이론적으로 매우 중요하다. DP 는 앞으로 다룰 내용들을 이해하는데 꼭 필요한 기반이 된다. 

이 챕터에서는 주로 environment 가 **finite MDP** 라고 가정할 것이다. 또한 **dynamics** 가 $p(s^\prime,r \mid s,a)$ 으로 주어진다. $s \in \mathscr{S}, a \in \mathscr{A}(s), r \in \mathscr{R}, s^\prime \in \mathscr{S}^+$ ($\mathscr{S}^+$ 는 episodic 문제에서 terminal state 를 포함)

Reinforcement learning 과 DP 의 핵심 아이디어는 좋은 policy 를 찾기 위해서 value function 을 잘 구조화하는 것이다. 이 챕터에서는 DP 가 value function 을 계산하기 위해서 어떻게 사용하는지 알아볼 것이다. 만약 우리가 **Bellman optimality equation** 을 만족하는 $v_\*$ 혹은 $q_\*$ 를 알고 있으면 **optimal policy** 는 쉽게 구할 수 있다. 

$$
\begin{align*}
 	v_*(s) &= \underset{a}{\text{max}} \mathbb{E} \left[ R_{t+1} + \gamma v_*(S_{t+1}) \mid S_t = s, A_t = a \right] \\
	&= \underset{a}{\text{max}} \sum_{s^\prime, r}p(s^\prime, r \mid s, a) \left[ r + \gamma v_*(s^\prime) \right] & (4.1)
\end{align*}
$$


$$
\begin{align*}
	q_*(s,a) &= \mathbb{E} \left[ R_{t+1} + \gamma \underset{a^\prime}{\text{max}}q_*(S_{t+1}, a^\prime) \mid S_t=s, A_t = a \right] \\
	&= \sum_{s^\prime, r}p(s^\prime, r \mid s, a) \left[ r + \gamma \underset{a^\prime}{\text{max}}q_*(s^\prime, a^\prime)) \right] & (4.2)
\end{align*}
$$

앞으로 다루겠지만, DP 알고리즘은 Bellman equation 을 value function 의 근사치를 얻기 위한 업데이트 규칙으로 변환됨으로써 얻어진다.

> (4.1) 식에서 $v_\*(s)$ 를 구하기 위해서는 $v_\*(s^\prime)$ 가 먼저 업데이트 되어야 합니다. 이 챕터에서는 재귀적인 방법으로 계산하는 것이 아니라, 사전에 미리 구해진 $v_\*(s^\prime)$ 의 값을 사용합니다. 결국 반복적으로 업데이트 하면서 원하는 value function 에 근사합니다.



***
### Policy Evaluation (Prediction)

DP 에서 policy $\pi$ 에 대한 state-value function 을 **policy evaluation** 이라고 한다. 이전 장에서 모든 State s 에 대해 아래와 같이 정의 했었다.

$$
\begin{align*}
v_\pi(s) &\doteq  \mathbb{E}_\pi\left[G_t  \mid  S_t=s \right]  \\
			&= \mathbb{E}_\pi \left[R_{t+1} + \gamma G_{t+1}  \mid  S_t=s \right] &  (from (3.9))\\
			&= \mathbb{E}_\pi \left[R_{t+1} + \gamma v_{\pi}(S_{t+1})  \mid  S_t=s \right] & (4.3)\\
			&= \sum_a \pi(a \mid s) \sum_{s^\prime, r} p(s^\prime,r \mid s,a) \left[ r + \gamma v_\pi(s^\prime) \right], \text{for all } s \in \mathscr{S}, & (4.4)
			
\end{align*}
$$

$\pi(a \mid s)$ 는 policy $\pi$ 를 따랐을 때 state $s$ 에서 action $a$ 를 선택할 확률이다. 기댓값 $\mathbb{E}$ 에는 $\pi$ 에 따라 정해지기 때문에 $\pi$ 가 붙는다. 

만약 environment 의 dynamic 를 완벽하게 알고 있다면, 식 (4.4) 는 선형 연립방정식으로 풀 수 있다. 그러나 우리가 해결하려는 문제에는 반복적인 계산으로 방법이 더 적합하다. 연속적인 approximate value function 을 $v_0, v_1, v_2 ..., $ 으로 간주했을 떄, $v_\pi$ 에 대한 Bellman equation 을 사용해서 순차적으로 값을 계산할 수 있다. 여기서 각 $v_k$ 는 final state 를 포함한 모든 State $\mathscr{S}^+$ 에 맵핑 된다. 

$$
\begin{align*}
v_{k+1}(s) &\doteq \mathbb{E}_\pi \left[R_{t+1} + \gamma v_k(S_{t+1})  \mid  S_t=s \right] \\
			&= \sum_a \pi(a \mid s) \sum_{s^\prime, r} p(s^\prime,r \mid s,a) \left[ r + \gamma v_k(s^\prime) \right], \text{for all } s \in \mathscr{S}, & (4.5)
			
\end{align*}
$$

> 식 (4.4) 에서 (4.5) 로 넘어오는 식이 매우 중요하다고 생각합니다. 식 (4.5) 를 여러번 계산한다고 생각했을 때, $v_{k+1}$ 을 계산할 때 필요한 $v_k$ 는 이미 이전 시점에서 계산 된 해를 가지고 있습니다. $v_k$ 에서 모든 $s \in \mathscr{S}$ 에 대해서 계산하고 다음 $v_{k+1}$ 로 넘어간다고 생각하시면 편할 겁니다.

시퀀스 {$v_k$} 는 $k$ 가 무한으로 갈 때 $v_\pi$ 로 수렴한다. 이렇게 반복적으로 업데이트 하는 알고리즘을 **iterative policy evaluation** 이라고 한다. 

$v_k$ 으로부터 $v_{k+1}$ 에 대한 근사값(approximation) 을 구하기 위해서, 각 state $s$ 에서 동일한 iterative policy evaluation 을 적용한다. 이 작업은 기존 $s$ 의 값을 새로운 값으로 대체하는데, 이 값은 기존 $s$ 에 이어지는 다음 state 들의 값과 expected immediate reward 로부터 계산된다. 이런 업데이트를 **expected update** 라고 한다. 각 iterative policy evaludation 는 새로운 appoximate value function $v_{k+1}$ 를 구하기 위해서 한번 모든 state 의 값을 업데이트 한다. DP 알고리즘에서 완료된 update 를 expected update 라고 한다. 왜냐하면 다음 state 를 샘플링 하는 것이 아니라 가능한 모든 다음 state 를 기반으로 업데이트 하기때문이다. 

식 (4.5) 을 기반으로 iterative policy evaluation 을 프로그래밍 하기 위해서는 두개의 배열이 필요하다. 하나는 이전 값을 보관하는 $v_k(s)$ 이고, 또 다른 하나는 새로운 값을 보관하는 $v_{k+1}(s)$ 이다. 물론 하나의 배열을 사용해서 이전 값을 새로운 값으로 덮어씌워도 된다. 만약 그렇게 하면 업데이트되는 순서에 따라서 이미 업데이트 된 값이 이전 값 대신에 사용될 수도 있지만, 그렇다 하더라도 $v_\pi$ 에 수렴하게 된다. 사실 이런 방법이 두개의 배열을 사용하는 것보다 더 빠르게 수렴한다. 왜냐하면 업데이트된 새로운 값을 바로 사용할 수 있기 때문이다. 이런 알고리즘을 **in-place** 알고리즘 이라고 하며, 앞으로 DP 에서는 주로 이 방법을 사용할 것이다. 

다음은 **Iterative policy evaluation** 의 **in-place** 버전에 대한 슈도코드다.

![image](/assets/2019-02-15-rl-dynamic-programming/pic1.png)



***
### Policy Iteration






