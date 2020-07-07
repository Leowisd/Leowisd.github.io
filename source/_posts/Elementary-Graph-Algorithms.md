---
title: Elementary Graph Algorithms
tags: [Graph Algorithms, BFS, DFS, Strongly connected components, Topological sort]
date: 2018-09-15 09:06:37
categories: Algorithms
description: Review of Graph Algorithms
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fval0u3xbzj212w0m84qk.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Representations of graphs

### Concept

We can choose between two standard ways to represent a graph G=(V,E):
as a collection of adjacency lists or as an adjacency matrix.

##### Two representations of an undirected graph

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb52095jqj20h004074c.jpg" alt="" style="width:100%" />

##### Two representations of a directed graph

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb52s0ohfj20gh057mx9.jpg" alt="" style="width:100%" />

### Exercises

_From Introduction to Algorithms, 3rd edition_

##### 22.1-1 

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb5d280foj20e401lmx5.jpg" alt="" style="width:100%" />

##### Answer

Assume that the number of vertexes is N, the munber of edges is M. 

It will take O(N) to compute the out-degree of every vertex.

It will take O(N+M) to compute the in-degree.

##### 22.1-3

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb4o60vv8j20e002oq37.jpg" alt="" style="width:100%" />

##### Answer

Assume that the number of vertexes is N, the number of edges is M.

For adjacency-list, iterate all the nodes, for each node i, mark its adjacency-list as L, then add i to all the nodes in L. It costs O(N+M).

For adjacency-matrix, just only transpose the matrix. It costs O(N*N).

##### 22.1-4

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb5egz93bj20e302p74j.jpg" alt="" style="width:100%" />

##### Answer

* Iterate through all the vertices in the multigraph.
* For each of the vertices, iterate through their multigraph adjacency list.
* While iterating through the multigraph adjacency list of a vertex u, add the neighbor to the new adjacency list of u and u to the new adjacency list of the neighbor, if the neighbor is not vertex u itself and if the neighbor is not already present in the new adjacency list of u.
* The new adjacency list array is a representation of the required undirected graph.

##### 22.1-6

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb5r6ckzgj20e602074h.jpg" alt="" style="width:100%" />

##### Answer

If vertex i is a universal sink according to the definition, the i-th row of the adjacency-matrix will be all “0”, and the i-th column will be all “1” except the A(i,i) entry, and clearly there is only one such vertex. We then describe an algorithm to find out if a universal sink really exist.

Starts from A(1,1). If current entry a(i,j) = 0 then j = j + 1 (take one step right); if A(i,j) = 1 then i = i +1 (take one step down). In this way, it will stop at an entry A(k,n) of the last row or A(n,k) of the last column (n = |V|, 1 ≦ k ≦|V|). Check if vertex k satisfies the definition of universal sink (check for kth row to contain V zeros and kth column to contain k-1 1s, because the column in adajacency matrix defines in degree of a vertex), if yes then we found it, if no then there is no universal sink. Since we always make a step right or down, and checking if a vertex is a universal sink can be done in O(V), the total running time is O(V).

If there is no universal sink, this algorithm won’t return any vertex. If there is a universal sink u, the path starts from A(1,1) will definitely meet u-th column or u-th row at some entry. Once it’s on track, it can’t get out of the track and will finally stop at the right entry.

##### 22.1-7

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb69fuqqjj20e404kglw.jpg" alt="" style="width:100%" />

##### Answer

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb7dwh2i3j20de0520t4.jpg" alt="" style="width:100%" />

Note: The **incidence matrix** is |V| * |E| not |V|*|V|. It's a matrix to represent the relation between vertexes and edges.

## Breadth-First Search

### Concept

##### pseudocode

