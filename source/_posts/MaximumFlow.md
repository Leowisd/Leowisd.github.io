---
title: Maximum Flow
tags: [Maximum Flow, Graph Algorithms, Ford-Fulkerson, Edmonds-Karp algorithm, Maximum bipartite matching, Push-relabel algorithms]
mathjax: true
date: 2018-11-11 20:56:38
categories: Algorithms
description: Review of Graph Algorithms
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fx54cm6f9vj209b04374c.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Ford-Fulkerson method

![](http://ww1.sinaimg.cn/large/cf684029ly1fx53n0bi5ej20e70483yr.jpg)

### Residual networks

Intuitively, given a flow network $G$ and a flow $f$ , the residual network $G_f$ consists
of edges with capacities that represent how we can change the flow on edges of G.

![](http://ww1.sinaimg.cn/large/cf684029ly1fx53u7mkpfj208j023glh.jpg)

### Augmenting paths

Given a flow network $G=(V,E)$ and a flow $f$ , an **augmenting path** p is a
simple path from s to t in the residual network $G_f$.

### Cuts of flow networks

A cut $(S,T)$ of flow network $G=(V,E)$ is a partition of $V$ into $S$ and
$T = V - S$ such that $s \in S$ and $t \in T$ .

![](http://ww1.sinaimg.cn/large/cf684029ly1fx53tgp99pj205s021glh.jpg)

### basic Ford-Fulkerson algorithm

![](http://ww1.sinaimg.cn/large/cf684029ly1fx53v378o5j20c004z74k.jpg)

### The Edmonds-Karp algorithm

We can improve the bound on **FORD-FULKERSON** by finding the augmenting
path p in line 3 with a breadth-first search. That is, we choose the augmenting
path as a shortest path from s to t in the residual network, where each edge has
unit distance (weight).

Running Time: $O(VE^2)$

## Maximum bipartite matching

Thus, given a bipartite undirected graph $G$, we can find a maximum matching by
creating the flow network $G'$, running the Ford-Fulkerson method, and directly obtaining
a maximum matching $M$ from the integer-valued maximum flow $f$ found. Since anymatching in a bipartite graph has cardinality at most $min(L,R) = O(V)$, the value of the maximum flow in $G'$ is $O(V)$. We can therefore find a maximum matching in a bipartite graph in time $O(VE') = O(VE)$

## Push-relabel algorithms

### The push operation

![](http://ww1.sinaimg.cn/large/cf684029ly1fx540vvnalj20di04xglz.jpg)

### The relabel operation

![](http://ww1.sinaimg.cn/large/cf684029ly1fx541m4ezmj20dt02taa6.jpg)

### The generic algorithm

![](http://ww1.sinaimg.cn/large/cf684029ly1fx54248mjuj206906474g.jpg)

![](http://ww1.sinaimg.cn/large/cf684029ly1fx5431wn83j20by02awei.jpg)

## The relabel-to-front algorithm

### Discharging an overflowing vertex

![](http://ww1.sinaimg.cn/large/cf684029ly1fx544unfqfj209504t74f.jpg)

### The relabel-to-front algorithm

![](http://ww1.sinaimg.cn/large/cf684029ly1fx545m18jcj207i06c0t1.jpg)

<hr />