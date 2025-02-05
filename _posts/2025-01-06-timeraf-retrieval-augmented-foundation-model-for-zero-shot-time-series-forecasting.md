---
layout: post
title:  "TimeRAF: Retrieval-Augmented Foundation model for Zero-shot Time Series Forecasting"
date:   2025-01-06 04:00:00 0000
link: https://arxiv.org/abs/2412.20810
categories: ML
tags: time-series rag
---

Abstract: Time series forecasting plays a crucial role in data mining, driving rapid advancements across numerous industries. With the emergence of large models, time series foundation models (TSFMs) have exhibited remarkable generalization capabilities, such as zero-shot learning, through large-scale pre-training. Meanwhile, Retrieval-Augmented Generation (RAG) methods have been widely employed to enhance the performance of foundation models on unseen data, allowing models to access to external knowledge. In this paper, we introduce TimeRAF, a Retrieval-Augmented Forecasting model that enhance zero-shot time series forecasting through retrieval-augmented techniques. We develop customized time series knowledge bases that are tailored to the specific forecasting tasks. TimeRAF employs an end-to-end learnable retriever to extract valuable information from the knowledge base. Additionally, we propose Channel Prompting for knowledge integration, which effectively extracts relevant information from the retrieved knowledge along the channel dimension. Extensive experiments demonstrate the effectiveness of our model, showing significant improvement across various domains and datasets.