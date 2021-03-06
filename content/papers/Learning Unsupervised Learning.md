---
katex: true
markup: "mmark"
date: 2019-10-27T08:47:11+01:00
draft: false
title: "Learning Unsupervised Learning Rules"
---

# Learning Unsupervised Learning Rules

https://arxiv.org/pdf/1804.00222.pdf

**Problem**

* Unsupervised learning has yet to fulfil the potential of being powerful in situations with limited labelled data.
* Ideally learned representations should integrate high level attributes of data in the representations generated. However, possibly due to utilising incorrect target tasks during training, useful representations are only produced as a side effect.

**Solution**

* Use a semi-supervised task (meta objective) to help build improve the quality of representations using the unsupervised model.
* The unsupervised update rule is recast as a transfer learning problem which targets the usefulness of a representation generated from unlabelled data for later supervised tasks

**Meta Learning**

* Meta Learning in simplest terms is the process of learning how to learn. The machine trains on data which is useful for it to be able to generalise better to any task.
* Meta-Learning algorithms consist of two levels of learnings or ‘loops’.
	* An inner loop where some form of learning occurs like optimization
	* An outer loop or meta training loop which optimises some aspect of the inner loop. 
	* The performance of the inner loop is quantified by the inner loop and the aspects of the inner loop that are modified by the outer loop are called meta-parameters
* This paper models the unsupervised network as the inner loop of meta-learning

**Meta Objective**: 

Use the learned unsupervised representations in a supervised setting. The optimisation of this object will directly influence the unsupervised representation learning


**Unsupervised Update Rule**

* The update rule is  /Neuron local/(Research this exact term), which means the updates are a function of pre- and post- synaptic neutrons in the base model.
* To build the updates, each neutron has an update network associated with it. All update networks share certain parameters and are only evaluated during unsupervised training as they are not part of the base model
* The backdrop  error signal is generated by the corresponding update network for each unit and propagated backward using a set of learned backward weights as opposed to the transpose of the forward weights in regular backdrop. Depicted pictorially below

![Screenshot 2019-02-15.png](/attachments/b07b60e6.png)

**Meta Objective**

* The meta-objective determines the quality of the unsupervised representations. This loss needs to be differentiable else stochastic gradient descent can not be applied.
* The meta-objective used is based on fitting a linear regression to labelled examples with a small number of data points

**Experiments and Conclusion**

* The method is shown to match or exceed existing unsupervised learning tasks.
* The update rule is flexible enough to be used with different network architectures
* Meta-Learning is shown to be useful for learning complex optimisation tasks and can be further expanded upon in this domain