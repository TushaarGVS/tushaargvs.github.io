---
layout: post
title: Introduction to diffusion models
tagline: (<a href="https://arxiv.org/pdf/2006.11239.pdf">arxiv</a>)
description: Denoising Diffusion Probabilistic Models
tags: [ diffusion, noise, vae, gan, generative models, image generation ]
date: 2023-08-09
author: Tushaar Gangavarapu
next:
previous: 
---

Imagine we took an image and added random noise to it; if we did this repeatedly, we would eventually end up with just noise (and no recognizable features pertaining to the original image). Now, what if we had a magic function that started with the noise, gradually undid the noise, eventually regenerating the coherent image? This magic function is essentially the denoising diffusion model that removes noise incrementally.

<img src="./imgs/noising.png">

Two main differences to note between diffusion models and other popularly-used generative models such as GANs or VAEs is that: (1) diffusion models don't perform one-step denoising; they denoise incrementally (which can be effective, but not efficient time-wise), and (2) the latent representation has high dimensionality, i.e., same as the original data.

### Introduction to diffusion models

#### Foward process

The process of incrementally adding Gaussian noise at each timestep is referred to as the forward process and destroys information gradually, usually according to a non-learned, manually-defined variance schedule. More concretely, given a data point, $$x_0 \sim q(x)$$, where $$q(x)$$ is the "true" (unknown to us!) pdf of the data, the forward process of $$T$$ total timesteps is such that at each timestep $$t \in \{1, 2, \dotsc, T\}$$, we produce a noisy sample $$x_t$$ as follows:

$$q(x_t | x_{t-1}) = \mathcal{N}(x_t; \mu = x_{t-1}\sqrt{1-\beta_t}, \sigma^2 = \beta_t \mathrm{I})$$

where $$\beta_t \in (0, 1)$$ is the variance schedule, and usually $$\beta_1 < \beta_2 < \cdots < \beta_T$$ [= it's okay to take larger steps as the input gets noisier]; the variance schedule (as we will see later) can be linear, quadratic, cosine, etc. Given a well-behaved variance schedule, the forward process results in an isotropic Gaussian distribution [= variance in each dimension of the multivariate Gaussian is the same; $$\Sigma = \sigma^2\mathrm{I}$$] at $$T = \infty$$. 

Simply put, the forward process is essentially drawing (slightly noisier) samples (at each timestep) from a *conditional* Gaussian with mean $$x_{t-1}\sqrt{1-\beta_t}$$ and variance $$ \beta_t \mathrm{I}$$. For some $$\varepsilon \sim \mathcal{N}(0, 1)$$, the above can also be written as (following the properties of a standard normal distribution): 

$$x_t \sim \mathcal{N}(x_{t-1}\sqrt{1-\beta_t}, \beta_t \mathrm{I}) \equiv x_t = x_{t-1} \sqrt{1-\beta_t} + \varepsilon\sqrt{\beta_t} $$

The forward process is a simple Markov chain, where the distribution at a particular timestep only depends on the sample from the immediately preceeding timestep. Hence,

$$q(x_{1:T}|x_0) = \prod_{t=1}^T q(x_t | x_{t-1})$$

A nice property of the forward process us that any $$x_t$$ can be sampled for some arbitrary timestep $$t$$ in a closed form as follows; let $$\alpha_t = 1 - \beta_t$$, $$\bar{\alpha}_t = \prod_{s=1}^T \alpha_s$$, $$\bar{\varepsilon}_t = \prod_{s=1}^T \varepsilon_s$$:

$$
\begin{align*}
x_t = q(x_t | x_0) = \prod_{t=1}^T q(x_t | x_{t-1}) &= \prod_{t=1}^T \bbox[#90EE90]{x_{t-1}} \sqrt{\alpha_t} + \varepsilon_t\sqrt{1 - \alpha_t} \\
&= \prod_{t=2}^T \bbox[#90EE90]{\left(x_{t-2} \sqrt{\alpha_{t-1}} + \varepsilon_{t-1}\sqrt{1 - \alpha_{t-1}} \right)} \sqrt{\alpha_t} + \varepsilon_t \sqrt{1 - \alpha_t} \\
&= \prod_{t=2}^T x_{t-2} \sqrt{\alpha_t\alpha_{t-1}} + \underbrace{\varepsilon_{t-1} \sqrt{\alpha_t - \alpha_t\alpha_{t-1}}}_{\mathcal{N}(0, \alpha_t - \alpha_t\alpha_{t-1})} + \underbrace{\varepsilon_{t} \sqrt{1 - \alpha_t}}_{\mathcal{N}(0, 1 - \alpha_t)} \\
&= \prod_{t=2}^T \bbox[#F984EF]{x_{t-2}} \sqrt{\alpha_t\alpha_{t-1}} + \varepsilon \sqrt{1 - \alpha_t\alpha_{t-1}} \\
&\hphantom{=~} \vdots \\
&= x_0 \sqrt{\bar{\alpha}_t} + \varepsilon \sqrt{1 - \bar{\alpha}_t}
\end{align*} 
$$

Hence, $$q(x_t|x_0) = \mathcal{N}(x_t; x_0 \sqrt{\bar{\alpha}_t}, (1 - \bar{\alpha}_t)\mathrm{I})$$.

#### Parameterized reverse process

If we can somehow reverse the above process

#### An aside on variance scheduling

In the forward process, the final limiting distribution is essentially $$q(x_T | x_0) \sim \mathcal{N}(0, \mathrm{I})$$.