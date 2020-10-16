#### **马尔可夫性质**	Markov Property 

当一个随机过程在给定现在状态及其过去所有状态下，其==未来状态的条件概率分布仅依赖与当前状态==。定义$S$为可能状态的集合，$s_t$为观测到的状态序列（$s_t\in S$），$a_t$为可能的动作集合。$P(·)$为历史状态和历史动作的概率函数，表示在$S$上的**状态转移（trasition dynamics）**概率分布。
$$
P(s_{t+1}|s_t,a_t,\dots,s_1,a_1)=P(s_{t+1}|s_t,a_t)
$$
#### **马尔可夫过程**	Markov Process

马尔可夫过程是一个随机过程。是满足马尔可夫性质的状态序列。

#### **马尔可夫奖励过程**	Markov Reward Process

带有价值判断的马尔可夫过程，该价值能够告诉我们该状态有多好。

马尔可夫奖励过程可以由一组参数描述：$(S,\mathcal{P},\mathcal{R},\mathcal{\gamma})$

- $~~\mathcal{S}$是状态的有限集；

- $\mathcal{P}$是状态转移概率矩阵，

  $\mathcal{P_{ss'}}=\mathbb{P}[S_{t+1}=s'|S_t=s]$

- $\mathcal{R}$是奖励函数，$\mathcal{R_s}=\mathbb{E}[R_{t+1}|S_t=s]$
- $\gamma$是衰减因子，$\gamma\in[0,1]$

> 因为$S_t$是状态转移概率矩阵确定的，所以使用的期望？:thinking:

定义$G_t$为决策过程中我们能够得到的奖励总和
$$
G_t=R_{t+1}+\gamma R_{t+2}+\dots=\sum_{k=0}^{\infty}\gamma^kR_{t+k+1}
$$
