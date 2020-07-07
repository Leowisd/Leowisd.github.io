---
title: 4-Game_Adversarial Search
tags: [AI, Course Note, Algorithm, Game, Adversarial Search, Minimax]
date: 2018-09-25 20:30:08
categories: Course
description: The Note of AI Course
image:
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvmrp426maj212w0m816v.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Game Tree(2-player, deterministic, turns)

![](http://ww1.sinaimg.cn/large/cf684029ly1fvutmwlzmuj20gf0atwf1.jpg)

## Minimax Algorithm

#### Concept

Perfect play for deterministic, perfect-information games

Idea: choose move to position with highest minimax value => best achievable payoff against best play

![](http://ww1.sinaimg.cn/large/cf684029ly1fvutqhdjr6j20ko07zq38.jpg)

#### Code
```
function MINIMAX-DECISION(state) returns an action
    inputs: state, currrent state in game
    return the a in ACTIONS(state) maximizing MIN-VALUE(RESULT(a.state))
```
```
function MAX-VALUE(state) returns a utility value
    if TERMINAL-TEST(state) then return UTILITY(state)
    v <- -infinity
    for a.s in SUCCESSION(state) do v <- MAX(v, MIN-VALUE(s))
    return v
```
```
function MIN-VALUE(state) returns a utility value
    if TERMINAL-TEST(state) then return UTILITY(state)
    v <- infinity
    for a.s in SUCCESSION(state) do v <- MIN(v, MAX-VALUE(s))
    return v
```

#### Properties of minimax

Complete: Yes, if the tree is finite

Optimal: Yes, against an optimal oppoent.

Time complexity: O(b^m)

Space complexity: O(bm)

**If we explore every path, the algorithm will run for a lot of time, so it's necessary to reduce searching-width(d) or searching-depth(m)**

## Reduce searching-width(d): Alpha-Beta purning

#### Concept

![](http://ww1.sinaimg.cn/large/cf684029ly1fvuu3g4qdxj20l10e7aax.jpg)

#### Code
```
function ALPHA-BETA-DECISION(state) returns an action
    return the a in ACTIONS(state) maximizing MIN-VALUE(RESULT(a,state))
```
```
function MAX-VALUE(state,a,b) returns a utility value
    inputs: state, current state in game
            a, the value of the best alternative for MAX along the path to state
            b, the value of the best alternative for MIN along the path to state
    IF TERMINAL-TEST(state) then return UTILITY(state)
    v <- -infinity
    for x.s in SUCCESSORS(state) do
        v <- MAX(v, MIN-VALUE(s,a,b))
        if v >= b then return v
        a <- MAX(a, v)
    return v
```
```
function MIN-VALUE(state,a,b) returns a utility value
    same as MAX-VALUE but with roles of a,b reversed
```

#### Properties of Alpha-Beta

Pruning **does not** affect final result

Good move ordering improvres effectiveness of pruning

With "perfect ordering" time complexity == O(b^(m/2))  => doubles solvable depth

## Reduce searching-depth(m): Evaluation functions

An evaluation function returns an estimate of the expected utility of the game from a given position, just as the heuristic functions.

![](http://ww1.sinaimg.cn/large/cf684029ly1fvuuqw60gwj20k803rmxi.jpg)

## Stochatic games

#### Schematic game tree
![](http://ww1.sinaimg.cn/large/cf684029ly1fvuutlwbyxj20hr0cmmxr.jpg)

#### Process Formula
![](http://ww1.sinaimg.cn/large/cf684029ly1fvuuuer7pdj20lx05rjsa.jpg)

#### Example

![](http://ww1.sinaimg.cn/large/cf684029ly1fvuuxeh3gsj20l6097jrq.jpg)

<hr />