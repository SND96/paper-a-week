---
katex: true
markup: "mmark"
date: 2019-10-26T08:47:11+01:00
title: "Finding Friend or Foe in Multi-Agent Games"
description: "" 


draft: false
---

# Finding Friend or Foe in Multi-Agent Games

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

![Screenshot 2019-11-08 at 01.15.08.png](/attachments//6d2f113f.png)

**DeepRole**
* 