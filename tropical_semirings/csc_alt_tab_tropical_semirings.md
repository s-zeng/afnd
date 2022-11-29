---
title: Tropical Semirings
subtitle: A general method for declaratively solving graph problems
author: Simon Zeng
date: \today
theme: Frankfurt
titlegraphic: title_image.png
section-titles: false
slide-level: 2
institute: UWCSC
logo: csc.png
aspectratio: 54
---

## Handout

- You may obtain a copy of these notes and code samples on my website
- Code samples are in Haskell and were tested on GHC 9.2.4

### Links

- [https://simonzeng.com/tropical.pdf](https://simonzeng.com/tropical.pdf)
- [https://simonzeng.com/tropical.hs](https://simonzeng.com/tropical.hs)

::: notes

- Greeting
- Spoiler: Functional programming talk
  - Not lambda
  - Not purity
  - Not monads
- Solving real problems declaratively
  - Graph problems!
- We develop an algebraic method that elegantly describes a class of graph 
  problems and their solutions
- These notes are available on my website

:::

# Motivating problem

![Graph where edge weights represent **number of paths**](graph.dot.svg){height=50%}

- Problem: find the number of paths between two nodes on a graph that traverses 
  $n$ edges?
- Example: there are 3 paths from 0 to 2 that traverse 1 edge

## Solving imperatively

![The graph](graph.dot.svg){height=50%}

- DFS, priority queue, etc
- Works, but a bit painful

::: notes

- Informally go over an imperative DFS
- Do example with $n = 3$

:::

# Towards an elegant solution

![The graph](graph.dot.svg){height=50%}

- Example: What exactly are we doing when we want to solve for paths between 0 
  and 5 with $n=2$?
- $Paths(0, 5) = 3\cdot 1 + 5\cdot 0 + 2\cdot 1 + 4\cdot 2 = 13$

::: notes

- What does this look like? A linear combination!
- It's actually a dot product!

:::

## What does that look like?

![The graph](graph.dot.svg){height=50%}

### Solution for $n=4$ as a dot product

$$Paths(0, 5) =(3, 5, 2, 4)\cdot (1, 0, 1, 2) = 13$$

::: notes

- Explain where the numbers come from

:::

## Expanding it out

![The graph](graph.dot.svg){height=50%}

- Actually, there are 0 paths of length 1 between two unconnected nodes, so the 
  full dot product looks like:
$$Paths(0, 5) = (0, 3, 5, 2, 4, 0, 0)\cdot (0, 1, 0, 1, 2, 0, 5) = 13$$

::: notes

- Explain where the numbers come from again, but with the 0s

:::

## The solution for $n=2$ is a dot product

::: {.block}
### Our previous exmple

$$Paths(0, 5) = (0, 3, 5, 2, 4, 0, 0)\cdot (0, 1, 0, 1, 2, 0, 5) = 13$$
:::

- If the nodes are labelled $u, v, a, b, c, \cdots$ and edges between nodes $u$ 
  and $v$ are labelled $e_{uv}$, then we have:

$$Paths(u, v) = (e_{ua}, e_{ub}, e_{uc}, \cdots)\cdot (e_{av}, e_{bv}, e_{cv}, 
\cdots,)$$

- The first vector is all the edges that start at $u$
- The second vector is the edges that end at $v$

::: notes

So if the answer is just dot products, what if we want to calculate the number 
of paths between two nodes for the entire graph at once?

A bunch of dot products??? What's that called?

It's a matrix product!
:::

## A global answer

![The graph](graph.dot.svg){height=25%}

- Consider the adjacency matrix of the graph:
$$\begin{bmatrix}
  0 & 3 & 5 & 2 & 4 & 0 & 0 \\
  3 & 0 & 0 & 0 & 0 & 1 & 4 \\
  5 & 0 & 0 & 0 & 0 & 0 & 0 \\
  2 & 0 & 0 & 0 & 0 & 1 & 0 \\
  4 & 0 & 0 & 0 & 0 & 2 & 0 \\
  0 & 1 & 0 & 1 & 2 & 0 & 5 \\
  0 & 4 & 0 & 0 & 0 & 5 & 0 \\
\end{bmatrix}
$$
- Do you spot the $Path(0, 5)$ dot product?



# A different problem?

swapping semiring to shortest distance

# Get Closure

introduce calculation of 1 + a + a^2 + a^3 + ...

# Choose your character

- longest path
- widest flow
- dfa->regex
- inverting matrices
- determine graph is bipartite
- reconstructing path