```
BFS(G, s)
for each vertex u <- G. V - {s}
  u.color = WHITE
  u.distance = infinity
  u.pre = NULL
s.color = GRAY
s.distance = 0
s.pre = NULL
Q = NULL
ENQUEUE(Q, s)
while Q != NULL
  u = DEQUEUE(Q)
  for each v <- G. Adj[u]
    if v.color == WHITE
        v.color = GRAY
        v.distance = u.distance + cost[u, v]
        v.pre = u
        ENQUEUE(Q, v)
  u.color = BLACK
```

### Exercises

##### 22.2-1

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb7za951aj20dz0193yg.jpg" alt="" style="width:100%" />

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb7ycswqbj204p03f3yc.jpg" alt="" />

##### Answer

| Vertex | d | pre |
| :---: | :---: | :---: |
| 3 | 0 | NULL |
| 5 | 1 | 3 |
| 6 | 1 | 3 |
| 4 | 2 | 5 |
| 2 | 3 | 4 |
| 1 | Infinity | NULL |

##### 22.2-6

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb8bry5ppj20e702k74j.jpg" alt="" style="width:100%" />

##### Answer

To find such a graph, we simply need to think how BFS tree edges come about: once a node is discovered, we will not have another tree edge to that node. So to provide a directed graph tree edge set that cannot be produced by running BFS, we simply need multiple paths to given nodes, and choose paths based on different starting points:

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb8pa2y6bj20kk06djr9.jpg" alt="" />

In this simple example above, assuming that we run a BFS on A, we can either start exploring from B or start exploring from C. These would yield the following BFS trees:

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb8r2bqamj20hq06bdfp.jpg" alt="" />

To find a set of tree edges that cannot be found from BFS, we simply need to choose at least one minimum path that exists only in the first tree, and one path that exists only in the second tree. We choose {(A,B), (B,D), (A,C), (C,E)}.

##### 22.2-7

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb8tb404rj20e3043jrw.jpg" alt="" style="width:100%" />

##### Answer

[**Bipartite Graph problem.**]()

Run DFS or BFS, the start node we could mark as white. Each time, we encounter a node, if it is not currently colored, we should mark it as the opposite color of current node. Else, check the color with current node. If same, then it is not bipartite graph.

##### 22.2-8

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvb90do7sgj20e301kglo.jpg" alt="" style="width:100%" />

##### Answer

##### Solution 1

For all node v, run BFS each, and choose the longest shortest path. Running time is O(V*(V+E))

##### Solution 2

USing Floyd algorithm to calculate all point-point shortest path. Running time is O(V^3)

##### Solution 3

Running BFS twice, arbitrarily choose a vertex as the source. The second time, let the vertex with largest d[] be the source.

##### Solution 4

The diameter of a tree can computed in a bottom-up fashion using a recursive solution. Running Time is O(N), in the other word, a linear solution.

