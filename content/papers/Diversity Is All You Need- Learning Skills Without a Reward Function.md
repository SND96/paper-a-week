---
katex: true
markup: "mmark"
date: 2020-10-28T08:47:11+01:00
title: "Diversity Is All You Need: Learning Skills Without a Reward Function"
description: "" 


draft: false
---

# Diversity Is All You Need: Learning Skills Without a Reward Function

### TLDR:
Uses a mix of discriminatory methods/goals for maximizing information and entropy to learn a diverse set of tasks in an unsupervised manner.

## Introduction:

* Learning skills without any reward signals is practically very useful especially for RL tasks with a long horizon.
* The authors propose a method to not only learn skills that are generalizable but also diverse so that they can encompass the maximum amount of behaviour space.
* Uses a discriminatory goal of maximizing an information theoretic objective (to learn general skills) while maximizing an entropy policy (to increase the diversity of skills)


![Screenshot 2020-10-06 at 01.35.56.png](/attachments/941f4402.png)


## Diversity is all you need: 

* How it works:
  * Skills to dictate the states that the agent visits or skills affect the policy. This idea is encoded by maximizing the mutual information between skills and states.
  * Different skills should visit different states and states, not actions, should be used to distinguish skills. This is done by the above method of mutual information maximization and to distinguish skills, the mutual information between the skills and action given the state should be minimized.
  $$F(\theta)=H[A|S,Z] - H[Z|S] +H[Z]$$
$$F(\theta)\geq H[A|S,Z] + E_{z\in p(z), s\in\pi(z)}[\log q_\phi(z|s)-\log p(z)] \triangleq G(\theta,\phi)$$

* Implementation
  * Uses a soft actor critic, learning a policy $$\pi(a|s,z)$$ that is conditioned on latent variable $$z$$

* Stability
  * DIAYN forms a co-operative game which makes it different from adversial RL games and allows it to avoid the saddle point instabilities of those approaches.


  




