---
title: 6-Logical Agents
tags: [AI, Course Note, Algorithm, Logical Agents, Forward chaining, Backward chaining]
date: 2018-10-20 20:29:23
categories: Course
description: The Note of AI Course
mathjax: true
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fwflggtwdmj212w0m8drl.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Knowledge-based agents

**Knowledge base** = set of sentences in a formal language

### Basic actions:Ask/Tell
* A knowledge base keeps track of things
* we can **TELL** it facts and **ASK** for inference

### At every step:
* Construct a sentence with assertion about percepts
* Construct a sentence asking what action is next
* Construct a sentence asserting that action

## Logic in general

### Basic concepts

**Logics** are formal languages for representing information such that conclusions can be drawn

**Syntax** defines the sentences in the language

**Semantics** define the “meaning” of sentences, i.e., define truth of a sentence in a world

![2](http://ww1.sinaimg.cn/large/cf684029ly1fy1j1yuolcj20gt05awf3.jpg)

### Entailment

Entailment means that one thing follows from another: $KB$ |= $\alpha$

Knowledge base KB entails sentence α if and only if where KB is true, α is also true

Entailment is a relationship between sentences (i.e., syntax) that is based on semantics

### Models

Logicians typically think in terms of models, which are formally structured worlds with respect to which truth can be evaluated, which means models describe possible worlds. 

We say m is a model of a sentence α if α is true in m

$M(α)$ is the set of all models of $α$

$KB$ |= $α$, if and only if $M(KB) \subseteq M(α)$ 

## Logical equivalence

Two sentences are logically equivalent iff true in same models:

$α ≡ β$ if and only if $α$ |= $β$ and $β$ |= $α$

![](http://ww1.sinaimg.cn/large/cf684029ly1fwfmmc64l4j20ge08bq4f.jpg)

## Validity and satisfiability

**Validity**: it is true in all models

**Deduction**: $α$ |= $β$ iff $α \Rightarrow β$

**Satisfiability**: if some model makes it true

**Unsatisfiable:** if it is true in no models

## Inference: Forward chaining & Backward chaining

### Horn Form
* KB conjunction of Horn clauses
* Horn Clause(at most one literal is Positive)
* For examples: $（¬ P \bigvee ¬Q\bigvee V)$ is a Horn Clause
* so is $(¬ P \bigvee ¬ Q)$, but $(¬P \bigvee Q\bigvee V)$ is not
* Definite Clauses: exactly one literal is positive
* Horn Clauses can be re-written as implications:
    * proposition symbol(fact) or
    * conjunction of symbols (body or premise) $\Rightarrow$ symbol(head)
    * Examples: $(¬ C \bigvee ¬ B \bigvee A)$ becomes $(C\bigwedge B \Rightarrow A)$, because $(\alpha \Rightarrow \beta \equiv (¬ \alpha \bigvee \beta))$

### Video about the process of FC and BC
<iframe width="90%" height="480" src="https://www.youtube.com/embed/EZJs6w2YFRM" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Resolution

### CNF

conjunction of **disjunctions of literals**(clauses)

E.g., $(A ∨ ¬B) ∧ (B ∨ ¬C ∨ ¬D)$

[More details about CNF in wiki](https://zh.wikipedia.org/wiki/%E5%90%88%E5%8F%96%E8%8C%83%E5%BC%8F)

### Resolution Algorithm

Proof by contradiction, i.e., show $KB ∧ ¬α$ unsatisfiable to prove $KB$ |= $α$ satisfiable

### Video about the process of the resolution algorithm

<iframe width="90%" height="480" src="https://www.youtube.com/embed/PMm5Mat0MRA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

<hr />