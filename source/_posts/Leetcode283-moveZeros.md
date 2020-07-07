---
title: Leetcode283-moveZeros
categories: leetcode
tags: [Array, Two Pointers, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 12:23:54
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

## Example
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note:**

* You must do this in-place without making a copy of the array.
* Minimize the total number of operations.

## Solution
```java
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length <= 1) return;
        
        int pos = 0;
        for (int num: nums){
            if (num != 0)
                nums[pos++] = num;
        }
        while(pos < nums.length)
            nums[pos++] = 0;
    }
```

<hr />