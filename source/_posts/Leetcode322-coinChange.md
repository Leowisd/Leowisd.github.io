---
title: Leetcode322-coinChange
categories: leetcode
tags: [DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 16:31:28
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

## Example
**Example 1:**
```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```
**Example 2:**
```
Input: coins = [2], amount = 3
Output: -1
```
**Note:**

You may assume that you have an infinite number of each kind of coin.

## Solution

**Solution 1:** DP, faster
```java
class Solution {
    public int coinChange(int[] coins, int amount){
        if (coins == null || coins.length == 0) return -1;
        if (amount == 0) return 0;
        int[] dp = new int[amount + 1];
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) dp[i] = Integer.MAX_VALUE;
        for (int i = 1; i <= amount; i++)
            for (int coin: coins){
                if (coin <= i && dp[i - coin] != Integer.MAX_VALUE)
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        return (dp[amount] == Integer.MAX_VALUE) ? -1 : dp[amount];       
    }
}
```

Solution 2: Recursion
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) return -1;
        if (amount == 0) return 0;
        return helper(coins, amount, new int[amount]);
    }
    private int helper(int[] coins, int remain, int[] count){
        if (remain == 0) return 0;
        if (remain < 0) return -1;
        if (count[remain - 1] != 0) return count[remain - 1];
        int min = Integer.MAX_VALUE;
        for (int coin: coins){
            int temp = helper(coins, remain - coin, count);
            if (temp >= 0 && temp < min)
                min = temp + 1;
        }
        if (min == Integer.MAX_VALUE) count[remain - 1] = -1;
        else count[remain - 1] = min;
        return count[remain - 1];
    }
}
```

<hr />