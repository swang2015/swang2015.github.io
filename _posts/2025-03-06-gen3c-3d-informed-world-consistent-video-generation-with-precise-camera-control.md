---
layout: post
title:  "GEN3C: 3D-Informed World-Consistent Video Generation with Precise Camera Control"
date:   2025-03-06 17:10:00 0000
link: https://research.nvidia.com/labs/toronto-ai/GEN3C/
categories: AGI
tags: genai codebase tbc
---

Abstract: We present GEN3C, a generative video model with precise Camera Control and temporal 3D Consistency. We achieve this with a 3D cache: point clouds obtained by predicting the pixel-wise depth of seed images or previously generated frames. When generating the next frames, GEN3C is conditioned on the 2D renderings of the 3D cache with the new camera trajectory provided by the user. Our results demonstrate more precise camera control than prior work, as well as state-of-the-art results in sparse-view novel view synthesis, even in challenging settings such as driving scenes and monocular dynamic video.