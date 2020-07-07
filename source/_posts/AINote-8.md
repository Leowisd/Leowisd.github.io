---
title: 8-Uncertainty
tags: [AI, Course Note, Probability, Independence]
mathjax: true
date: 2018-12-08 08:44:27
categories: Course
description: The Note of AI Course
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fxzq5xephoj212w0m878l.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Conditional probability

Definition of conditional probability:

$$ P(a|b) = {P(a \bigwedge b) \over P(b)}$$

**Product rule** gives an alternative formulation:

$$ P(a \bigwedge b) = P(a|b)P(b) = P(b|a)P(a)$$

**Chain rule** is derived by successive application of product rule:

$$P(X_1,...,X_n)=P(X_1,...,X_{n-1})P(X_n|X_1,...,X_{n-1})=...=\prod_{i=1}^nP(X_i|X_1,...,X_{i-1})$$

## Independence

A and B are independent iff

$P(A|B)=P(A)$ or $P(B|A)=P(B)$ or $P(A,B)=P(A)P(B)$

## Conditional independence 

$$P(Toothache,Catch|Cavity) = P(Toothache|Cavity)P(Catch|Cavity)$$

Conditional independence is our most basic and robust form of knowledge about uncertain environments.

## Bayes' Rule

$$P(a|b)={P(b|a)P(a) \over P(b)}$$

<hr />