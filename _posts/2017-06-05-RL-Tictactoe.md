---
layout: post
title:  "Reinforcement Learning for Beginners: Tic-Tac-Toe"
date:   2017-06-05 7:00:00 +0800
categories: machine-learning
tags: feature reinforcement-learning code-example
math: true
background: /images/bg/bg_futurama.jpg
---

You might have heard of _reinforcement learning_, lots of its magical stories from media and are curious about what it is. Reinforcement learning is about getting an agent learn to act given rewards. RL is inspired by behavioral psychology. The process is just like teaching a pet: you don't tell it what to do, but you reward/punish it when it does the right/wrong thing. There are plenty of [online tutorials](#resources) which give you comprehensive ideas about reinforcement learning.

## The Model

We can describe the RL process as follows. At each step, the agent receives observation and reward, and selects an action. The environment receives the action and emits another observation and reward. The goal is to maximize the total reward in long run.

<div class="post-img">
	<img src="/images/rl/rl_model.jpeg" width="40%">
</div>

A __policy__ is the agent's behavior, it's a mapping from state to action. Whereas the reward signal gives immediate score, a __value function__ specifies a long-term desirability. Even a state yiels low rewards it might still have high value because its consequent states yield high rewards. Let's illustrate the idea with a really simple example ([with code](https://github.com/swang2015/data-science-messy-notes/blob/master/reinforcement-learning/tictactoe.py)).

## A Simple Example: Training a Tic-Tac-Toe Player <sup>[1](#resources)</sup>

Tic-Tac-Toe is a classic child's game. Two players fullfill a 3x3 board in turn with Xs and Os until one wins by placing three marks in a row. The problem is to train an agent to play the game and maximize its chances of winning.

<div class="post-img">
	<img src="/images/rl/rl_tictactoe.png" width="65%">
</div>

How do we apply RL to solve this problem? In this game, the states of the board are finite. We search a space of _policies_ and greedily select the best one with high potential to beat the opponent. The chance of winning for each policy is estimated via _value function_. As the agent plays, value of a state _V(s)_ is backed up to be closer to the value after the best move _V(s')_, which can be written as @@V(s)\leftarrow V(s)+\alpha[V(s')-V(s)]@@. _α_ is the _step-size parameter_ and influences the learning rate. This update method is an example of _temporal-difference_ learning. When the system's random number is below a threshold ε, the agent ignores suggested move and takes a _exploratory move_.

Up til now, our agent is well-trained and ready to play with. [Take a try](https://github.com/swang2015/data-science-messy-notes/blob/master/reinforcement-learning/tictactoe.py)! This example illustrates how a RL method works -- there's no supervisor or prior knowledge, the agent learns from interacting with environment with feedback. It's also a remarkable feature that a RL agent can consider the delayed effects. It's like it looks ahead for the best choice over a time span to achieve its goal in the future.


## Discussions

- The agent prefers to take previous move with highest score to maximize reward. Also the agent has to try moves which it has not take before in order to improve policies, so the tradeoff between _exploration_ and _exploitation_ becomes a challenge since no one would guanrantee which is nicer to approach the goal.
- Besides the _temporal-difference learning_, some other approximation methods to estimate value function include _Q-learning_, _SARSA_, etc.
- RL can be used to solve complex problems whose states are huge or even infinite. We can estimate their value functions through neural network, combinations of features, etc.

## Resources

1. [Richard Sutton's textbook](http://incompleteideas.net/sutton/book/the-book.html)
2. [David Silver's lecture notes](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html)
