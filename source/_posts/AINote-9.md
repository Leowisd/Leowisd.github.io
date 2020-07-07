---
title: 9-Machine Learning
tags: [AI, Course Note, Machine Leraning, decision tree, linear regression, neural networks]
mathjax: true
date: 2018-12-08 11:01:44
categories: Course
description: The Note of AI Course
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fy042z90m9j212w0m8134.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->
## Learning agents

Design of a learning element is affected by
* Which components of the performance element are to be learned
* What feedback is available to learn these components
* What representation is used for the components

Type of feedback:
* **Supervised learning**: correct answers for each example
* **Unsupervised learning**: correct answers not given
* **Reinforcement learning**: occasional rewards

## Inductive learning

Simplest form: learn a function from examples

$f$ is the **target function**

An example is a pair $(x,f(x))$

Problem: find a **hypothesis** h
* such that $h \approx f$
* given a **training set** of examples

(This is a highly simplified model of real learning:
* Ignores prior knowledge
* Assumes examples are given)

## Decision tree learning

One possible representation for hypotheses

E.g., here is the "true" tree for deciding whether to wait:

![](http://ww1.sinaimg.cn/large/cf684029ly1fxzuinv5czj20dx08oq3p.jpg)

### Expressiveness

Decision trees can express any function of the input attributes.

E.g., for Boolean functions, truth table row → path to leaf:

![](http://ww1.sinaimg.cn/large/cf684029ly1fxzukg8b67j20fb04z74e.jpg)

There is another example:

![4](http://ww1.sinaimg.cn/large/cf684029ly1fy02ruj2k3j20nm0dxn0x.jpg)

### Hypothesis spaces

How many distinct decision trees with n Boolean attributes?

= number of Boolean functions

= number of distinct truth tables with $2^n$ rows = $2^{2^n}$

### Decision tree learning algorithm

Aim: find a small tree consostent with the training examples

Idea: (recurisvely) choose "most significant" attribute as root of (sub)tree

![](http://ww1.sinaimg.cn/large/cf684029ly1fxzuoap2e4j20fq07qabg.jpg)

#### Choosing an attribute

Idea: a good attribute splits the examples into subsets that are (idealy) "all positive" or "all negative"

#### Using information theory

To implement Choose-Attribute in the DTL algorithm

Information Content(Entropy)

$$I(P(v_1),...,P(v_n)) = \sum_{i=1}^n -P(v_i)log_2P(v_i)$$

For a training set containing p positive examples and n negative examples:

![5](http://ww1.sinaimg.cn/large/cf684029ly1fy04e8ejmuj20c101rjr9.jpg)

#### Information gain

A chosen attribute A divides the training set E into subsets $E_1, … , E_v$ according to their values for A, where A has $v$ distinct values.

![6](http://ww1.sinaimg.cn/large/cf684029ly1fy04fpipfwj20c601m748.jpg)

Information Gain (IG) or reduction in entropy from the attribute test:

![7](http://ww1.sinaimg.cn/large/cf684029ly1fy04g94s5nj20bj01hjrc.jpg)

It's same as 

![8](http://ww1.sinaimg.cn/large/cf684029ly1fy04hopy9gj20f602dq3h.jpg)

<iframe width="90%" height="480" src="https://www.youtube.com/embed/eLlYSpVjH94" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Neural Networks

<iframe width="90%" height="480" src="https://www.youtube.com/embed/A6UCSkOut7U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr />
