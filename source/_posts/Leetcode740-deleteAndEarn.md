---
title: Leetcode740-deleteAndEarn
categories: leetcode
tags: [DP, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 15:58:19
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums of integers, you can perform operations on the array.

In each operation, you pick any nums[i] and delete it to earn nums[i] points. After, you must delete every element equal to nums[i] - 1 or nums[i] + 1.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.

## Example
**Example 1:**
```
Input: nums = [3, 4, 2]
Output: 6
Explanation: 
Delete 4 to earn 4 points, consequently 3 is also deleted.
Then, delete 2 to earn 2 points. 6 total points are earned.
 ```

**Example 2:**
```
Input: nums = [2, 2, 3, 3, 3, 4]
Output: 9
Explanation: 
Delete 3 to earn 3 points, deleting both 2's and the 4.
Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
9 total points are earned.
```

## Solution
```java
class Solution {
    public int deleteAndEarn(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int[] count = new int[10001];
        int[] dp = new int[10001];
        
        for (int num: nums) count[num] += num;
        dp[1] = count[1];
        dp[2] = Math.max(dp[1], count[2]);
        for (int i = 3; i < 10001; i++){
            dp[i] = Math.max(dp[i-2] + count[i], dp[i-1]);
        }
        
        return dp[10000];
    }
}
```

<hr />