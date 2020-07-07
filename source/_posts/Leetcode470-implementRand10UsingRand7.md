---
title: Leetcode470-implementRand10UsingRand7
categories: leetcode
tags: [Random, Rejection Sampling, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 15:45:57
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a function rand7 which generates a uniform random integer in the range 1 to 7, write a function rand10 which generates a uniform random integer in the range 1 to 10.

Do NOT use system's Math.random().

## Example
**Example 1:**
```
Input: 1
Output: [7]
```
**Example 2:**
```
Input: 2
Output: [8,4]
```
**Example 3:**
```
Input: 3
Output: [8,1,10]
```

**Note:**
1. rand7 is predefined.
2. Each testcase has one argument: n, the number of times that rand10 is called.

**Follow up:**
1. What is the expected value for the number of calls to rand7() function?
2. Could you minimize the number of calls to rand7()?

## Solution
```java
/**
 * The rand7() API is already defined in the parent class SolBase.
 * public int rand7();
 * @return a random integer in the range 1 to 7
 */
class Solution extends SolBase {
//      rand7() -> rand49() -> rand40() -> rand10()
    public int rand10() {
        int result = 40;
        while (result >= 40) {result = 7 * (rand7() - 1) + (rand7() - 1);}
        return result % 10 + 1;
    }
}

// Implement rand11() using rand3():
// Idea: rand3() -> rand27() -> rand22 -> rand11
// public int rand11() {
//     int result = 22;
//     while (result >= 22) {result = 3 * 3 * (rand3() - 1) + 3 * (rand3() - 1) + (rand3() - 1);}
//     return result % 11 + 1;
// }
```

<hr />