---
title: Single-Source Shortest Paths
tags: [Graph Algorithms, Single-Source Shortest Paths, Bellman-Ford, Dijkstra]
date: 2018-10-13 09:32:10
categories: Algorithms
description: Review of Graph Algorithms
mathjax: true
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fw6z6dlblbj212w0m8ti0.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Concept

### Lemma 24.1 (Subpaths of shortest paths are shortest paths)

Given a weighted, directed graph G = (V, E) with weight function w:E->R, let P = (v0,v1,...,vk) be a shortest path from vertex v0 to vertex vk and, for any i and j such as 0<=i<=j<=k, let Pij = (vi,vi+1,...,vj) be the subpath of P from vertex vi to vertex vj. Then, Pij is a shortest path from vi to vj.

### Negative-weight edges

Some instances of the single-source shortest-paths problem may include edges whose weights are negative. If the graph G(V,E) contains no negativeweight cycles reachable from the source s, then for all v <- V , the shortest-path weight P(s,v) remains well defined, even if it has a negative value. If the graph contains a negative-weight cycle reachable from s, however, shortest-path weights are not well defined. No path from s to a vertex on the cycle can be a shortest path—we can always find a path with lower weight by following the proposed “shortest” path and then traversing the negative-weight cycle. If there is a negativeweight cycle on some path from s to v, we define P(s,v)=-infinity.

### Cycle

As we have just seen, it cannot contain a negative-weight cycle. Nor can it contain a positive-weight cycle, since removing the cycle from the path produces a path with the same source and destination vertices and a lower path weight. 

That leaves only 0-weight cycles. We can remove a 0-weight cycle from any path to produce another path whose weight is the same. Thus, if there is a shortest path from a source vertex s to a destination vertex v that contains a 0-weight cycle, then there is another shortest path from s to v without this cycle. As long as a shortest path has 0-weight cycles, we can repeatedly remove these cycles from the path until we have a shortest path that is cycle-free. Therefore, without loss of generality we can assume that when we are finding shortest paths, they have no cycles, i.e., they are simple paths.

### Relaxation

For each vertex v<-V, we maintain an attribute v.d, which is an upper bound on the weight of a shortest path from source s to v. We call v.d a shortest-path estimate.
```
INITIALIZE-SINGLE-SOURCE(G,s)
1   for each vertex v <- G.V
2       v.d = infinity
3       v.pre = NIL
4   s.d=0
```

The following code performs a relaxation step on edge (u,v) in O(1) time:
```
RELAX(u,v,w)
1   if v.d > u.d + w(u,v)
2       v.d = u.d + w(u,v)
3       v.pre = u 
```

### Properties of shortest paths and relaxation

#### Triangle inequality (Lemma 24.10)

For any edge(u,v) <- E, we have d(s,v) <= d(s,u) + w(u,v).

#### Upper-bound property (Lemma 24.11)

We always have v.d >= P(s, v) for all vertices v <- V , and once v.d achieves the value d(s,v), it never changes.

#### No-path property (Corollary 24.12)

If there is no path from s to v, then we always have v.d = d(s,v) = infinity.

#### Convergence property (Lemma 24.14)

If s ~> u -> v is a shortest path in G for some u; u,v <- V , and if u.d = d(s, u) at any time prior to relaxing edge (u,v), then v.d = d(s, v) at all times afterward.

#### Path-relaxation property (Lemma 24.15)

If $p=(v_1,v_2,\ldots,v_k)$ is a shortest path from s=v0 to vk, and we relax the edges of p in the order (v0, v1), (v1, v2), ....,(vx-1,vk), then vk.d = d(s,vk). This property holds regardless of any other relaxation steps that occur, even if they are intermixed with relaxations of the edges of p.

#### Predecessor-subgraph property (Lemma 24.17)

Once v.d = d(s,v) for all v <- V , the predecessor subgraph is a shortest-paths tree rooted at s.

## The Bellman-Ford algorithm

The Bellman-Ford algorithm solves the single-source shortest-paths problem in the general case in which edge weights may be negative. The Bellman-Ford algorithm returns a boolean value indicating whether or not there is a negative-weight cycle that is reachable from the source. If there is such a cycle, the algorithm indicates that no solution exists. If there is no such cycle, the algorithm produces the shortest paths and their weights.

```
BELLMAN-FORD(G,w,s)
1   INITIALIZE-SINGLE-SOURCE(G,s)
2   for i = 1 to |G.V|-1
3       for each edge(u,v) <- G.E
4           RELAX(u,v,w)
5   for each edge(u,v) <- G.E
6       if v.d > u.d + w(u,v)
7           return FALSE
```

Running Time: O(VE)

## Single-source shortest paths in directed acyclic graphs

By relaxing the edges of a weighted dag (directed acyclic graph) $ G=(V,E) $ according to a topological sort of its vertices, we can compute shortest paths from a single source in $\Theta(V + E)$ time.

```
DAG-SHORTEST-PATHS(G,w,s)
1   topologically sort the vertices of G
2   INITIALIZE-SINGLE-SOURCE(G,s)
3   for each vertex u, taken in topologicall sorted order
4       for each vertex v <- G.Adj[u]
5           RELAX(u,v,w)
```

## Dijkstra’s algorithm

Dijkstra’s algorithm solves the single-source shortest-paths problem on a weighted, directed graph $G=(V, E)$ for the case in which all edge weights are nonnegative.

```
DIJKSTRA(G,w,s)
1   INITIALIZE-SINGLE-SOURCE(G,s)
2   S = null
3   Q = G.V
4   while Q != null
5       u = EXTRACT-MIN(Q)
6       S = S U {u}
7       for each vertex v<-G.Adj[u]
8           RELAX(u,v,w)
```

Dijkstra’s algorithm? It maintains the min-priority queue Q by calling three priority-queue operations: INSERT (implicit in line 3), EXTRACT-MIN(line 5), and DECREASE-KEY (implicit in RELAX, which is called in line 8).

The running time of Dijkstra’s algorithm depends on how we implement the min-priority queue. For a total time of $O(V^2+E)=O(V^2)$

If the graph is sufficiently sparse—in particular, $E = o(V^2/lgV)$—we can improve the algorithm by implementing the min-priority queue with a binary minheap. The total running time is therefore $O((V+E)lgV)$, which is $O(ElgV)$ if all vertices are reachable from the source.This running time improves upon the straightforward $O(V^2)$ time implementation if $E = o(V^2/lgV)$.

We can in fact achieve a running time of $O(VlgV + E)$ by implementing the min-priority queue with a Fibonacci heap

<hr />