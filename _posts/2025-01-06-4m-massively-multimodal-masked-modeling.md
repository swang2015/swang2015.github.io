---
layout: post
title:  "4M: Massively Multimodal Masked Modeling"
date:   2025-01-06 04:30:00 0000
link: https://4m.epfl.ch
categories: CV
tags: 3d-modelling codebase pretrained-models
---

Current machine learning models for vision are often highly specialized and limited to a single modality and task. In contrast, recent large language models exhibit a wide range of capabilities, hinting at a possibility for similarly versatile models in computer vision.

We take a step in this direction and propose a multimodal training scheme called 4M, short for Massively Multimodal Masked Modeling. It consists of training a single unified Transformer encoder-decoder using a masked modeling objective across a wide range of input/output modalities — including text, images, geometric, and semantic modalities, as well as neural network feature maps. 4M achieves scalability by unifying the representation space of all modalities through mapping them into discrete tokens and performing multimodal masked modeling on a small randomized subset of tokens.

4M leads to models that exhibit several key capabilities:
1. they can perform a diverse set of vision tasks out of the box,
2. they excel when fine-tuned for unseen downstream tasks or new input modalities, and
3. they can function as a generative model that can be conditioned on arbitrary modalities, enabling a wide variety of expressive multimodal editing capabilities with remarkable flexibility.

Through experimental analyses, we demonstrate the potential of 4M for training versatile and scalable foundation models for vision tasks, setting the stage for further exploration in multimodal learning for vision and other domains. Please see our [GitHub repository](https://github.com/apple/ml-4m/) for code and pre-trained models.