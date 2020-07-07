---
title: 3-Local search algorithms
tags: [AI, Course Note, Algorithm, Search, Hill Climbing, Simulated annealing, Local beam search, Genetic Algorithms]
date: 2018-09-17 18:19:42
categories: Course
description: The Note of AI Course
image:
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvdcczwxmlj212w0m8n0c.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Hill Climbing 

_"Like climbing Everest in thick fog with amnesia"_

```
function HILL-CLIMBING(problem) returns a state that is a local maximum
    inputs: problem, a problem
    local variables: current, a node
                     neighbor, a node
    current <- MAKE-NODE(INITIAL-STATE[problem])
    loop do
        neighbor <- a highest-valued successor of current
        if VALUE[neighbor] <= VALUE[current] then return STATE[current]
        current <- neighbor
    end
```

Random-restart hill climbing overcomes local maxima--trivially complete

Random sideways moves escape from shoulders loop on flat maxima 

## Simulated annealing

Idea: escape local maxima by allowing some "bad" moves

but gradually decrease their size and frequency

```
function SIMULATED-ANNEALING(problem, schedule) returns a solution state
    inputs: problem, a problem
            schedule, a mapping from time to "temperature"
    local variables: current, a node
                     next, a node
                     T1 a "temperature" controlling prob. of downward steps
    current <- MAKE-NODE(INITIAL-STATE[problem])
    for t <- 1 to infinity do
        T <- schedule[t]
        if T=0 then return current
        next <- a randomly selected successor of current
        disE <- VALUE[next] - VALUE[current]
        if disE>0 then current <- next
        else current <- next only with probability e^(disE/T)
```

## Local beam Search

Idea: keep k states instead of 1; choose top k of all their successors

Not the same as k searches run in parallel!

Searches that find good states recruit other searches to join them

Problem: quite often, all k states end up on same local hill

Idea: choose k successors randomly, biased towards good ones

Observe the close analogy to native selection!

## Genetic Algorithms

= stochastic local beam search + generate successors from pairs of states

```
function GENETIC-ALGORITHM(population, FITNESS-FN) returns an individual
    inputs: population, a set of individuals
            FITNESS-FN: a function that measures the fitness of an individual
    repeat
        new.population <- empty set
        for i= 1 to SIZE(population) do
            x <- RANDOM-SELECTION(population, FITNESS-FN)
            y <- RANDOM-SELECTION(population, FITNESS-FN)
            child <- REPRODUCE(x,y)
            if (small random probability) then child <- MUTATE(child)
            add child to new_population
        population = new_population
    until some individual is fit enough, or enough time has clapsed
    return the best individual in population, according to FITNESS-FN

function REPRODUCE(x,y) returns an individual
    inputs: x,y, parent individuals

    n <- LENGTH(x); c<- random number from 1 to n
    return APPEND(SUBSTRING(x,1,c), SUBSTRING(y, c+1, n))
```

<hr />