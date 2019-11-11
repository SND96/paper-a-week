---
katex: true
markup: "mmark"
date: 2019-10-13T08:47:11+01:00
draft: false
title: "Guiding Policies with Language via Meta-Learning"
---

# Guiding Policies with Language via Meta-Learning

**Problem**:

* Reward functions and imitation learning have disadvantages for policy learning
* Reward functions require manual engineering while demonstrations require a human expert to be able to perform the task

**Solution:**

* Natural language instructions can overcome those disadvantages by being able to specify in detail the goals of the agent
* However, one instruction would not be enough so it is proposed that iterative language corrections are provided to an agent. These corrections gradually guide the agent towards the final desired goal.
* These corrections can be far more natural to provide than abstract reward functions or demonstrations

**Algorithm**

* End-to-end algorithm for grounding iterative language corrections by using a multi-task setup to meta-train a model that can incorporate its previous behaviour and a correction so as to correct its policy to produce better actions
	* Agent attempts a task
	* Agent provided with a language correction after each attempt. This correction is language phrase according to some unknown stochastic function of the trajectory
	* Correction indicates how to improve the current trajectory to bring it closer to accomplishing the goal

**Model:**

![Screenshot 2019-02-26 at 23.13.35.png](/papers/attachments/e33ef43b.png)
* Instructions are provided as a sequence of words which are converted into a sequence of word embeddings.
* Each previous trajectory is processed by a 1D CNN to generated a trajectory embedding. The correction $C_i$, similar to the language description is converted into a sequence of word-embeddings.
* Policy module has to integrate the high level description embedded into $Z_{im}$, the actionable changes from the correction module $Z_{cm}$ and environment state _s_ to generated the right action
* By iteratively incorporating language corrections, the model is in effect learning how to learn better analogous to meta-reinforcement learning recurrent models

**Meta-training the GPL model**

* Meta-training tasks which will teach the model how to draw corrections from the task pool