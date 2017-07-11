---
layout: post
title:  "Statistical Language Learning II - PCFG and tree CRF (draft)"
date:   2015-04-05 01:00:00
categories: natural-language-processing
tags: parsing nlp crf
math: true
---

## Probabilistic Context-Free Grammar

The probability of a parse tree _t_ is @@ p(t) = \prod_{i=1}^n q(N_i \rightarrow \zeta_i) @@. @@N_i \rightarrow \zeta_i@@ are rules in _t_. @@ \zeta_i @@ is a sequence of nonterminals and terminals. For Chomsky Normal Form rules, @@ \zeta_i @@ is composed of @@ N^jN^k @@ or @@ w^j @@. _N_ is nonterminal and _w_ is terminal.

## Tree CRF

Rule scores: @@ S(N^i \rightarrow \zeta^i, p, q) = \sum_{k=1}^F \lambda_k (N^i \rightarrow \zeta^i) f_k(w_1...w_m, p, q, N^i \rightarrow \zeta^i) @@

