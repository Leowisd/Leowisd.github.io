---
title: NP-Completeness
tags: [P, NP, NPC, NPC-Complete]
mathjax: true
date: 2018-12-03 20:09:48
categories: Algorithms
description: Review of NPC
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fxuntyysxzj212w0m8ab6.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## NP-completeness and the classes P and NP

### Classes P

The class P consists of those problems that are solvable in polynomial time.

More specifically, they are problems that can be solved in time $O(n^k)$ for some
constant k, where n is the size of the input to the problem.

### Classes NP

The class NP consists of those problems that are “verifiable” in polynomial time.

What do we mean by a problem being verifiable? If we were somehow given a
“certificate” of a solution, then we could verify that the certificate is correct in time
polynomial in the size of the input to the problem.

### NP-completeness

Informally, a problem is in the class NPC—and we refer to it as being NP-complete if 
it is in NP and is as “hard” as any problem in NP.

In the meantime, we will state without proof that if any NP-complete problem
can be solved in polynomial time, then every problem in NP has a polynomialtime
algorithm.

### Reference: 

![P问题、NP问题、NPC问题的概念及实例证明](https://blog.csdn.net/golden1314521/article/details/51470999)

## Polynomial time

### Abstract problems

To understand the class of polynomial-time solvable problems, we must first have
a formal notion of what a “problem” is. We define an abstract problem **Q** to be a
binary relation on a set **I** of problem instances and a set **S** of problem solutions.
For example, an instance for **SHORTEST-PATH** is a triple consisting of a graph
and two vertices. A solution is a sequence of vertices in the graph, with perhaps
the empty sequence denoting that no path exists. The problem **SHORTEST-PATH**
itself is the relation that associates each instance of a graph and two vertices with
a shortest path in the graph that connects the two vertices. Since shortest paths are
not necessarily unique, a given problem instance may have more than one solution.

### Endocing

In order for a computer program to solve an abstract problem, we must represent
problem instances in a way that the program understands. An encoding of a set S
of abstract objects is a mapping e from S to the set of binary strings.

### A formal-language framework

Omit!

### Exercise

Show that if an algorithm makes at most a constant number of calls to polynomial-time subroutines and performs an additional amount of work that also takes polynomial time, then it runs in polynomial time. Also show that a polynomial number of calls to polynomial-time subroutines may result in an exponential-time algorithm.

![](http://ww1.sinaimg.cn/large/cf684029ly1fxuk9s3tlmj20h80d6q5j.jpg)
![](http://ww1.sinaimg.cn/large/cf684029ly1fxuk9y886hj20hz073js2.jpg)

## Polynomial-time verification

### Hamiltonian cycles

A hamiltonian cycle of an undirected graph $G=(V;E)$ is a simple cycle that contains each vertex in $V$. A graph that contains a hamiltonian cycle is said to be hamiltonian; otherwise, it is nonhamiltonian.

We can define the hamiltonian-cycle problem, “Does a graph G have a hamiltonian cycle?” as a formal language:

$$HAM-CYCLE = \{(G) : G is a hamiltonian graph\}$$

This naive algorithm does not run in polynomial time. In fact, the hamiltonian-cycle problem is NP-complete.

### Verification algorithms

We define a verification algorithm as being a two-argument algorithm A, where one argument is an ordinary input string x and the other is a binary string y called a certificate. A two-argument algorithm A verifies an input string x if there exists a certificate y such that $A(x,y) = 1$. The language verified by a verification algorithm A is

$$L = \{x \in \{0,1\}^* : there \space exists \space y \in \{0, 1\}^* such \space that \space A(x,y) = 1\}$$

### The complexity class NP

Omit!

### Exercises

#### Question 1
Prove that if $G$ is an undirected bipartite graph with an odd number of vertices, then $G$ is nonhamiltonian.

#### Answer
Let graph G be a bipartite graph with an odd number of vertices and G be Hamiltonian, meaning that there is a directed cycle that includes every vertex of G. As such, there exists a cycle in G would of odd length. However, a graph G is bipartite if and only if every cycle of G has even length. Proven by contradiction, if G is a bipartite graph with an odd number of vertices, then G is non-Hamiltonian.

#### Question 2
Show that any language in NP can be decided by an algorithm running in time $2^{O(n^k)}$ for some constant k.

#### Answer
![](http://ww1.sinaimg.cn/large/cf684029ly1fxukxkdlysj20go0av3zt.jpg)

#### Question 3
A hamiltonian path in a graph is a simple path that visits every vertex exactly
once. Show that the language $HAM-PATH = \{(G, u , i): there \space is \space a \space hamiltonian \space path \space from \space u \space to \space i \space in \space graph \space G\}$ belongs to NP.

#### Answer
![](http://ww1.sinaimg.cn/large/cf684029ly1fxuleeazmtj20gq07hgn1.jpg)

#### Question 4
Show that the hamiltonian-path problem from Exercise 34.2-6 can be solved in polynomial time on directed acyclic graphs. Give an efficient algorithm for the problem.

#### Answer
For this particular problem, we could find a polynomial-time solution for it and then it's proven it could be solved in polynomial-time.

In this following step, I will give some steps that will demonstrate it will resolve the problem:

1) find a path in the original graph $G$ that in-degree is zero, because for a DAG it must have a source node that in-degree is zero. If there're more than one nodes, then there is no solution, since every node must be visited, but the zero degree should start first and if there're more than one point, then there must be some nodes that left cannot be visited at first.

2) remove the source node which in-degree is zero and its neighboring edges so that we could find the next node to start, let's assume that the left graph is $G'$.

3) if the left graph $G'$ has more than two nodes or vertices that have the in-degree which is zero, then we could judge that it's unsolvable, because as I said in 1) there is no way to visit those nodes since there in-degree is zero and there should only be one to visit after its predecessor.

4) keep doing the 3) until we have reached the end-point, which there is no other nodes to visit. If there is some nodes that are not visited but we cannot find an edge to reach it, then it's unsolvable, otherwise we should get the solution.

