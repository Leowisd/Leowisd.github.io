---
title: Leetcode673-numberOfLongestIncreasingSubsequence
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 23:21:22
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an unsorted array of integers, find the number of longest increasing subsequence.


## Example
**Example 1:**
```
Input: [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```
**Example 2:**
```
Input: [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```
**Note:** Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.

## Solution
Add one array to record the number of each dp[i] 
```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int[] dp = new int[nums.length];
        int[] count = new int[nums.length];
        for (int i = 0; i < nums.length; i++){
            dp[i] = 1;
            count[i] = 1;
        }
        int maxLen = dp[0];
        int res = 0;
        for (int i = 1; i < nums.length; i++){
            for (int j = 0; j < i; j++){
                if (nums[j] < nums[i]){
                    if (dp[i] == dp[j] + 1) count[i] += count[j];
                    if (dp[i] < dp[j] + 1){
                        dp[i] = dp[j] + 1;
                        count[i] = count[j];
                    }
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }
        for(int i = 0; i < dp.length; i++)
            if (dp[i] == maxLen) res += count[i];
        return res;
    }
}
```

<hr />