---
title: Leetcode560-subarraySumEqualsK
categories: leetcode
tags: [Array, Hash Table, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 17:22:49
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

## Example
```
Input:nums = [1,1,1], k = 2
Output: 2
```
**Note:**
1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

## Solution
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum = 0, result = 0;
        Map<Integer, Integer> preSum = new HashMap<>();
        preSum.put(0, 1);
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (preSum.containsKey(sum - k)) {
                result += preSum.get(sum - k);
            }
            preSum.put(sum, preSum.getOrDefault(sum, 0) + 1);
        }
        
        return result;
    }
}
```

<hr />