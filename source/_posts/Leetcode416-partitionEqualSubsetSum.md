---
title: Leetcode416-partitionEqualSubsetSum
categories: leetcode
tags: [DP, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 16:23:54
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note**:

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

## Example
**Example 1:**
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

## Solution

**Solution 1:** DFS, but a little cheat, cannot be standard method
```java
class Solution {
    public boolean canPartition(int[] nums) {
        if (nums.length == 0) return false;
        int sum = 0;
        for (int num: nums){
            sum += num;
        }
        if (sum % 2 != 0) return false;
        boolean[] visited = new boolean[nums.length];
        Arrays.sort(nums);
        if (nums[nums.length - 1] > (sum / 2)) return false;
        return helper(nums, sum / 2, 0, visited, nums.length - 1, 2);
    }
    private boolean helper(int[] nums, int target, int sum, boolean[] visited, int start, int round){
        if (round == 0) return true;
        if (sum == target && helper(nums, target, 0, visited, nums.length - 1, round-1)) return true;
        for (int i = start; i >= 0; i--){
            if (!visited[i] && sum + nums[i] <= target){
                visited[i] = true;
                if (helper(nums, target, sum + nums[i], visited, start - 1, round))
                    return true;
                visited[i] = false;
            }
        }
        return false;
    }
}
```

**Solution 2:** DP

Actually, this is a 0/1 knapsack problem, for each number, we can pick it or not. Let us assume dp[i][j] means whether the specific sum j can be gotten from the first i numbers. If we can pick such a series of numbers from 0-i whose sum is j, dp[i][j] is true, otherwise it is false.

Base case: dp[0][0] is true; (zero number consists of sum 0 is true)

Transition function: For each number, if we don't pick it, dp[i][j] = dp[i-1][j], which means if the first i-1 elements has made it to j, dp[i][j] would also make it to j (we can just ignore nums[i]). If we pick nums[i]. dp[i][j] = dp[i-1][j-nums[i]], which represents that j is composed of the current value nums[i] and the remaining composed of other previous numbers. Thus, the transition function is dp[i][j] = dp[i-1][j] || dp[i-1][j-nums[i]]

```java
class Solution {
    public boolean canPartition(int[] nums){
        if (nums == null || nums.length == 0) return false;
        int sum = 0;
        for (int num: nums) sum += num;
        if (sum % 2 != 0) return false;
        sum /= 2;
        boolean[][] dp = new boolean[nums.length + 1][sum + 1];
        dp[0][0] = true;
        for (int i = 1; i < nums.length + 1; i++) dp[i][0] = true;
        for (int i = 1; i < sum + 1; i++) dp[0][i] = false;
        for (int i = 1; i < nums.length + 1; i++)
            for (int j = 1; j < sum + 1; j++){
                dp[i][j] = dp[i-1][j];
                if (j >= nums[i-1]){
                    dp[i][j] = dp[i][j] || dp[i-1][j-nums[i-1]];
                }
            }
        return dp[nums.length][sum];
    }
}
```

**Solution 3**: DP, space optimized
```java
class Solution {
    public boolean canPartition(int[] nums){
        if (nums == null || nums.length == 0) return false;
        int sum = 0;
        for (int num: nums) sum += num;
        if (sum % 2 != 0) return false;
        sum /= 2;
        boolean[] dp = new boolean[sum + 1];
        dp[0] = true;
        for (int num: nums)
            for (int j = sum; j >= num; j--){
                dp[j] = dp[j] || dp[j-num];
            }
        return dp[sum];
    }
}
```
<hr />