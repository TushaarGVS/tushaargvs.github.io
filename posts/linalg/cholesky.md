---
layout: post
title: Cholesky factorization
tagline: 
description: Cholesky factorization (for SPD matrices)
tags: [cholesky, SPD, matrix factorization]
date: 2024-10-10
author: Tushaar Gangavarapu
next: 
previous: householder_qr
toc: true
---

{:toc}

In this post, we will focus on solving a system of linear equations, $Ax = b,$ with
$A \in \mathbb{C}^{n \times n}$—we will view this for the case of $A$ being symmetric,
Hermitian (or symmetric) positive-definite.

<u><i>Hermitian positive definite (HPD) matrix</i></u>. $A \in \mathbb{C}^{n \times n}$
is HPD if $A = A^H$ and all $x > 0,$ the quadratic form, $x^H A x > 0.$ Note that this
is equivalent to having all positive eigenvalues.

---

#### Cholesky theorem

If $A$ is HPD ($A^H = A$ and )