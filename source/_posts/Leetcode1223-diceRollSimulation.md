---
title: Leetcode1223-diceRollSimulation
categories: leetcode
tags: [DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 11:47:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A die simulator generates a random number from 1 to 6 for each roll. You introduced a constraint to the generator such that it cannot roll the number i more than rollMax[i] (1-indexed) consecutive times. 

Given an array of integers rollMax and an integer n, return the number of distinct sequences that can be obtained with exact n rolls.

Two sequences are considered different if at least one element differs from each other. Since the answer may be too large, return it modulo 10^9 + 7.

## Example
**Example 1:**
```
Input: n = 2, rollMax = [1,1,2,2,2,3]
Output: 34
Explanation: There will be 2 rolls of die, if there are no constraints on the die, there are 6 * 6 = 36 possible combinations. In this case, looking at rollMax array, the numbers 1 and 2 appear at most once consecutively, therefore sequences (1,1) and (2,2) cannot occur, so the final answer is 36-2 = 34.
```
**Example 2:**
```
Input: n = 2, rollMax = [1,1,1,1,1,1]
Output: 30
```
**Example 3:**
```
Input: n = 3, rollMax = [1,1,1,2,2,3]
Output: 181
```

## Solution
```java
class Solution {
    public int dieSimulator(int n, int[] rollMax) {
        int mod = (int)1e9 + 7;
        //dp[i][j] represents the number of distinct sequences that can be obtained when rolling i times and ending with j
        //The one more row represents the total sequences when rolling i times
        int[][] dp = new int[n + 1][7];
        for (int i = 0; i < 6; i++){
            dp[1][i] = 1;
        }
        dp[1][6] = 6;
        
        for (int i = 2; i <= n; i++){
            int total = 0;
            for (int j = 0; j < 6; j++){
                //If there are no constraints, the total sequences ending with j should be the total sequences from previous rolling
                dp[i][j] = dp[i-1][6];
                //For xx1, only 111 is not allowed, so we only need to remove 1 sequence from previous sum
                if (i - rollMax[j] == 1)
                    dp[i][j]--;
                //For axx1, we need to remove the number of a11 (211 + 311 + 411 + 511 + 611) => (..2 + ..3 + ..4 + ..5 + ..6) => (sum - ..1)
                if (i - rollMax[j] >= 2){
                    int reducation = dp[i - rollMax[j] - 1][6] - dp[i - rollMax[j] - 1][j];
                    //must add one more mod because subtraction may introduce negative numbers
                    dp[i][j] = ((dp[i][j] - reducation) % mod + mod) % mod;
                }
                total = (total + dp[i][j]) % mod;
            }
            dp[i][6] = total;
        }
        
        return dp[n][6];
    }
}
```

<hr />