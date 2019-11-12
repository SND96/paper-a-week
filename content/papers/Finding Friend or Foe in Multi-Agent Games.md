
---
katex: true
markup: "mmark"
date: 2019-11-10T08:47:11+01:00
title: "Finding Friend or Foe in Multi-Agent Games"
description: "" 


draft: false
---

# Finding Friend or Foe in Multi-Agent Games

https://arxiv.org/pdf/1906.02330.pdf

**Problem**

* There have been multiple breakthroughs in multi-agent games in recent research, however none of these games deal with the scenario where co-operation is with unknown team mates is uncertain. 
* In games like *Dota* and *Capture the Flag* there is no ambiguity on who to co-operate with.
* In hidden role games like *The Resistance: Avalon*, discovering the roles of each player is a challenging task with similarities to deception games like poker. 
* Agents will have to learn both deception and the ability to counter this deception.


**Solution**

* Develops an algorithm called *DeepRole* which is a multi-agent reinforcement learning method that addresses the question of who to cooperate with and how. 
* This algorithm is applied to a hidden role game in which players join different teams at the start of the game and adopt roles that are not known to all players in the game.
* During the course of the game, the agents will try to deduce the roles of the other players while ensuring their own role does not get discovered.
* Uses counterfactual regret minimization (CFR) to reason about joint beliefs and partially observable actions based on consistency with the observed outcomes. 


**Setting**

* *The Resistance: Avalon* is a multi-agent imperfect information game which is used as a testing bed for the *DeepRole* algorithm.
* In this game there are 5 players with 3 randomly assigned to the Resistance team and 2 assigned to the Spy team. One member of the Resistance is privately cchosen to be Merlin who can see the roles of all other players. One member of the Spy team is assigned as the Assassin. The Spy team wins if the Assassin guesses the identity of the Merlin.
* Each round consists of players voting for a pair of players to go on a mission and this mission's success is dependent on the privately cast votes of the pair who are sent. If three missions succeed, the Resistance team wins.

![6d2f113f.png](/attachments/dbb66ae7.png)

**DeepRole**

* CFR requires a public game tree from player action which is easily obtainable in games like poker where all player actions are visible.
* In hidden role games, key actions are done in private and to support this, the public gagme tree is made into a history of third person observations instead of just actions.
* Using the public game tree, a joint posterior belief $b(\rho|h)$ over initial assignment of roles $\rho$. This belief represents the joint probability that each players has role specified in $\rho$ given $h$ which represents history of observations so far. 
* The joint posterior can be estimated by using individual players likelihoods.
![Screenshot 2019-11-12 at 00.33.55.png](/attachments/eb738e35.png)
* $I_i(h,\rho)$ represents the information set implied by public history $h$. The indicator term zeros the probability that nay $\rho$ is logically inconsistent with the public game treee by removing impossible outcomes.
* Actions in Avalon are not inherently related to each other. Betting 105 chips in poker is very similar to betting 104 chips, but voting a mission up is distinct from voting it down.
* The size of Avalon's game tree comes from the number of players rather than the available actions.
* The authors partition the game tree to enable a deep network to more easily traverse the branches.

![Screenshot 2019-11-12 at 00.41.15.png](/attachments/a3519019.png)
* The paper also details a Value network which is calculated for private information $I$ for each player $i$ as: 

![Screenshot 2019-11-12 at 00.41.09.png](/attachments/f3f19d76.png)

**Conclusions**

* DeepRole surpassed both human and existing agents in competitions.
* The results were achieved through the addition of a deductive reasoning system using CFR and win probability layer for depth-limited search.
* Future work includes using DeepRole for ground language, enabling better coordination through communication. 

