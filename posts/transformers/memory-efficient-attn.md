---
layout: post
title: <a href="https://arxiv.org/abs/2112.05682v2">memory-efficient attention</a>
description: https://arxiv.org/abs/2112.05682v2
categories: nlp, llms
tags: attention, memory, efficiency
---

For an input sequence of length $$L$$, the regular dot-product attention is a mapping that uses $$Q, K, V \in \mathbb{R}^{L \times d}$$ ($$d$$ is the hidden dimension). For bidirectional attention, we have:

$$
\text{attn}_\leftrightarrow(Q, K, V) = D^{-1}AV \qquad A = \left(\frac{QK^T}{\sqrt{d}}\right) \qquad D = \text{diag}(Ae)
$$
