---
title: Leetcode219-containsDuplicateII
categories: leetcode
tags: [Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 16:39:17
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

## Example
**Example 1**:
```
Input: nums = [1,2,3,1], k = 3
Output: true
```
**Example 2:**
```
Input: nums = [1,0,1,1], k = 1
Output: true
```
**Example 3:**
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```
## Solution
```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if (nums == null || nums.length == 0) return false;
        HashSet<Integer> set = new HashSet<>();
        
        for (int i = 0; i < nums.length; i++){
            if (i > k) set.remove(nums[i - k - 1]);
            if (!set.add(nums[i])) return true;
        }
        return false;
    }
}
```

<hr />