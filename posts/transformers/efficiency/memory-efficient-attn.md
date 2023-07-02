---
layout: post
title: Memory-efficient attention
tagline: (<a href="https://arxiv.org/pdf/2112.05682v3.pdf">arxiv</a>)
description: self-attention does not need O(n^2) memory
tags: [llms, transformers, memory-efficient, attention]
date: 2023-07-02
author: Tushaar Gangavarapu
next:
previous: 
    url: 'posts/transformers/efficiency/performers.html'
    title: performers
---
{% include JB/setup %}

### Self-attention

Self-attention (<a href="https://arxiv.org/abs/1706.03762">Vaswani et al., 2017</a>) is at the core of several large language models. 

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
