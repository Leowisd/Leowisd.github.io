---
title: 5-Constraint Satisfacation Problems
tags: [AI, Course Note, Algorithm, Constraint Satisfacation Problems, CSPs]
date: 2018-10-06 20:52:13
categories: Course
description: The Note of AI Course
image:
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvzfi0y2tfj212w0m8aiw.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Constraint Satisfacation Problems

For CSP, state is defined by variables X, with vlaues from domain D. Goal test is a set of constraints specifying, allowable combinations of values for subsets of variables.

For example, Map-coloring problem:

![](http://ww1.sinaimg.cn/large/cf684029ly1fvzfy7nqt1j20ir0duwg5.jpg)

### Constraint Graph

Binary CSP: each constraint relates at most two variables

Constraint graph: nodes are variables, arcs are constraints

![](http://ww1.sinaimg.cn/large/cf684029ly1fvzg0x7i1rj20e707cmxb.jpg)

### Extra example: Cryptarithmetic

![](http://ww1.sinaimg.cn/large/cf684029ly1fvzg2zl7b6j20hj094t9k.jpg)

Variable：F T U W R O X1 X2 X3

Domain：{0,1,2,3,4,5,6,7,8,9}

Constraints：alldiff (F,T,U,W,R,O)

O + O = R + 10 * X1

X1 + W + W = U + 10 * X2

X2 + T + T = O + 10 * X3

X3 = F , T ≠ 0, F ≠ 0

## Backtracking search

Depth-first search for CSPs with single-variable assignments is called backtracking search. Backtracking search is the basic uniformed algrithom for CSPs. It can solve n-queens for n almost equals to 25.

```
function BACKTRACKING-SEARCH(csp) returns solution/failure
    return RECURSIVE-BACKTRACKING({},csp)
function RESCURSIVE-BACKTRACKING(assignment,csp) returns solution/failure
    if assignment is complete then return assignment
    var <- SELECT-UNASSIGNED-VALRIABLE(VARIABLES[csp], assignment,csp)
    for each value in ORDER-DOMAIN-VALUES(var, assignment, csp) do
        if value is consistent with assignment given CONSTRAINTS[csp] then
            add {var = value} to assignment
            result <- RESCURSIVE-BACKTRACKING(assignment,csp)
            if result != failue then return result
            remove {var = value} from assignment
    return failue
```

## Minimum remaining values （最小剩余值）

Choose the variable with the fewest legal values. 

选择拥有最少合法值的变量，即约束最多的一个，按照最快失败顺序

## Degree heuristic （度启发式）

Tie-breaker among MRV variables, choose the variable with the most constraints on remaining variables. 

选择与其他未赋值变量约束最多的变量

## Least constraining value （最少约束值）

Given a variable, choose the least constraining value: the one that rules out the fewest values in the remaining variables

给定一个变量，选择最少约束值：优先选择的值是给邻居变量留下更多的选择

## Forward checking

Idea: Keep track of remaining legal values for unassigned variables. Terminate search when any variable has no legal values

对剩下的未赋值的变量的合法值进行跟踪检查，如果发现任一变量不再拥有合法值则终止搜索算法

### Constraint propagation

Forward checking propagates information from assigned to unassigned variables, but doesn’t provide early detection for all failures:

![](http://ww1.sinaimg.cn/large/cf684029ly1fvzi8yaqylj20dr05iq31.jpg)

NT and SA cannot both be blue!

Constraint propagation repeatedly enforces constraints locally

前向检查从已赋值的变量向未赋值的变量传播信息，但是不对早期的失败提供早期的发现:

约束传播局部重复地实施约束

## Arc consistency (弧相容算法 AC-3)

```
function AC-3(csp) returns the CSP, possibly with reduced domains
    inputs:csp, a binary CSP with variables {X1,X2,...,Xn}
    local variables:queue, a queue of arcs, initially all the arcs in csp
    while queue is not empty do
        (Xi,Xj) ← REMOVE-FIRST(queue)
        if REMOVE-INCONSISTENT-VALUES(Xi,Xj) then
            for each Xk in NEIGHBORS[Xi] do
                add (Xk,Xi) to queue

function REMOVE-INCONSISTENT-VALUES(Xi,Xj) returns true iff succeeds
    removed ← false
    for each x in DOMAIN[Xi] do
        if no value y in DOMAIN[Xj] allows (x,y) to satisfy the constraint (Xi, Xj)
            then delete x from DOMAIN[Xi]; removed ← true
    return removed
```

O(n^2^d^3^), can be reduced to O(n^2^d^2^) (but detecting all is NP-hard)

## Tree-structured CSPs

Theorem: if the constraint graph has no loops, the CSP can be solved in O(nd^2^) time

### Algorithm for tree-structured CSPs

![](http://ww1.sinaimg.cn/large/cf684029ly1fw038c5kc5j20fj03wwen.jpg)

1. Choose a variable as root, order variables from root to leaves such that every node’s parent precedes it in the ordering
2. For j from n down to 2, apply RemoveInconsistent(Parent(Xj), Xj)
3. For j from 1 to n, assign Xj consistently with Parent(Xj)


<hr />