---
title: Leetcode050-pow(x,n)
categories: leetcode
tags: [Math, Recursion, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-12 22:14:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement _pow(x, n)_, which calculates _x_ raised to the power _n_ $(x^n)$.

## Example

**Example 1:**
```
Input: 2.00000, 10
Output: 1024.00000
```
**Example 2:**
```
Input: 2.10000, 3
Output: 9.26100
```
**Example 3:**
```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```
**Note:**
* -100.0 < x < 100.0
* n is a 32-bit signed integer, within the range [$−2^{31}$, $2^{31} − 1$]

## Solution
```java
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) return 1;
        
        if (n == Integer.MIN_VALUE){
            x *= x;
            n /= 2;
        }//beacuse Integer.MAX_VALUE = abs(Integer.MIN_VALUE)-1
        if (n < 0){
            n = -n;
            x = 1/x;
        }
        return (n % 2 == 0) ? myPow(x * x, n / 2) : x * myPow(x * x, n / 2); 
    }
}
```

<hr />