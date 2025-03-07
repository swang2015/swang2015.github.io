---
layout: post
title:  "WarriorCoder: Learning from Expert Battles to Augment Code Large Language Models"
date:   2025-02-24 18:40:00 0000
link: https://arxiv.org/abs/2412.17395
categories: AGI
tags: llm codebase
---

Abstract: Despite recent progress achieved by code large language models (LLMs), their remarkable abilities are largely dependent on fine-tuning on the high-quality data, posing challenges for data collection and annotation. To address this, current methods often design various data flywheels to collect complex code instructions, enabling models to handle more intricate tasks. However, these approaches typically rely on off-the-shelf datasets and data augmentation from a limited set of proprietary LLMs (e.g., Claude, GPT4, and so on), which restricts the diversity of the constructed data and makes it prone to systemic biases. In this paper, we propose WarriorCoder, a novel paradigm learns from expert battles to address these limitations. Specifically, we create an arena where leading expert code LLMs challenge each other, with evaluations conducted by impartial judges. This competitive framework generates novel training data from scratch, leveraging the strengths of all participants. Experimental results show that WarriorCoder achieves state-of-the-art performance compared to previous models of the same size, even without relying on proprietary LLMs.

A reproduction of the work: https://huggingface.co/HuggingMicah/warriorcoder_reproduce