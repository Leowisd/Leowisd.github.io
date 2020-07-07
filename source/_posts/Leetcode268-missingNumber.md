---
title: Leetcode268-missingNumber
categories: leetcode
tags: [Array, Math, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 16:21:17
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

## Example
**Example 1:**
```
Input: [3,0,1]
Output: 2
```
**Example 2:**
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```
## Solution
```java
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int sum = (n)*(n+1)/2;
        int sum2 = 0;
        for (int it: nums) sum2+=it;
        return sum - sum2;
        
        // // Method 2: XOR
        // int res = 0, i;
        // for (i = 0; i< nums.length;i++){
        //     res = res ^ i ^ nums[i];
        // }
        // return res ^ i;
    }
}
```

<hr />