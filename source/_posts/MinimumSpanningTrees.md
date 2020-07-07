---
title: Minimum Spanning Trees
tags: [Graph Algorithms, Minimum Spanning Trees, Kruskal, Prim]
date: 2018-10-12 21:07:51
categories: Algorithms
description: Review of Graph Algorithms
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fw6drerq9rj212w0m8tfl.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Growing a minimum spanning tree

```
GENERIC_MST(G, w)
A = 0
while A does not form a spanning tree
    find an edge(u,v) that is safe for A
    A = A U {(u,v)}
return A
```

### Safe-Edge Theorem 

Let G = (V, E) be a connected, undirected graph with a real-valued weight function w defined on E. Let A be a subset of E that is inclueded in some minimum spanning tree for G, let (S, V-S) be any cut of G that
respects A, and let (u,v) be a light edge crossing (S, V-S). Then edge(u, v) is safe for A.   

## Kruskal
```
MST-KRUSKAL(G, w)
1   A = null
2   for each vertex v <- G.V
3       MARK-SET(v)
4   sort the edges of G.E into nondecreasing order by weight w
5   for each edge(u,v) <- G.E, taken in nondecreasing order by weight w
6       if FIND-SET(u) != FIND-SET(v)
7           A = A U {(u,v)}
8           UNION(u,v)
9   return A
```
The operation FIND-SET(u) returns a representative element from the set that contains u. Thus, we can determine whether two vertices u and v belong to the same tree by testing whether FIND-SET(u) equals FIND-SET(v). To combine trees, Kruskal’s algorithm calls the UNION procedure.

Lines 1–3 initialize the set A to the empty set and create |V| trees, one containing each vertex. The for loop in lines 5–8 examines edges in order of weight, from lowest to highest. The loop checks, for each edge (u, v), whether the endpoints u and v belong to the same tree. If they do, then the edge (u, v) cannot be added to the forest without creating a cycle, and the edge is discarded. Otherwise, the two vertices belong to different trees. In this case, line 7 adds the edge (u, v) to A, and line 8 merges the vertices in the two trees.

Running Time: O(ElgV)

## Prim
```
MST-PRIM(G, W, r)
1   for each u <- G.V
2       u.key = infinity
3       u.pre = NIL
4   r.key = 0
5   Q = G.V
6   while Q != null
7       u = EXTRACT-MIN(Q
8       for each v <- G.adj[u]
9       if v<-Q and w(u,v)<v.key
10          v.pre = u
11          v.key = w(u,v)
```
The running time of Prim’s algorithm depends on how we implement the minpriority queue Q.

If we implement Q as a binary min-heap, the total time for Prim’s algorithm is O(ElgV), which is
asymptotically the same as for our implementation of Kruskal’s algorithm.

if we use a Fibonacci heap to implement the min-priority queue Q, the running time of Prim’s
algorithm improves to O(E + VlgV)

<hr />