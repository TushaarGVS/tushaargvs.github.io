---
layout: post
title: <a href="https://arxiv.org/pdf/2112.05682v3.pdf">memory-efficient attention</a>
description: self-attention does not need O(n^2) memory
categories: 
    nlp
    llms
tags: 
    attention
    memory
    efficiency
output:
  html_document:
    highlight: pygments
  pdf_document: default
  word_document: default
---
{% include JB/setup %}

{% highlight python %
import numpy as np
import jax as jax
{% endhighlight %}}