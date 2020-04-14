---
katex: true
markup: "mmark"
date: 2020-03-10T08:47:11+01:00
title: "Agent 57: Outperforming the Atari Human Benchmark"
description: "" 


draft: false
---

# Agent 57

https://arxiv.org/pdf/2003.13350.pdf

**Problem:**

* Current state of the art reinforcement learning models for Atari games can only do well on a subset of the the 57 games available.
* Models that solve hard exploration problems like Pitfall can reach human level performance but can't do so for every game

**Solution**

* Agent57 incorporates many existing approaches to solve these hard exploration problems but iterates on them to achieve human level performance on all of the games and not just a subset
* The two problems that the model has to solve is,
  *  Long-term credit assignment: Games where the reward is only assigned after a very long sequence of actions which means the agent has to infer how its current action will affect states that are many steps into the future. Example for such games include *Skiing*
  *  Exploration: Games where hundreds of combinations of actions may be required before a reward is seen. Examples include *Montezuma's Revenge* and *Pitfall*
*  The long-term credit assignment is solved by improving the training stability. This is done by a new parameterization of the state-action value function that decomposes the contributions of the intrinsic and extrinsic reward so that they can be individually optimized.
*  The hard-exploration problem is solved by building on the Never Give Up model from Puigdomenech Badia et all. This model trains many policies with different exploration rates to explore as quickly and efficiently as possible. Agent57 improves upon this model by adding an adaptive meta controller which determines which policies to prioritize during the training process.

**Never Give Up (NGU)**

* NGU computes an intrinisic reward to encourage exploration.
* The reward is defined by combining per-episode ($r_t^{episodic}$) and life-long novelty ($\alpha_t$)
* Per episode novelty vanishes over the course of an episode while life-long novertly slowly vanishes over the entire training process.


The intrinsic reward is defined by,
$r_t^i=r_t^{episodic}.min(max(\alpha_t,1),L)$, where L = 5 is maximum reward scaling.

The combined reward including extrinsic,
$r_{j,t}=r_t^e+\beta_jr^i_t$. 
The $\beta$ parameter provides a means of controlling the exploration rate. Since the intrinisic reward is typically more dense than the extrinsic reward, the parameter is chosen to allow for long term horizons(high values of $\gamma_j$) for exploitative policies (small values of $\beta_j$) and small term horizons (low values of $\gamma_j$) for exploratory policies (large values of $\beta_j$).
* In practice, NGU can be unstable and fail to learn an approximation of the state-action value function possibly due to the case when the scale and sparseness of the two rewards are both different or one is more noisy than the other. This is solved by introducing an architectural modification.
* * The core idea of NGU is to jointly train a family of policies with different exploration rates using a single network architecture. These policies play the role of auxiliary tasks that help train the shared architecture. The limitation to this approach is that all policies are trained equally regardless of their contribution. This is solved by intoducing a meta-controller that selects the best policy dynamically during training.

**Improvements to NGU**

* To fix the issue of instability, the state-action value function is split:
$$Q(x,a,j;\theta)=Q(x,a,j;\theta^e) + \beta_jQ(x,a,j;\theta^i) $$
* By explicitly splitting the optimization of each reward, two separate networks can be trained too adapt better to a single function.
* This optimization is equivalent to the original optimization function in NGU.
* Adaptive exploration over a family of policies
  * Instead of treating each policy as equal, based on where the model is in during training, a particular set of policies is prioritized.
  * Early on in the process, policies with a higher exploration rate and lower discount rate are favoured which is natural since the model has very little information at that point. This is slowly shifted to the opposite as training progresses.
  * The meta controller is implemented using a non--stationary multi-arm bandit algorithm running independently on each actor. Each arm is linked to a policy in the family and at the beginning of each episode, a particular arm/policy will be executed.

**Results**

* Agent57 outperforms human scores in each of the 57 Atari games. It does not do better in certain games compared to just NGU or MuZero
* The model overall is still not optimized and work remains to be done.


