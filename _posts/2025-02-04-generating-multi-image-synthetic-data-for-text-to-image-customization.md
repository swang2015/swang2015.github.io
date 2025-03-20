---
layout: post
title:  "Generating Multi-Image Synthetic Data for Text-to-Image Customization"
date:   2025-02-04 20:05:00 0000
link: https://github.com/nupurkmr9/syncd
categories: AGI
tags: codebase dataset genai
---

Abstract: Customization of text-to-image models enables users to insert custom concepts and generate the concepts in unseen settings. Existing methods either rely on costly test-time optimization or train encoders on single-image training datasets without multi-image supervision, leading to worse image quality. We propose a simple approach that addresses both limitations. We first leverage existing text-to-image models and 3D datasets to create a high-quality synthetic training dataset, SynCD, consisting of multiple images of the same object in different lighting, backgrounds, and poses. We then propose a new encoder architecture based on shared attention mechanisms that better incorporate fine-grained visual details from input images. Finally, we propose a new inference technique that mitigates overexposure issues during inference by normalizing the text and image guidance vectors. Through extensive experiments we show that our final model trained on the synthetic dataset and combined with the proposed inference algorithm outperforms existing tuning-free methods on standard customization benchmarks.