---
layout: post
title: Linear algebra refresher
tagline: (<a href="https://www.cs.cornell.edu/courses/cs6210/2023fa">CS6210</a>)
tags: [ vector spaces, matrices, norms, real and complex spaces, linear algebra ]
date: 2023-08-21
author: Tushaar Gangavarapu (the contents of this blog are adopted from CS6210 lecture notes)
toc: false
next:
previous: 
---

This and the following posts are about, well, "using matrices"; more specifically, 1) (*stable* and efficient 
algorithms for) linear systems, 2) least squares, 3) eigenvalue problems. We will attempt to solve these problems 
using direct (factorization) methods and iterative methods.

## Preliminaries