From the above steps, we have found the solution for the hamiltonian-path, and its complexity if $O(|E|+|V|)$, while here $|V|$ is the number of vertices in the graph and $|E|$ is the number of edges in the graph, because we have to trace the vertices and its neighborhood edges from $v_{1}$ to $v_{n}$. We know that it is done in polynomial time.

## NP-completeness and reducibility

### Reducibility

A language $L_1$ is polynomial-time reducible to a language $L_2$, written $L_1 \leq_p L_2$

If there exists a polynomial-time computable function $f :\{0, 1\}^* \rightarrow \{0, 1\}^*$ such that for all $x \in \{0, 1\}^*$,

$$x \in L_1 \space if \space and \space only \space if \space f(x) \in L_2 $$

We call the function f the **reduction function**, and a polynomial-time algorithm F that computes f is a **reduction algorithm**.

### NP-completeness

A language $L \in \{0,1\}$ is NP-complete if
1. $L \in NP$, and
2. $L' \leq_p L$ for every $L' \in NP$.

If a language L satisfies property 2, but not necessarily property 1, we say that L is NP-hard. We also define NPC to be the class of NP-complete languages.

### Circuit satisfiability

The language CIRCUIT-SAT is therefore at least as hard as any language in NP, and since it belongs to NP, it is NP-complete.

### Exercise

#### Question 1
Show that the $\leq_p$ relation is a transitive relation on languages. That is, show that if $L_1 \leq_p L_2$ and $L_2 \leq_p L_3$, then $L_1 \leq_p L_3$.

#### Answer
![](http://ww1.sinaimg.cn/large/cf684029ly1fxumuzljmej20gk05yq3g.jpg)

#### Question 2
A language L is complete for a language class C with respect to polynomial-time reductions if $L \in C$ and $L' \leq_p L$ for all $L' \in C$. Show that $\empty$ and $\{0,1\}^*$ are the only languages in P that are not complete for P with respect to polynomial-time reductions.

#### Answer
Omit

## NP-completeness proofs

Language L is NP-complete:

1. Prove $L \in NP$.
2. Select a known NP-complete language $L'$.
3. Describe an algorithm that computes a function $f$ mapping every instance $x \in \{0,1\}^*$ of $L'$ to an instance $f(x)$ of $L$.
4. Prove that the function $f$ satisfies $x \in L'$ if and only if $f(x) \in L$ for all $x \in \{0,1\}^*$.
5. Prove that the algorithm computing $f$ runs in polynomial time.

### 3-CNF satisfiability

We define 3-CNF satisfiability using the following terms. A literal in a boolean formula is an occurrence of a variable or its negation. A boolean formula is in conjunctive normal form, or CNF, if it is expressed as an AND of clauses, each of which is the OR of one or more literals. A boolean formula is in 3-conjunctive normal form, or 3-CNF, if each clause has exactly three distinct literals.

#### Theorem
Satisfiability of boolean formulas in 3-conjunctive normal form is NP-complete.

### Exercises

#### Question 1

Consider the straightforward (nonpolynomial-time) reduction in the proof of Theorem 34.9. Describe a circuit of size n that, when converted to a formula by this method, yields a formula whose size is exponential in n.

#### Answer

#### Question 2

Suppose that someone gives you a polynomial-time algorithm to decide formula satisfiability. Describe how to use this algorithm to find satisfying assignments in polynomial time.

#### Answer

![](http://ww1.sinaimg.cn/large/cf684029ly1fxvn7ofocfj20gq06agn7.jpg)
![](http://ww1.sinaimg.cn/large/cf684029ly1fxvn8cgbw0j20gp03f0t3.jpg)

## NP-complete problems

What the F***!

### Exercises

#### Question 1

The subgraph-isomorphism problem takes two undirected graphs $G_1$ and $G_2$, and it asks whether $G_1$ is isomorphic to a subgraph of $G_2$. Show that the subgraph-isomorphism problem is NP-complete.

#### Answer
![](http://ww1.sinaimg.cn/large/cf684029ly1fxvo8qcea8j20g905575j.jpg)
![](http://ww1.sinaimg.cn/large/cf684029ly1fxvo8w97ftj20i10ajgoz.jpg)

<hr />