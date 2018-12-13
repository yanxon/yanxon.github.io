---
layout: page
title: "Week 1: Overview and Introduction"
---

There are a few fundamental matrix computations that show up frequently,
in many different disciplines. Although there are other interesting 
computational linear algebra problems, we focus our attention on these three:

## The Fundamental Types of Matrix Computations

- Linear Systems of Equations

$$
A x = b, \qquad A \in \mathbb{R}^{n \times n}
$$

- The Eigenvalue Problem 

$$
A x = \lambda x, \qquad A \in \mathbb{R}^{n \times n}
$$

- Model Order Reduction of Dynamical Systems

$$
\begin{gathered}
E \frac{d}{dt} x(t) = A x(t) + B u(t), 
\qquad A, E \in \mathbb{R}^{n \times n},
\; B \in \mathbb{R}^{n \times m} \\ \\
\text{given} \;\; x(t_0) = x_0, \;\; y(t) = C^{\top} x(t) \\ \\
\text{for} \; m \ll n
\end{gathered}
$$

## What exactly does "Large Scale" mean?

"Large" doesn't correspond to a particular problem size,
because that value would change over time, as computing
resources become more efficient.

Instead, we define "Large" to mean that the problem size 
is big enough that these operations take a significant 
amount of time/memory to complete, and that any practical
implementation must take advantage of special structures
of the underlying matrices to obtain a solution.

Most of the time, the matrices that are involved in these
kinds of computations for realistic problems (e.g. 
discretization of differential equations, network problems,
web search) do exhibit some kind of special structures,
sparsity being the most common.

> A matrix is said to be **sparse** if most of its entries
> are zero. Sparse matrices are stored in such a way as to only
> keep track of the nonzero values. In contrast, if a matrix
> stores all of its entries, zero and nonzero, it is said to be
> **dense**.

## Terminology: the Graph of a (sparse) matrix

Let $$A = [a_{jk}] \in \mathbb{R}^{n \times n}$$. We associate with A
a directed graph $$G(A)$$ with:

- nodes: $$N = \bigg\{ 1, 2, ... \;, n \bigg\} $$
- edges: $$E = \bigg\{ (j,k) \mid j,k \in N \; \text{and} \; a_{jk} \neq 0 \bigg\} $$

Consider the following sparse matrix (nonzero values indicated with $$*$$):

$$
A = 
\begin{bmatrix}
0 & * & 0 & * & * & 0 \\
* & 0 & * & 0 & * & 0 \\
0 & 0 & * & 0 & 0 & * \\
0 & 0 & 0 & * & 0 & 0 \\
0 & 0 & 0 & * & 0 & * \\
0 & 0 & * & 0 & * & 0
\end{bmatrix}
$$

This matrix has a graph $$G(A)$$ given by

$$ N = \big\{ 1, 2, 3, 4, 5, 6 \big\} $$
$$ E = \big\{ 
(1,2), (1,4), (1,5), (2,1), (2,3), (2,5), (3,3),
(3,6), (4,4), (5,4), (5,6), (6,3), (6,5) \big\} 
$$

and it can be plotted:

![](/images/math/sparse_graph.svg)


### Example: Sparse Matrix used in Page Ranking

Consider the following model of the internet as a graph, $$G_I$$ with

- nodes: $$ N = \big\{ 1, 2, … , n \big\}, \; n = \text{number of visible web pages} $$
- edges: $$ E = \big\{ (j,k) \mid j,k \in N, \; j \neq k, \; 
                \text{ and page } j \text{ links to page } k \big\} $$

Although $$n$$ for this problem is enormous, the average number of links on any page is small. As
a result, a matrix with graph $$G_I$$ is very sparse.

Let $$ Q = \big[ q_{jk} \big] \in \mathbb{R}^{n \times n} $$ be a one such matrix satisfying $$G(Q) = G_I$$

with $$ q_{jk} = 
\begin{cases} 
\frac{1}{d_j} \qquad \text{if } (j,k) \in E \\
0 \qquad \text{otherwise}
\end{cases} $$

where $$ d_j $$ is the _out degree_ of page $$j$$, the number of links
from $$j$$ to other sites. 

Then, let $$A = \big[ a_{jk} \big] \in \mathbb{R}^{n \times n}$$,
  where $$ a_{jk} = 
\begin{cases} 
q_{jk} \qquad \text{if } d_j > 0 \\
\frac{1}{n} \qquad \text{if } d_j = 0
\end{cases} $$

$$A$$ can also be written as $$ A = Q + \frac{1}{n} v e^{\top} $$, where 
$$v_i \begin{cases} 1 \text{ if } d_i = 0 \\ 0 \text{ if } d_i > 0 \end{cases}$$, and
$$e_i = 1$$

By construction, $$A$$ is _row stochastic_, meaning the entries in each row are non-negative and
sum to 1. As a consequence, we observe that $$A e = e$$, or that $$e$$ is an eigenvector of $$A$$
with eigenvalue 1.
