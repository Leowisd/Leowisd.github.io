---
title: Leetcode525-contiguousArray
categories: leetcode
tags: [Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:47:40
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

## Example
**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```
**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:** The length of the given binary array will not exceed 50,000.

## Solution
```java
//The idea is to change 0 in the original array to -1. Thus, if we find SUM[i, j] == 0 then we know there are even number of -1 and 1 between index i and j. Also put the sum to index mapping to a HashMap to make search faster

class Solution {
    public int findMaxLength(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        HashMap<Integer, Integer> map = new HashMap<>();
        int sum = 0;
        map.put(0, -1);
        
        int res = 0;
        for (int i = 0; i < nums.length; i++){
            sum += nums[i] == 0 ? -1 : 1;
            if (map.containsKey(sum)){
                res = Math.max(res, i - map.get(sum));
            }
            else map.put(sum, i);
        }
        
        return res;
    }
}
```

<hr />