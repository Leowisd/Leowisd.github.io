---
title: Leetcode089-grayCode
categories: leetcode
tags: []
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-08 00:18:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

## Example
**Example 1:**
```
Input: 2
Output: [0,1,3,2]
Explanation:
00 - 0
01 - 1
11 - 3
10 - 2

For a given n, a gray code sequence may not be uniquely defined.
For example, [0,2,3,1] is also a valid gray code sequence.

00 - 0
10 - 2
11 - 3
01 - 1
```
**Example 2:**
```
Input: 0
Output: [0]
Explanation: We define the gray code sequence to begin with 0.
             A gray code sequence of n has size = 2n, which for n = 0 the size is 20 = 1.
             Therefore, for n = 0 the gray code sequence is [0].
```
## Solution
```java
class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> res = new ArrayList<>();
        res.add(0);
        if (n  == 0) return res;
        res.add(1);
        if (n == 1) return res;
        for (int i = 2; i <= n; i++){
            for (int j = res.size()-1; j >= 0; j--){
                res.add(res.get(j) + (1 << (i - 1)));
            }
        }
        return res;
    }
}
```

<hr />