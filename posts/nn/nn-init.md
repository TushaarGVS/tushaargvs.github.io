---
layout: post
title: How to initialize neural networks?
tagline: (<a href="https://arxiv.org/pdf/2112.05682v3.pdf">arxiv</a>)
description: how to initialize neuural networks
tags: [nn-init, xavier, he, kaiming]
date: 2023-07-02
author: Tushaar Gangavarapu
next:
previous: 
    url: ''
    title:
---

One of the main reasons behind the success of large, deep neural networks relies on the underlying initialization strategies (without which, we would easily run into vanishing and/or exploding gradients). In this post, I'll mostly be referring to the Xavier initialization (<a href="http://proceedings.mlr.press/v9/glorot10a.html">Xavier and Bengio, 2010</a>) and its adaptation (<a href="https://arxiv.org/abs/1502.01852">Kaiming et al., 2015</a>) [= Kaiming or He initialization].

### So, why should you care about initialization?

As mentioned earlier, a bad network initialization could easily lead to exploding (going off to infinity) or vanishing (vanish to zero) gradients, since computers can't represent floating points to infinite precision,[^1] which can become a significant bottleneck in training deep neural networks (if you've worked with an 
RNN before, you understand the severity of this issue!). But even beyond numerical stability, initialization can play a significant role in the rate of convergence of the learning algorithm–<a href="https://arxiv.org/abs/1511.06422">Mishkin and Matas, 2015</a> show that arbitrary initialization can slow down or even stall the training process.

So, what considerations are important in the intialization of neural networks?: the number of inputs (often depends on the type of layer: linear layers vs. convolutional layers), number of outputs, type of non-linearity, and the type of the network. Let's look at a few (bad) initializations:  

#### `nn.init.constant_()`: constant initialization

*Note: for convenience, I will set bias to zero throughout this post; the topics discussed in this post equally apply to non-zero bias cases.*

To understand why zero initialization (or for that matter any constant initalization) is a bad idea, consider a toy network with two input units, two hidden units (not layers, but units), and a non-linearity $$f$$ applied to the hidden unit outputs. Consider that the weights on the hidden units are all initialized to some constant, $$\kappa$$; for an input, $$(x_1, x_2)$$ forwarded through the network, we have outputs, $$(o_1, o_2)$$ as:

$$
\begin{align*}
o_1 &= f(w_{11}x_1 + w_{21} x_2) = f(\kappa (x_1 + x_2)) \\
o_2 &= f(w_{12}x_1 + w_{22} x_2) = f(\kappa (x_1 + x_2))
\end{align*}
$$

Observe that both $$o_1$$ and $$o_2$$ are the same! So, the gradients, $$\partial o_1/\partial x_1 = \partial o_2/\partial x_1$$ and $$\partial o_1/\partial x_2 = \partial o_2/\partial x_2$$, and for gradient-based updates, notice that both $

#### 

To further motivate the vitality of initialization, consider a deep neural network of (just![^2]) five hidden layers (this example is inspire from the work by <a href="http://proceedings.mlr.press/v9/glorot10a.html">Xavier and Bengio, 2010</a>):

{% tabs code1 %}
{% tab code1 pytorch %}

```python
import math

import torch
import torch.nn as nn
import torch.nn.functional as F

class ToyNetwork(nn.Module):
    """toy network to simulate results in: http://proceedings.mlr.press/v9/glorot10a.html"""
    def __init__(self, input_dim=784, hidden_dim=1000, output_dim=10, num_hidden_layers=5):
        super().__init__()
        
        self.input_proj = nn.Linear(in_features=input_dim, out_features=hidden_dim)
        self.hidden_projs = nn.ModuleList([nn.Linear(in_features=hidden_dim, out_features=hidden_dim) 
                                           for _ in range(num_hidden_layers)])
        self.output_proj = nn.Linear(in_features=hidden_dim, out_features=output_dim)
        self.apply(self._init_weights)
        
    def _init_weights(self, module):
        """initialize using uniform distribution U[-1/sqrt(n), 1/sqrt(n)]"""
        if isinstance(module, nn.Linear):
            n = module.weight.shape[-1]
            module.weight.data = self.uniform(module, -1 / math.sqrt(n), 1 / math.sqrt(n))
            if module.bias is not None:
                # tip: in pytorch, an '_' after the method name indicates in-place operation.
                module.bias.data.zero_()
    
    @staticmethod
    def uniform(module, a, b):
        # module.weight.shape matrix of uniformly distributed numbers between [0.0, 1.0).
        weight = torch.rand(module.weight.shape)
        weight = (b - a) * weight  # [0.0, 1.0) to [0.0, b - a)
        weight = weight + a  # [0.0, b - a) to [a, b)
        return weight
        
    def forward(self, inputs, get_activations=False):
        outputs = self.input_proj(inputs)
        activations = []
        for hidden_proj in self.hidden_projs:
            outputs = F.tanh(hidden_proj(outputs))
            if get_activations:
                activations.append(outputs.detach().numpy())
        outputs = self.output_proj(outputs)
        return outputs, activations if get_activations else outputs
```

{% endtab %}

{% tab code1 jax %}

```python
```

{% endtab %}
{% endtabs %}

We can now plot the activations (averaged across the batch) at each layer and visualize the normed histograms:

{% tabs code2 %}
{% tab code2 pytorch %}

```python
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

colors = ["xkcd:red orange", "xkcd:electric green", "xkcd:electric blue", "xkcd:black", "xkcd:neon blue"]
plt.figure(figsize=(7, 3))

for layer_idx in range(len(activations)):
    sns.kdeplot(np.mean(activations[layer_idx], axis=0), label=f"layer-{layer_idx + 1}", 
                color=colors[layer_idx]);

plt.xlabel("tanh activation value")
plt.ylabel("density")
plt.legend()

plt.savefig("tanh-act.png", dpi=300, bbox_inches="tight")  # save the plot
```

{% endtab %}

{% tab code2 jax %}

```python
```

{% endtab %}
{% endtabs %}



[^1]: Aside: it might be an interesting exercise to pause here and think about the <a href="https://en.wikipedia.org/wiki/Machine_epsilon">numerical stability of floating-point operations</a>; as a fun exercise, try running `1 - 1e-16` vs. `1 - 1e-17`. (For more details, see <a href="https://www.cs.cornell.edu/courses/cs4220/2023sp/lec/2023-02-03.pdf">Prof. Bindel's lecture notes on numerical stability and catastrophic cancellation</a>.)
[^2]: Given the transformers era, a five-layer deep network is practically nothing!