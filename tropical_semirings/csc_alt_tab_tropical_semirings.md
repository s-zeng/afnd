---
title: Tropical Semirings
subtitle: A general method for declaratively solving graph problems
author: Simon Zeng
date: \today
theme: Frankfurt
titlegraphic: title_image.png
slide-level: 2
section-titles: false
institute: UWCSC
logo: csc.png
---

## Handout

- You may obtain a copy of these notes and code samples on my website
- Code samples are in Haskell and were tested on GHC 9.2.4

### Links

- [https://simonzeng.com/tropical.pdf](https://simonzeng.com/tropical.pdf)
- [https://simonzeng.com/tropical.hs](https://simonzeng.com/tropical.hs)

::: notes

- Greeting
- Functional programming talk
  - Not lambda
  - Not purity
  - Not monads
- Solving real problems declaratively
  - Graph problems!
- We develop an algebraic method that elegantly describes a class of graph 
  problems and their solutions
- These notes are available on my website

:::

# The essence of the path algorithm

## Dijkstra's Shortest Path Algorithm

- Q: How do we traditionally get the shortest path between two nodes on a graph? \pause
- A: *Dijkstra's algorithm*

::: {.block}
### Pseudocode

\tiny
```algol
01 function Dijkstra(Graph, source):
02     dist[source] <- 0
03     create vertex priority queue Q
04     for each vertex v in Graph.Vertices:
05         if v != source
06             (dist[v], prev[v]) <- INFINITY, UNDEFINED
07         Q.add_with_priority(v, dist[v])
08     while Q is not empty:
09         u <- Q.extract_min()
10         for each neighbor v of u:
11             alt <- dist[u] + Graph.Edges(u, v)
12             if alt < dist[v]:
13                 (dist[v], prev[v]) <- alt, u
14                 Q.decrease_priority(v, alt)
15     return dist, prev
```
\normalsize
:::
\pause
- Very classic, but:
  - Uses lots of state and mutation
  - Hard to tell what's going on from just reading the code

::: notes

- Q: read
- (next, then read)
- Everyone love's Dijkstra's
- Set up priority queue, put things into it, take things out of it, stop 
  iterating based on it
- (next, then read)
- It's a very imperative algorithm
- CS 341 shows a few other graph path algorithms
  - from that you'd think they're all inherently imperative
- But: graph problems are **not** inherently imperative!
- Let's zoom in to the meat

:::

## Core of Dijkstra's Algorithm

- When going from some node $u$ to some node $v$: \pause
  - Get the best distance from source to $u$... \pause
  - ...**add** the weight of the edge $uv$... \pause
  - ...compare against existing best distance of $v$... \pause
  - ... store the **minimum** between our number and what $v$ already has \pause

::: {.block}
### Pseudocode

\tiny
```algol
11 alt <- dist[u] + Graph.Edges(u, v)
12 if alt < dist[v]:
13    dist[v] <- alt
```
\normalsize
:::

\pause
- The rest of Dijkstra's tells us only **when** we look at a particular 
  node \pause
- Dijkstra's is just node ordering boilerplate around this core operation

## A Functional Kernel

- The original calculates, then compares, then (sometimes) sets

::: {.block}
### Original Pseudocode
\tiny
```algol
11 alt <- dist[u] + Graph.Edges(u, v)
12 if alt < dist[v]:
13    dist[v] <- alt
```
\normalsize
:::

- The comparison+set can be written as a single function call

::: {.block2}
### Refined pseudocode

\tiny
```algol
dist[v] <- min(dist[v], dist[u] + Graph.Edges(u, v))
```
\normalsize
:::

- This is the core of path algorithms!
- Remember this for later

