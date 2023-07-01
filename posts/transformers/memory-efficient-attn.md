---
layout: post
title: <a href="https://arxiv.org/pdf/2112.05682v3.pdf">Memory-efficient attention</a>
description: self-attention does not need $\mathcal{O}(n^2)$ memory
author: Tushaar Gangavarapu
categories: [nlp, llms]
tags: [transformers, memory-efficient, attention]
date: 2023-06-30
next:
previous: 
    url: 'posts/transformers/performers.html'
    title: performers
---
{% include JB/setup %}

### Self-attention

```r
library(ggplot2)

# Use stdout as per normal...
print("Hello, world!")

# Use plots...
plot(cars)

# Even ggplot!
qplot(wt, mpg, data = mtcars, colour = factor(cyl))
```

{% highlight rurby %}
library(ggplot2)

# Use stdout as per normal...
print("Hello, world!")

# Use plots...
plot(cars)

# Even ggplot!
qplot(wt, mpg, data = mtcars, colour = factor(cyl))
{% endhighlight %}

### Memory-efficient attention

#### Softmax trick

### References
