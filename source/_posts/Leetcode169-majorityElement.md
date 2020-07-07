---
title: Leetcode169-majorityElement
categories: leetcode
tags: [Array]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:17:13
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

## Example
**Example 1:**
```
Input: [3,2,3]
Output: 3
```
**Example 2:**
```
Input: [2,2,1,1,1,2,2]
Output: 2
```

## Solution
```java
// Boyer-Moore Majority Algorithm
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = 0;
        int count = 0;
        for (int num : nums){
            if (count == 0)
                candidate = num;
            if (candidate == num)
                count++;
            else count--;
        }
        return candidate;
    }
}
```

<hr />