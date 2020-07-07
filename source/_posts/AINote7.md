---
title: 7-First Order Logic
tags: [AI, Course Note, Algorithm, FOL, First Order Logic]
mathjax: true
date: 2018-11-12 21:18:04
categories: Course
description: The Note of AI Course
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fx69s00ej5j20ad06mdgf.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## First Order Logic: Formal/Natural Languages

Whereas propositional logic assumes world contains **facts**, fitst-order logic(like natural language) assumes the world contains.

* Objects: people, houses, numbers, theories ...
* Relations: red, round, bogus ..., brother of, bigger than, inside ...
* Functions: father of, best friend, end of ...

## Syntax of FOL

### Basic elements

* Constants: KingJohn, 2, UCB...
* Predicates: Brother, >, ...
* Functions: Sqrt, LeftLegOf, ...
* Variables: x, y, a, b...
* Connectives: $\bigvee, \bigwedge, \Rightarrow$
* Equality: $=$
* Quantifiers: $\forall, \exists$

### More on Syntax

* Three kinds of symbols
    * Constant: objects
    * Predicate: relations
    * Function: functions (i.e. can return values other than truth vals)
* Predicate and Function have **arity**.
* Symbols have an interpretation.
* **Terms**: $function(term_1 ,..., term_n)$ or constant or variable, i.e. $LeftLeg(John)$
* **Atomic Sentences** state facts: $predicate(term_1,...,term_n)$ or $term_1 = term_2$, i.e. $Brother(Richard, John)$
* **Complex Sentences**: $Brother(R,J) \bigwedge Brother(J,R)$
* **Universal Quantifiers**: $\forall (variable) (sentence)$, i.e. $\forall King(x) \Rightarrow Person(x)$
    * **A common mistake to avoid**: 
        * Typically, $\Rightarrow$ is the main connective with $\forall$. 
        *  Common mistake: using $\bigwedge$ as the main connective with $\forall$: $$\forall x At(Berkeley) \bigwedge Smart(x)$$ means "Everyone is at Berkeley and everyone is smart", not "Everyone at Berkeley is smart", which should to be $$\forall x At(x, Berkeley) \Rightarrow Smart(x)$$
* **Existential Quantifiers**: $\exists <variable> <sentence>$, i.e. $\exists Crown(x) \bigwedge OnHead(x,John)$
    * **A common mistake to avoid**:
        * Typically, $\bigwedge$ is the main connective with $\exists$.
        * Common mistake: using $\Rightarrow$ as the main connective with $\exists$: $$\exists x At(x, Standford) \Rightarrow Smart(x)$$ is true even if there is anyone who is at Stanford! The correct one is $$\exists x At(x, Standford) \bigwedge Smart(x)$$

#### Properties of quantifiers

* $\forall x \forall y$ is the same as $\forall y \forall x$
* $\exists x \exists y$ is the same as $\exists x \exists y$
* $\exists x \forall y$ is **not** the same as $\forall x \exists y$

#### Equality 

$term_1 = term_2$ is true under a given interpretation if and only if $term_1$ and $term_2$ refer to the same object.

E.g. $1=2$ and $\forall xMutiple(Sqrt(x), Sqrt(x)) = x$ are satisfiable, $2=2$ is vaild.
<hr />