[Click here to see more details about Solution 3 and Solution 4](https://blog.csdn.net/qq_32400847/article/details/51469917) 

## Depth-First Search

### Concept

##### pseudocode

```
DFS(G)
for each vertex u <- G.V
  u.color = WHITE
  u.pre = NULL
time = 0
for each vertex u <- G.V
  if u.color == WHITE
    DFS-VISIT(G, u)


DFS-VISIT(G, u)
time = time + 1 //white vertex u has just been discovered
u.d = time
u.color = GREY
for each v <- G.Adj[u]  //explore edge (u,v)
  if v.color == WHITE
    v.pre = u
    DFS-VISIT(G, v)
u.color = BLACK //blacken u; it is finished
time = time + 1
u.f = time
```
##### CLassification of edges

* Tree edges are edges in the depth-first forest G'.Edge(u,v) is a tree edge if v was first discovered by exploring edge (u,v).
* Back edges are those edges (u,v) connecting a vertex u to an ancestor v in a depth-first tree. We consider self-loops, which may occur in directed graphs, to be back edges.
* Forward edges are those nontree edges (u,v) connecting a vertex u to a descendant v in a depth-first tree.
* Cross edges are all other edges. They can go between vertices in the same depth-first tree, as long as one vertex is not an ancestor of the other, or they can go between vertices in different depth-first trees.

### Exercises

##### 22.3-5

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbpo1biq2j20c402yt8t.jpg" alt="" style="width:100%" />

##### Answer

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbq76ibjjj20kv0eywgq.jpg" alt="" style="width:100%" />

##### 22.3-7

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbpu8a94ij20bf00o744.jpg" alt="" style="width:100%" />

##### Answer

```
DFS_Stack(G)
for each vertex u <- G.V
  u.color = WHITE
  u.pre = NULL
s.color = GRAY
s.pre = NULL
ENQUEUE(Q,s)
while Q != NULL
  u = pop(Q)
  for each v <- G.Adj[u] 
    if v.color = WHITE
      v.pre = u
      v.color = GRAY
      ENQUEUE(Q, v)
```

##### 22.3-8

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbqcggn42j20e801mq2y.jpg" alt="" style="width:100%" />

##### Answer

Let us consider the example graph depth-first search below

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbqhdqp4qj20mp0fuab1.jpg" alt="" style="width:100%" />

CLearly, there is a path from u to v in G. The bold edges are in the depth-first forest produced by search. We can see that u.d < v.d in the depth-first search but v is not a descendant of u in the forest.

##### 22.3-9

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbqoda9r9j20e60143yg.jpg" alt="" style="width:100%" />

##### Answer

Let us consider the example graph depth-first search below

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbqhdqp4qj20mp0fuab1.jpg" alt="" style="width:100%" />

CLearly, there is a path from u to v in G. The bold edges are in the depth-first forest produced by search. However, v.d > u.f and the conjecture is false.

##### 22.3-10

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbr0mqgagj20e201lq2y.jpg" alt="" style="width:100%" />

##### Answer

We need only update DFS-VISIT. If G is undirected we don't need to make any modifications.

```
DFS-VISIT-PRINT(G, u)
  time = time + 1
  u.d = time
  u.color = GRAY
  for each v in G.Adj[u]
      if v.color == white
          print "(u,v) is a Tree edge."
          v.PI = u
          DFS-VISIT-PRINT(G, v)
      else if v.color == gray
          print "(u, v) is a Back edge."
      else
          if v.d > u.d
              print "(u, v) is a Forward edge."
          else print "(u, v) is a Cross edge."
  u.color = BLACK //blacken u; it is finished
  time = time + 1
  u.f = time
```

NOte, the porve can be found in 22.3-5

##### 22.3-11

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbr4wf923j20e3011t8n.jpg" alt="" style="width:100%" />

##### Answer

Let us consider the example graph and depth-first search below.

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbr7m1mvzj20pg08hwf3.jpg" alt="" style="width:100%" />

Cleary u has both incoming and outgoing edges in G but a depth-first search of G produced a depth-first forest where u is in a tree by itself.

##### 22.3-13

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbr9ofnemj20e101mglp.jpg" alt="" style="width:100%" />

##### Answer

Run DFS for each vertex in the graph, if there are no crosses edges and forward edges in the DFS tree, the graph must be single connected. Running time is O(V*(V+E)).

[More details and methods on this question, please click here](https://blog.csdn.net/wdq347/article/details/11096945)

## Topological sort

### Concept

##### Pseudocode

```
TOPOLOGICAL-SORT(G)
  call DFS(G) to compute finishing times v.f for each vertex v
  as each vertex is finsished, insert it onto the front of a linked list
  return the linked list of vertices
```

### Exercises

##### 22.4-2

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbrvgc5xhj20e702l3yt.jpg" alt="" style="width:100%" />

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbrxq4ktsj207r05k3yl.jpg" alt="" />

##### Answer

The algorithm works as follows. The attribute u.paths of node u tells the number of simple paths from u to v, where we assume that v is fixed throughout the entire process. To count the number of paths, we can sum the number of paths which leave from each of u's neighbors. Since we have no cycles, we will never risk adding a partially completed number of paths. Moreover, we can never consider the same edge twice among the recursive calls. Therefore, the total number of executions of the for-loop over all recursive calls is O(V+E). Calling SIMPLE-PATHS(s,t) yields the desired result.

```
SIMPLE-PATHS(u, v)
    if u == v
        return 1
    else if u.paths != NIL
        return u.paths
    else
        for each w in Adj[u]
            u.pahts = u.paths + SIMPLE-PATHS(w, v)
        return u.paths
```

##### 22.4-3

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbsby7d2qj20e501kgll.jpg" alt="" style="width:100%" />

##### Answer

An undirected graph is acyclic if and only if a DFS yields no back edges.

* If there's a back edge, there's a cycle.
* If there's no back edge, then by Theorem 22.10, there are only tree edges. Hence, the graph is acyclic. Thus, we can run DFS: if we find a back edge, there's a cycle.
* Time: O(V).(Not O(V+E)), because if we ever see |v| distinct edges, we must have seen a back edge because in an acyclic (undirected) forest, |E|<=|V|-1. Thus, DFS's running time is O(V+E) but in such solution, O(V).

##### 22.4-4

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbsm64pryj20e201l3yk.jpg" alt="" style="width:100%" />

##### Answer

This is not true.

?

##### 22.4-5

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvbt0ohgzrj20e8022q34.jpg" alt="" style="width:100%" />

##### Answer

Running DFS or BFS to calculate in-degree for each vertex in O(V+E). After that, delete those vertexes whose in-degree are 0 and update these information. Each time, print the vertex whose in-degree is 0 and delete its out-edges. Thus, there are E edges and V vertexes in total, so it's need to run O(V) print and O(E) delete. So the total running time is O(V+E).

If there is a cycle, it may cannot find vertex with 0 in-degree, so not all vertices will be output

The other way is
```
TOPOLOGICAL-SORT(G)
    // Initialize in-degree, Θ(V) time.
    for each vertex u ∈ G.V
        u.in-degree = 0
    // Compute in-degree, Θ(V + E) time.
    for each vertex u ∈ G.V
        for each v ∈ G.Adj[u]
            v.in-degree = v.in-degree + 1
    // Initialize Queue, Θ(V) time.
    Q = ∅
    for each vertex u ∈ G.V
        if u.in-degree == 0
            ENQUEUE(Q, u)
    // while loop takes O(V + E) time.
    while Q != ∅
        u = DEQUEUE(Q)
        output u
        // for loop executes O(E) times total.
        for each v ∈ G.Adj[u]
            v.in-degree = v.in-degree - 1
            if v.in-degree == 0
                ENQUEUE(Q, v)
    // Check for cycles, O(V) time.
    for each vertex u ∈ G.V
        if u.in-degree != 0
            report that there's a cycle
    // Another way to check for cycles would be to count the vertices 
    // that are output and report a cycle if that number is < |V|.
```

## Strongly connected components

### Concept

A strongly connected component of a directed graph G = (V,E) is a maximal set of vertices such that for every pair of vertices u and v in C, we have both u -> v and v -> u; that is, vertices u and v are reachable from each other.

##### pseudocode
```
STRONGLY-CONNECTED-COMPONENTS(G)
1 call DFS(G) to compute finishing times u.f for each vertex u
2 compute GT
3 call DFS(GT), but in the main loop of DFS, consider the vertices in order of decreasing u.f
4 output the vertex of each tree in the depth-first forest formed in line 3 as a separate strongly connected component. 
```

### Exercises

##### 22.5-1

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvc236je4nj20e4015glh.jpg" alt="" style="width:100%" />

##### Answer

* If an edge is added in an SCC, the number of SCCs will remain the same.
* If an edge is added outside of an SCC, in a graph with n > 0 SCCs, the reduction in SCCs can be between 0 and (n-1).


<hr />