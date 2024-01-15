---
layout: post
title: "Hello, CUDA: Writing CUDA extensions for PyTorch"
tagline: 
description: "Writing CUDA extensions for PyTorch"
tags: [ CUDA, PyTorch, parallel computing ]
date: 2024-01-15
author: Tushaar Gangavarapu
toc: false
next:
previous: 
---

(This blog is inspired from Shijie Wang's post "[Beyond Native PyTorch: The Power of C++/CUDA Integration](https://witnessj.com/archives/cuda)" and several other PyTorch CUDA/CPP extension tutorials online.)

Okay, so a natural question is: why would one need to learn how to write CPP/CUDA extensions for PyTorch? It's simple: performance optimization. But wait!, isn't PyTorch already optimized?---not in all cases! For example, you might want to enable fast matrix multiplication with _sparse_ matrices (which was my motivation!), or you want to employ fused kernel operations. CUDA/CPP extensions can offer high performance (compared to naive PyTorch-only implementations).

---

## Preliminaries

__Memory.__ Memory is hierarchical in nature, and the general rule is that faster the memory, the more expensive it is, and smaller its capacity. As a reference: an A$100$ GPU has a CPU DRAM (main memory) of over one TB and offers a bandwidth of $12.8$GB/sec, $40$-$80$GB of high-bandwidth memory (HBM) with a bandwidth of $1.5$-$2.5$TB/sec, and $192$KB of on-chip SRAM per multiprocessor (total: $108$) with an estimated bandwidth of $19$TB/sec.
