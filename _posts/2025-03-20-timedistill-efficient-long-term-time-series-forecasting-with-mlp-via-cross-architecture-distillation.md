---
layout: post
title:  "TimeDistill: Efficient Long-Term Time Series Forecasting with MLP via Cross-Architecture Distillation"
date:   2025-03-20 13:20:00 0000
link: https://arxiv.org/abs/2502.15016
categories: ML
tags: time-series
---

Abstract: Transformer-based and CNN-based methods demonstrate strong performance in long-term time series forecasting. However, their high computational and storage requirements can hinder large-scale deployment. To address this limitation, we propose integrating lightweight MLP with advanced architectures using knowledge distillation (KD). Our preliminary study reveals different models can capture complementary patterns, particularly multi-scale and multi-period patterns in the temporal and frequency domains. Based on this observation, we introduce TimeDistill, a cross-architecture KD framework that transfers these patterns from teacher models (e.g., Transformers, CNNs) to MLP. Additionally, we provide a theoretical analysis, demonstrating that our KD approach can be interpreted as a specialized form of mixup data augmentation. TimeDistill improves MLP performance by up to 18.6%, surpassing teacher models on eight datasets. It also achieves up to 7X faster inference and requires 130X fewer parameters. Furthermore, we conduct extensive evaluations to highlight the versatility and effectiveness of TimeDistill.