---
layout: post
title:  "Statistical Language Learning I - HMM and Linear Chain CRF (draft)"
date:   2015-04-01 20:00:00
categories: natural-language-processing
tags: POStagging nlp crf
math: true
---

## Part-of-Speech Tagging

Part-of-Speech(POS) tagging is a basic problem in nlp. Many words can be in one or more POS class. The aim is to assign a sequence of words with POS tags like _noun_, _verb_, _adjective_, etc. For example, given a sentence "Edward went to supermarket", the labeling can be "Edward/_noun_ went/_verb_ to/_preposition_ supermarket/_noun_".

Here, we have three things to worry about: the _observed sequence_ **x** which are the words, the hidden _states_ **y** which are the tags, and the _transition process_. Also we have three critical questions to answer:

- given the model, calculate **probability of the observed sequence**;
- how to **estimate parameters of the model** from training samples;
- the **decoding** problem, which is to efficiently find possible states of a sentence.

## Hidden Markov Model

HMM makes two independence assumptions:
- each state @@y_t@@ depends only on its immediate predecessor @@y_{t-1}@@;
- each observation @@x_t@@ depends only on the current state @@y_t@@.

HMM is made up of a chain of @@s_i \xrightarrow{w_k} s_j@@, which means at any time _t_ a state @@s_i@@ transits from a state @@s_j@@ and we see a word @@w_k@@. HMM combines the transition distribution and the emission distribution, so the joint probability of the state sequence **y** and the observations **x** is modeled as:

%%p(\mathbf{y},\mathbf{x}) = \prod_{t=1}^T p(y_t\|y_{t-1})p(x_t\|y_t)%%

We define a transition @@\Psi_t(s_j, s_i, w_k) := p(y_t=s_j\|y_{t-1}=s_i)p(x_t=w_k\|y_t=s_j)@@, so HMM can be rewritten as: @@p(\mathbf{y},\mathbf{x}) = \prod_{t=1}^T \Psi_t(y_t, y_{t-1}, x_t)@@.

#### Observation probability

The probability of the word sequence is computed using forward/backward algorithm.

We define a set of _forward variables_: @@\alpha_t(s_j) := p(\mathbf{x}\_{1...t}, y_t=s_j) = \sum\_{s_i \in S} \Psi_t(s_j, s_i, x_t) \alpha_{t-1}(s_i)@@, so the observation probability @@p(\mathbf{x}) = \sum_{y_T} \alpha_T(y_T)@@.

And we define a set of _backward variables_: @@\beta_t(s_i) := p(\mathbf{x}\_{t+1...T}, y_t=s_i) = \sum_{s_j \in S} \Psi_{t+1}(s_j, s_i, x_{t+1})\beta_{t+1}(s_j)@@, so the observation probability can be computed as @@p(\mathbf{x})= \beta_0(y_0) = \sum_{y_1} \Psi_1(y_1, y_0, x_1) \beta_1(y_1)@@.


#### Parameter estimation

em algorithm

#### Decoding with HMM

viterbi

## Linear-chain Conditional Random Field

Linear-chain CRF is closely related to HMM. Both are sequence models except that HMM is _generative_ and linear-chain CRF is _discriminative_. The principal advantage of discriminative modeling is that it can include richer and overlapping features. Linear-chain CRF takes the form as below, which can be derived from HMM.

%%
p(\mathbf{y} \| \mathbf{x}) = \frac{1} {Z(\mathbf{x})} \prod_{t=1}^T exp\\{\sum_{k=1}^K \theta_k f_k (y_t, y_{t-1}, x_t)\\}
%%

Z(**x**) is a normalization function. @@Z(\mathbf{x}) = \sum_{y'} \prod_{t=1}^T exp\\{\sum_{k=1}^K \theta_k f_k (y_t', y_{t-1}', x_t)\\}@@.

@@ \\{f_k(y_t, y_{t-1}, x_t)\\}_{k=1}^K @@ is a set of feature functions, which can represent the current word, or prefixes/suffixes, etc.

#### Observation probability

The forward/backward algorithm for linear-chain CRFs is identical to HMM, except that we define @@\Psi_t(y_t, y_{t-1}, x_t) = exp \\{ \sum_k \theta_k f_k (y_t, y_{t-1}, x_t) \\}@@. And the conditional probability of **y** given **x** becomes: @@p(\mathbf{y} \| \mathbf{x}) = \frac{1}{Z(\mathbf{x})} \prod_{t=1}^T \Psi_t(y_t, y_{t-1}, x_t)@@.

#### Parameter estimation

Parameter estimation of linear-chain CRF is performed by penalized maximum likelihood @@\mathscr{l}(\theta) = \sum_{i=1}^Nlog p(\mathbf{y}^{(i)} \| \mathbf{x}^{(i)})@@.



#### Decoding with linear-chain CRF

viterbi