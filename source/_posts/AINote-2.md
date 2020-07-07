---
title: 2-Problem Solving
tags: [AI, Course Note, Algorithm, Search, DFS, BFS, IDS, Iterative Deepening Search, A*, Uniform-Cost Search, Greedy best-first Search]
date: 2018-09-05 18:38:55
categories: Course
description: The Note of AI Course
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fuzkfsqtqpj212w0m87wi.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## DEFINITION OF A PROBLEM
* Initial state
* Actions(s) -> {a1,a2,a3,......}
* Result(s, a) -> s'
* GoalTest(s) -> T|F
* Path Cost(s,a) -> n
  StepCost(s,a,s') -> m

## Problem types
* Deterministic, fully observable => single-state problem
* Non-observable => conformant problem
* Nondeterministic and/or partially observable => contingency problem
* Unknown state space => exploration problem("online")

## BFS
**Optimal**: Yes. Always find the shortest(not the cheapest) path.

**Complete**: Yes

**Time**: $O(b^{d+1})$

**Space**: $O(b^{d+1})$

**Implement** 

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
        // GOAL-TEST(v)
        ENQUEUE(Q, v)
  u.color = BLACK

Note: WHITE-NOT EXPANDED  GRAY-FRONTIER BLACK-EXPLORED
      Q is a FIFO queue
      s is the source vertex
      GOAL-TEST(v) to test if v is the goal vertex

Based on Intro to Algorithms. 3rd Edition. P595
```

## Uniform-Cost Search (Cheapest-Search)
Stop only until the goal is removed from Frontier to Explored

**Optimal:** Yes. Always find the cheapest path

**Complete:** Yes

**Implement** 
```
Uniform-Cost Search(G, s)
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
  // GOAL-TEST(u)
  for each v <- G. Adj[u]
    if v.color == WHITE
        v.color = GRAY
        v.distance = u.distance + cost[u, v]
        v.pre = u
        ENQUEUE(Q, v)
  Q.sort()  //by distance
  u.color = BLACK

Note: WHITE-NOT EXPANDED  GRAY-FRONTIER BLACK-EXPLORED
      s is the source vertex
      Q.sort() sorts vertices by their cost (most from lowest to highest)
      GOAL-TEST(u) is different from BFS because it can find the cheapest path correctly only when the goal vertx is removed from Frontier to Explored(most, when values of paths are different)

Based on Intro to Algorithms. 3rd Edition. P595
```

## DFS
**Optimal:** No. For example, in the tree below, if there is a goal both in 3 and 5, it will find 3 but not find 5, so it can't find the shortest path.
![](http://ww1.sinaimg.cn/large/cf684029ly1fuzk4l7z7fj204j03jgm0.jpg)

**Complete:** No. If there is a infinite tree, it will have a endless path to go down

**Time**: $O(b^m)$

**Space**: $O(bm)$

**Implement** 
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
// GOAL-TEST(u)
u.color = GREY
for each v <- G.Adj[u]  //explore edge (u,v)
  if v.color == WHITE
    v.pre = u
    DFS-VISIT(G, v)
u.color = BLACK //blacken u; it is finished
time = time + 1
u.f = time

Note: WHITE-NOT EXPANDED  GRAY-FRONTIER BLACK-EXPLORED
      time is global variable using for timestamping
      DFS records when it discovers vertex u in the attribute u.d and when it finishes vertex u in the attribute u.f
      u.d < u.f

Based on Intro to Algorithms. 3rd Edition. P604
```

## Iterative Deepening Search
**Optimal:** Yes

**Complete:** Yes

**Time**: $O(b^d)$

**Space**: $O(bd)$

**Implement** 
```
function ITERATIVE-DEEPENING-SEARCH(problem) returns a solution, or failure
  for depth = 0 to infinity do
    result = DEPTH-LIMITED=SEARCH(problem, depth)
    if result != cutoff then return result

function DEPTH-LIMITED-SEARCH(problem, limit) returns a solution, or failure/cutoff
  return RECURSIVE-DLS(MAKE-NODE(problem, INITIAL-STATE), problem, limit)

function RECURSIVE-DLS(node, problem, limit) returns a solution, or failure/cutoff
  if problem.GOAL-TEST(node, STATE) then returns SOLUTION(node)
  else if limit = 0 then return cutoff
  else
    cutoff_occurred? = false
    for each action in problem, ACTIONS(node, STATE) do
      child = CHILD_NODE(problem, node, action)
      result = RECURSIVE_DLS(child, problem, limit-1)
      if result = cutoff then cutoff_occured? = true
      else if result != failure then return result
    if curoff_occured? then return cutoff else return failure

Based on Artifical Intelligence: A Modern Approch, 3rd Edition. P88~P89
```

## Greedy best-first Search
**Optimal:** No

**Complete:** No

**Time**: $O(b^m)$

**Space**: $O(bm)$

**Implement**

Evaluation function h(n) (heuristic) = estimate of cost from n to the closest goal
E.g., hSLD(n) = straight-line distance from n to Bucharest
Greedy search expands the node that appears to be closest to goal

## A* Search (Heuristic Search)
```
f = g + h
g(path) = path cost
h(path) = h(s) = estimated distance to the goal
Stop only until the goal is removed from Frontier
```
**Finds lowest cost path if:**
* **h(s) <= true cost**
* h never overestimate
* h optimistic
* h admissable

**Implement** 
```
A*(G, s)
for each vertex u <- G. V - {s}
  u.color = WHITE
  u.distance = infinity
  u.pre = NULL
s.color = GRAY
s.distance = 0
s.pre = NULL
s.f = s.distance + h(s)
Q = NULL
ENQUEUE(Q, s)
while Q != NULL
  u = DEQUEUE(Q)
  // GOAL-TEST(u)
  for each v <- G. Adj[u]
    if v.color == WHITE
        v.color = GRAY
        v.distance = u.distance + cost[u, v]
        v.f = v.distance + h(v)
        v.pre = u
        ENQUEUE(Q, v)
  Q.sort()  //by f
  u.color = BLACK

Note: WHITE-NOT EXPANDED  GRAY-FRONTIER BLACK-EXPLORED
      s is the source vertex
      h(u) is the estimated distance to the goal vertex
      Q.sort() sorts vertices by their u.f which is equal to u.distance + h(u)
      A* stops searching only when the goal vertx is removed from Frontier to Explored(most, when values of paths are different)

Based on Intro to Algorithms. 3rd Edition. P595
```

## Problems with Search
Problem-Sloving works when:
* Fully Observable
* Known state space
* Discrete
* Deterministic
* Static
<hr />