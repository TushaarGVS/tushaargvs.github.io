---
layout: post
title: Householder QR
tagline: 
description: QR factorization using Householder reflectors
tags: [householder reflectors, QR, matrix factorization]
date: 2024-09-19
author: Tushaar Gangavarapu
next:
previous: 
toc: true
---

{:toc}

---

A compelling motivation: A natural decomposition for thinking about least 
squares problems ($Ax = b$) is the QR decomposition of $A$,

$$
A = QR,
$$

with $Q$ is an $m \times m$ orthogonal matrix (recall: $Q^H Q = \mathrm{I}$ for
orthogonal $Q$) and $R$ is an $m \times n$ upper triangular matrix. For 
tall-thin matrices ($m \geq n$), it is often beneficial to note the _economy_ 
(or, thin [Golub and Van Loan], or, reduced [Trefethen and Bau]) QR 
decomposition as

$$
A = QR = Q \begin{bmatrix}
R_1 \\
0
\end{bmatrix} = \begin{bmatrix} Q_1 & Q_2 \end{bmatrix} \begin{bmatrix}
R_1 \\
0
\end{bmatrix} = Q_1 R_1,
$$

where $R_1$ is an $n \times n$ upper triangular matrix and $0$ is an 
$(m - n) \times n$ zero matrix, $Q_1$ is an $m \times n$ matrix, and $Q_2$ is
$m \times (m - n)$. ($Q_1$ and $Q_2$ have orthogonal columns.)

We can find a solution, $\hat{x}$, to an overdetermined system $Ax = b$ 
($m \geq n$) using the QR decomposition as

$$
\hat{x} = R_1^{-1} (Q_1^H b).
$$

(Note: We don't need to explicitly compute $R_1^{-1}$; instead, we can use
back substitution to find $\hat{x}$.)

<br/>
#### Gram-Schmidt, a brief note

A first course in linear algebra often shows orthogonalization (converting the 
existing basis of $A$ to an orthonormal basis) using the Gram-Schmidt process.
The Gram-Schmidt process orthogonalizes by subtracting off components in the
directions of previous columns and then normalizing the remainder to unit 
length. Simply put,

$$
q_j = (\mathrm{I} - P_{j-1}) a_j,
$$

where $P_{j-1}$ is a projector on to $(q_1, \dotsc, q_{j-1})$.

A critical question to ask here is the following: what happens when $a_j$ is
large and lies really close to $P_{j-1}$—aha!—the computation of $q_j$ as shown
above is prone to catastrophic cancellation. More concretely, the computed $q_j$
might not be orthogonal to previous $q_j$s.

To overcome this issue of catastrophic cancellation, the _modified_ Gram-Schmidt
algorithm is often discussed. However, we will see a different approach of using
Householder reflectors to achieve orthogonal triangularizations.

<br/>
#### Householder reflections and QR factorization

Our goal is to convert $A$ to an upper triangular matrix through a series of 
orthogonal transformations. Here's a chalkboard animation:

$$
\begin{bmatrix} 
    \small{\times} & \small{\times} & \small{\times} \\
    \small{\times} & \small{\times} & \small{\times} \\
    \small{\times} & \small{\times} & \small{\times} \\
    \small{\times} & \small{\times} & \small{\times} \\
    \vdots & \vdots & \vdots \\
    \small{\times} & \small{\times} & \small{\times} \\
\end{bmatrix} \xrightarrow{\color{green}{Q_1}} \begin{bmatrix} 
    \color{green}{*} & \small{\times} & \small{\times} \\
    \color{green}{0} & \small{\times} & \small{\times} \\
    \color{green}{0} & \small{\times} & \small{\times} \\
    \color{green}{0} & \small{\times} & \small{\times} \\
    \vdots & \color{green}{\vdots} & \vdots \\
    \color{green}{0} & \small{\times} & \small{\times} \\
\end{bmatrix} \xrightarrow{\color{blue}{Q_2}} \begin{bmatrix} 
    * & \color{blue}{\star} & \small{\times} \\
    0 & \color{blue}{\star} & \small{\times} \\
    0 & \color{blue}{0} & \small{\times} \\
    0 & \color{blue}{0} & \small{\times} \\
    \vdots & \color{blue}{\vdots} & \vdots \\
    0 & \color{blue}{0} & \small{\times} \\
\end{bmatrix} \xrightarrow{\color{red}{Q_3}} \begin{bmatrix} 
    * & \star & \color{red}{\bullet} \\
    0 & \star & \color{red}{\bullet} \\
    0 & 0 & \color{red}{\bullet} \\
    0 & 0 & \color{red}{0} \\
    \vdots & \color{red}{\vdots} & \vdots \\
    0 & 0 & \color{red}{0} \\
\end{bmatrix}
$$
