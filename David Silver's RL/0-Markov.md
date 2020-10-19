#### **马尔可夫性质**	Markov Property 

当一个随机过程在给定现在状态及其过去所有状态下，其**未来状态的条件概率分布仅依赖与当前状态**。定义$S$为可能状态的集合，$s_t$为观测到的状态序列（$s_t\in S$），$a_t$为可能的动作集合。$P(·)$为历史状态和历史动作的概率函数，表示在$S$上的**状态转移（trasition dynamics）**概率分布。
$$
P(s_{t+1}|s_t,a_t,\dots,s_1,a_1)=P(s_{t+1}|s_t,a_t)
$$
#### **马尔可夫过程**	Markov Process 	$<S,\mathcal{P}>$

马尔可夫过程是一个随机过程。是满足马尔可夫性质的状态序列。

#### **马尔可夫奖励过程**	Markov Reward Process	$<S,\mathcal{P},R,\gamma>$

带有**价值判断**的马尔可夫过程，该价值能够告诉我们该状态有多好。

马尔可夫奖励过程可以由一组参数描述：$(S,\mathcal{P},\mathcal{R},\mathcal{\gamma})$

- $\mathcal{S}$是状态的有限集；

- $\mathcal{P}$是状态转移概率矩阵，

  $\mathcal{P_{ss'}}=\mathbb{P}[S_{t+1}=s'|S_t=s]$

- $\mathcal{R}$是奖励函数，$\mathcal{R_s}=\mathbb{E}[R_{t+1}|S_t=s]$
- $\gamma$是衰减因子，$\gamma\in[0,1]$

> 因为$S_t$是状态转移概率矩阵确定的，所以使用的期望？:thinking:

定义$G_t$为决策过程中我们能够得到的奖励总和（回报）。$G_t$没使用期望，是因为只是一个样本的计算值。
$$
G_t=R_{t+1}+\gamma R_{t+2}+\dots=\sum_{k=0}^{\infty}\gamma^kR_{t+k+1}
$$

**值函数**	定义为从状态$s$开始，回报的期望。$v(s)=\mathbb{E}[G_t|S_t=s]$

#### **Bellman 方程** Bellman Equation

值函数的递归分解。
$$
\begin{align}
v(s)&=\mathbb{E}[G_t|S_t=s]\\
&=\mathbb{E}[R_{t+1}+\gamma R_{t+2}+\gamma^2R_{t+3}|S_t=s]\\
&=\mathbb{E}[R_{t+1}+\gamma (R_{t+2}+\gamma R_{t+3})|S_t=s]\\
&=\mathbb{E}[R_{t+1}+\gamma G_{t+1}|S_t=s]\\
&=\mathbb{E}[R_{t+1}+\gamma v(S_{t+1})|S_t=s]\\
\end{align}
$$
将原来的值分为了两个部分：1.立即奖励$R_{t+1}$； 2.后续状态的值函数。

**Bellman方程的矩阵形式**
$$
\begin{align}
v&=R+\gamma\mathcal{P}v\\
(1-\gamma\mathcal{P})v&=R\\
v&=(1-\gamma\mathcal{P})^{-1}R
\end{align}
$$
复杂度为$\mathcal{O}(n^3)$，$n$表示状态数量。

> 对bellman方程中的立即奖励使用贪心策略就变成了一个动态规划问题。:thinking:

#### 马尔可夫决策过程 Markov Decision Process	 $<S,A,\mathcal{P},R,\gamma>$

- $\mathcal{S}$是状态的有限集；

- $A$是动作的有限集；

- $\mathcal{P}$是状态转移概率矩阵，

  $\mathcal{P_{ss'}}=\mathbb{P}[S_{t+1}=s'|S_t=s]$

- $\mathcal{R}$是奖励函数，$\mathcal{R_s}=\mathbb{E}[R_{t+1}|S_t=s]$

- $\gamma$是衰减因子，$\gamma\in[0,1]$

**策略  policy**     根据制定状态所采取的动作的分布，完整定义了个体的行为方式。$\pi(a|s)=\mathbb{P}[A_t=a|S_t=s]$

**状态价值函数与动作价值函数**	状态价值函数表明了遵循当前策略，截至到最终态所能获得回报的期望。动作价值函数表明了在执行策略时，从当前状态到最终状态执行相应的动作所能获得回报的期望。
$$
v_\pi(s)=\mathbb{E}_\pi[G_t|S_t=s]\\
q_\pi(s)=\mathbb{E}_\pi[G_t|S_t=s,A_t=a]
$$
**状态价值函数与动作价值函数的bellman 方程**
$$
v_\pi(s)=\mathbb{E}_\pi[R_{t+1}+\gamma v_\pi(S_{t+1}|S_t=s)]\\
q_\pi(s,a)=\mathbb{E}_\pi[R_{t+1}+\gamma q_\pi({S_{t+1},A_{t+1})}|S_t=s,A_t=a]
$$
**最优化MDP**	存在一个策略，满足 $\pi_*\geq\pi$，此时$v_{\pi_*}=v_*(s)$,$q_{\pi_*}(s,a)=q_{*}(s,a)$