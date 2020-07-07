---
title: All Pairs Shortest Paths
tags: [Shortest Paths, Floyd-Warshall, Johnson's algorithm, Graph Algorithms]
mathjax: true
date: 2018-11-11 10:00:28
categories: Algorithms
description: Review of Graph Algorithms
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fx54bryekmj206v050jrb.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Shortest paths and matrix multiplication

### A recursive solution to the all-pairs shortest-paths problem

Now, let $l_{ij}^{(m)}$ be the minimum weight of any path from vertex i to vertex j that contains at most m edges. When $m=0$, there is a shortest path from i to j with no edges if and only if $i=j$. Thus,

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4lh0e4ocj204u01wmwy.jpg)

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4lhtph6hj208601zglh.jpg)

The actual shortest-path weights are given by

$\delta(i,j) = l^{(n-1)}_{ij} = l^{(n)}_{ij} = l^{(n+1)}_{ij} = ...$

Because there is a shortest path from i to j that is simple and thus contains at most n-1 edges.

### Computing the shortest-path weights bottom up

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4lnitfl3j207h04x74d.jpg)

Which extends the shortest paths computed so far by one more edge.

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4lrf7nsjj20a403uglp.jpg)

Running time: $\Theta(n^4)$

### Improving the running time

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4luckazcj20ah04w74f.jpg)

Running time: $\Theta(n^3 lgn)$

## The Floyd-Warshall algorithm

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4m4r802uj209m04zjri.jpg)

Running time: $\Theta(n^3)$

### Transitive closure of a directed graph

We define the transitive closure of G as the graph $G^*=(V, E^*)$, where $E^* = (i,j):$ there is a path from vertex i to vertex j in G. 

One way to compute the transitive closure of a graph in $\Theta(n^3)$ time is to assign a weight of 1 to each edge of E and run the Floyd-Warshall algorithm. If there is a path from vertex i to vertex j, we get $d_(ij) < n$. Otherwise, we get $d_(ij) =1$.

## Johnson’s algorithm for sparse graphs

Johnson’s algorithm finds shortest paths between all pairs in $O(V^2lgV+VE)$ time.

![](http://ww1.sinaimg.cn/large/cf684029ly1fx4n7wb4v1j20cu091gmj.jpg)

<hr />