---
layout: post
title:  "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning"
date:   2025-01-22 19:00:00 0000
link: https://github.com/deepseek-ai/DeepSeek-R1
categories: AGI
tags: nlu llm rl pretrained-models
---

In this study, we demonstrate that reasoning capabilities can be significantly improved through large-scale reinforcement learning (GRPO), even without using supervised fine-tuning as a cold start. Furthermore, performance can be further enhanced with the inclusion of a small amount of cold-start data. We present:
(1) DeepSeek-R1-Zero, which applies RL directly to the base model without any SFT data, and
(2) DeepSeek-R1, which applies RL starting from a checkpoint fine-tuned with thousands of long Chain-of-Thought (CoT) examples. 
(3) Distill the reasoning capability from DeepSeek-R1 to small dense models.
To support the research community, we open-source DeepSeek-R1-Zero, DeepSeek-R1, and six dense models (1.5B, 7B, 8B, 14B, 32B, 70B) distilled from DeepSeek-R1 based on Qwen and Llama.