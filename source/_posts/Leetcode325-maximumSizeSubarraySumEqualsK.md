---
title: Leetcode325-maximumSizeSubarraySumEqualsK
categories: leetcode
tags: [Array, Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-26 00:28:33
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

**Note:**
The sum of the entire nums array is guaranteed to fit within the 32-bit signed integer range.

## Example
**Example 1:**
```
Input: nums = [1, -1, 5, -2, 3], k = 3
Output: 4 
Explanation: The subarray [1, -1, 5, -2] sums to 3 and is the longest.
```
**Example 2:**
```
Input: nums = [-2, -1, 2, 1], k = 1
Output: 2 
Explanation: The subarray [-1, 2] sums to 1 and is the longest.
```

**Follow Up:**
Can you do it in O(n) time?

## Solution
```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int sum = 0;
        int res = 0;
        for (int i = 0; i < nums.length; i++){
            sum += nums[i];
            if (sum == k) res = i + 1;
            else if (map.containsKey(sum - k))
                res = Math.max(res, i - map.get(sum - k));
            if (!map.containsKey(sum)) map.put(sum, i);    
        }
        return res;
    }
}
```

<hr />