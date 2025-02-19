---
layout: post
title:  "Controllable Human-Object Interaction Synthesis"
date:   2025-01-06 11:20:00 0000
link: https://github.com/lijiaman/chois_release
categories: Omniverse
tags: physical-ai codebase
---

Synthesizing semantic-aware, long-horizon, human-object interaction is critical to simulate realistic human behaviors. In this work, we address the challenging problem of generating synchronized object motion and human motion guided by language descriptions in 3D scenes.

We propose Controllable Human-Object Interaction Synthesis (CHOIS), an approach that generates object motion and human motion simultaneously using a conditional diffusion model given a language description, initial object and human states, and sparse object waypoints. While language descriptions inform style and intent, waypoints ground the motion in the scene and can be effectively extracted using high-level planning methods.

Naively applying a diffusion model fails to predict object motion aligned with the input waypoints and cannot ensure the realism of interactions that require precise hand-object contact and appropriate contact grounded by the floor. To overcome these problems, we introduce an object geometry loss as additional supervision to improve the matching between generated object motion and input object waypoints. In addition, we design guidance terms to enforce contact constraints during the sampling process of the trained diffusion model.