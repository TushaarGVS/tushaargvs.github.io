---
layout: post
title: Memory-efficient attention
tagline: (<a href="https://arxiv.org/pdf/2112.05682v3.pdf">arxiv</a>)
description: self-attention does not need O(n^2) memory
tags: [llms, transformers, memory-efficient, attention]
author: Tushaar Gangavarapu
next:
previous: 
    url: 'posts/transformers/performers.html'
    title: performers
---
{% include JB/setup %}

### Self-attention

Self-attention (<a href="https://arxiv.org/abs/1706.03762">Vaswani et al., 2017</a>) is at the core of several large language models. For an input sequence of $$L$$ tokens, each represented as $$d$$-dimensional (a.k.a., hidden dimension) embedding; for a given query, $$q \in \mathbb{R}^d$$, and:

$$
K = \begin{bmatrix}
\rule[.5ex]{2.5ex}{0.5pt} & k_1 & \rule[.5ex]{2.5ex}{0.5pt} \\
\rule[.5ex]{2.5ex}{0.5pt} & k_2 & \rule[.5ex]{2.5ex}{0.5pt} \\
& \vdots & \\
\rule[.5ex]{2.5ex}{0.5pt} & k_L & \rule[.5ex]{2.5ex}{0.5pt} \\
\end{bmatrix}, V = \begin{bmatrix}
\rule[.5ex]{2.5ex}{0.5pt} & v_1 & \rule[.5ex]{2.5ex}{0.5pt} \\
\rule[.5ex]{2.5ex}{0.5pt} & v_2 & \rule[.5ex]{2.5ex}{0.5pt} \\
& \vdots & \\
\rule[.5ex]{2.5ex}{0.5pt} & v_L & \rule[.5ex]{2.5ex}{0.5pt} \\
\end{bmatrix}
$$

{% tabs attn %}
{% tab attn pytorch %}
```python
import torch

def attention(q, k, v):
    pass
```
{% endtab %}

{% tab attn jax %}
```python
import jax
from jax import numpy as jnp

def attention(q, k, v):
    pass
```
{% endtab %}
{% endtabs %}

### Memory-efficient attention

#### Softmax trick

### References
