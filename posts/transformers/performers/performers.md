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

### (Self-)attention

Transformers (<a href="https://arxiv.org/abs/1706.03762">Vaswani et al., 2017</a>; <a href="https://arxiv.org/abs/1810.04805">Devlin et al., 2019</a>) have become SOTA in several machine learning tasks, including language processing, machine translation, generative modeling, etc. (Self-)attention  is at the core of these transformer models. The attention mechanism describes a weighted average of elements, weighted dynamically by some function, $$f_\text{attn}$$ (usually, dot-product similarity, small multi-layer perceptron, etc.), of input query and elements' keys. In simpler terms, for a given query, we hope to determine which inputs to dynamically "attend" to.

* **query**: the feature vector of what we are looking for in the given sequence
* **key**: the feature vector of what a specific element is offering (can be thought of as the webpage titles in an information retrieval system)
* **value**: the feature vector of a specifc element (can be thought of as the webpage content in an information retrieval system)

Consider an input sequence of $$L$$ tokens, the "regular" dot-product attention is a mapping that accepts three matrices: $$Q, K, V \in \mathbb{R}^{L \times d}$$ ($$d$$ = embedding/hidden dimension); $$Q, K, V$$ are intermediate representations and the rows represent queries, keys, and values (= $$d$$-dimensional row vectors) respectively. Bidirectional[^1] or non-directional (<a href="https://arxiv.org/abs/1810.04805">Devlin et al., 2019</a>) attention can be computed as:

$$
\text{attn}_\leftrightarrow(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d}}\right)V
$$

The above can also be formulated as follows: for a given query $$q \in \mathbb{R}^{1\times d}$$, and lists of keys: $$\{k_{1,:}, \dotsc, k_{L,:}\}$$ and values: $$V = \{v_{1,:}, \dotsc, v_{L,:}\}$$, we have attention as:

$$
s_i = \frac{q k_{i,:}^{T}}{\sqrt{d}}, \quad s'_i = \underbrace{\frac{\exp(s_i)}{\sum_j\exp(s_j)}}_{\text{softmax}}, \quad \text{attn}_\leftrightarrow(q, K, V) = \sum_i s'_i v_{i,:}
$$

Note that in the above formulations, $$f_\text{attn}$$ is essentially the dot-product similarity (note $$QK^T$$ is essentially a dot-product between each query (row) and each key (column)). One final thing to note here is the scaling factor of $$1/\sqrt{d}$$. 

The implementation of the above is as follows:

{% tabs attn %}
{% tab attn pytorch %}

```python
import math

import torch
import torch.nn as nn
import torch.nn.functional as F

class SelfAttention(nn.Module):
	def __init__():
		super().__init__()
		
	def forward(self, Q, K, V):
		# Q, K, V: (batch_size, L, d)
		# attn_probs: (batch_size, L, L)
	    attn_probs = F.softmax(torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d), dim=-1)
	    return torch.matmul(attn_probs, V)

if __name__ == "__main__":
	self_attn = SelfAttention()
	L, d = 1024, 300
	Q, K, V = torch.randn((L, d)), torch.randn((L, d)), torch.randn((L, d))
	attn_out = self_attn(Q, K, V)
	
	print(attn_out)
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

Note that a straight-forward implementation of the attention mechanism (presented in the previous section) for a single query takes $$\mathcal{O}(d)$$ time to compute $$s_i$$, $$\mathcal{O}(Ld)$$ for all keys (= total $$L$$ keys). Note that we need to compute and store $$L$$ $$s'_i$$s per query, leading to $$\mathcal{O}(L)$$ space complexity. Hence, for $$L$$ queries, we have $$\mathcal{O}(L^2d)$$ time and $$\mathcal{O}(L^2)$$ space complexity. (Strictly speaking, we need $$\mathcal{O}(Ld)$$ to store $$Q, K, V$$ matrices, meaning that the space complexity is $$\mathcal{O}(L^2 + Ld)$$ to be exact.)

From the above, it is evident that attention scales quadratically in sequence length, which can become a significant computational bottleneck (several applications require sequence lengths of $$4,096$$ or higher; e.g., modeling conversational data, nursing notes, etc.).

#### Softmax trick

### References

[^1]: The focus of this post is to introduce memory-efficient attention, and to this end, bidirectional attention is used as a standing proxy for attention; the ideas introduced are transferable to unidirectional attention [= attention employed for autoregressive tasks].
