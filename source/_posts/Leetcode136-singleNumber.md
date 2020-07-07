---
title: Leetcode136-singleNumber
categories: leetcode
tags: [Hash Table, Bit Manipulation, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:30:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## Example
**Example 1:**
```
Input: [2,2,1]
Output: 1
```
**Example 2:**
```
Input: [4,1,2,1,2]
Output: 4
```

## Solution
```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num: nums) res = res ^ num;
        return res;
    }
}
```

<hr />