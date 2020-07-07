---
title: Leetcode697-degreeofArray
categories: leetcode
tags: [Array, Hash Table, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 16:18:26
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

## Example
**Example 1:**
```
Input: [1, 2, 2, 3, 1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```
**Example 2:**
```
Input: [1,2,2,3,1,4,2]
Output: 6
```

**Note:**
nums.length will be between 1 and 50,000.
nums[i] will be an integer between 0 and 49,999.

## Solution
```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        HashMap<Integer, Integer> freq = new HashMap<>();
        HashMap<Integer, Integer> index = new HashMap<>();
        int maxFreq = -1;
        for (int i = 0; i < nums.length; i++){
            freq.put(nums[i], freq.getOrDefault(nums[i], 0) + 1);
            maxFreq = Math.max(freq.get(nums[i]), maxFreq);
            index.put(nums[i], i);
        }
        int res = nums.length;
        for (int i = 0; i < nums.length; i++){
            if (freq.containsKey(nums[i]) && freq.get(nums[i]) == maxFreq){
                res = Math.min(res, index.get(nums[i]) - i + 1);
                freq.remove(nums[i]);
            }
        }
        return res;
    }
}

```

<hr />