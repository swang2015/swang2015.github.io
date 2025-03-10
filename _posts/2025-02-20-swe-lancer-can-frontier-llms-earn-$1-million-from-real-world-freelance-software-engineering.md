---
layout: post
title:  "SWE-Lancer: Can Frontier LLMs Earn $1 Million from Real-World Freelance Software Engineering?"
date:   2025-02-20 16:00:00 0000
link: https://github.com/openai/SWELancer-Benchmark
categories: AGI
tags: dataset llm
---

We introduce SWE-Lancer, a benchmark of over 1,400 freelance software engineering tasks from Upwork, valued at $1 million USD total in real-world payouts. SWE-Lancer encompasses both independent engineering tasks — ranging from $50 bug fixes to $32,000 feature implementations — and managerial tasks, where models choose between technical implementation proposals. Independent tasks are graded with end-to-end tests triple-verified by experienced software engineers, while managerial decisions are assessed against the choices of the original hired engineering managers. We evaluate model performance and find that frontier models are still unable to solve the majority of tasks. To facilitate future research, we open-source a unified Docker image and a public evaluation split, SWE-Lancer Diamond. By mapping model performance to monetary value, we hope SWE-Lancer enables greater research into the economic impact of AI model development.