---
title: Leetcode041-firstMissingPositive
categories: leetcode
tags: [Array, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 12:08:46
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an unsorted integer array, find the smallest missing positive integer.

## Example
**Example 1:**
```
Input: [1,2,0]
Output: 3
```
**Example 2:**
```
Input: [3,4,-1,1]
Output: 2
```
**Example 3:**
```
Input: [7,8,9,11,12]
Output: 1
```

**Note:**

Your algorithm should run in O(n) time and uses constant extra space.

## Solution
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        if (nums == null || nums.length == 0) return 1;
        
        int i = 0;
        // If the current value is in the range of (0,length) and it's not at its correct position, 
        // swap it to its correct position.
        // Else just continue;
        while (i < nums.length){
            if (nums[i] == i + 1 || nums[i] <= 0 || nums[i] > nums.length || nums[i] == nums[nums[i] - 1]) i++;
            else swap(nums, i, nums[i] - 1);
        }
        for (i = 0; i < nums.length; i++)
            if (nums[i] != i + 1) break;
        return i+1;
    }
    
    private void swap(int[] nums, int x, int y){
        int tmp = nums[x];
        nums[x] = nums[y];
        nums[y] = tmp;
    }
}
```

<hr />