---
layout: post
title: How to initialize neural networks?
tagline: (<a href="https://arxiv.org/pdf/2112.05682v3.pdf">arxiv</a>)
description: how to initialize neuural networks
tags: [nn-init, xavier, he, kaiming]
date: 2023-07-14
author: Tushaar Gangavarapu
next:
previous: 
    url: ''
    title:
---

{:toc}

One of the main reasons for the success of *deep* neural networks relies on the underlying initialization strategies. In this post, we'll mostly focus on the Xavier initialization ([Xavier and Bengio, 2010](http://proceedings.mlr.press/v9/glorot10a.html)) and its adaptation, the He or Kaiming initialization ([Kaiming et al., 2015](https://arxiv.org/abs/1502.01852)).

So why is initialization so important? If the weights are updated anyways, with any (random) initialization, wouldn't we eventually end up at the optimal weights? To motivate the problem of neural network initialization, consider a simple case of two ReLU-activated-neuron neural network and a sigmoid output (assume zero biases).

#### constant initialization

In the above toy network, we have weights $$W_{11}, W_{12}, W_{21}, W_{22}$$, where $$W_{ij}$$ denotes the weight on the edge from neuron $$i$$ to $$j$$. Let's initialize all the weights to some constant $$\kappa$$, i.e., $$W_{11} = W_{12} = W_{21} = W_{22} = \kappa$$; notice that the output from the two neurons are as follows:

$$
\begin{align*}
o_1 &= \text{relu}(W_{11} x_1 + W_{21} x_2) = \text{relu}(\kappa (x_1 + x_2)) \\
o_2 &= \text{relu}(W_{12} x_1 + W_{22} x_2) = \text{relu}(\kappa (x_1 + x_2))
\end{align*}
$$

Observe that the outputs $$o_1$$ and $$o_2$$ from both the neurons are exactly the same. The compute graph is as follows:

```
```

Let's build this simple network and inspect the gradients and the resultant weight updates.

{% tabs code1 %}
{% tab code1 pytorch %}

```python
```

{% endtab %}
{% tab code1 jax %}

```python
```

{% endtab %}
{% endtabs %}

