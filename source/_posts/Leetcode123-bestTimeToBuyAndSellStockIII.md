---
title: Leetcode123-bestTimeToBuyAndSellStockIII
categories: leetcode
tags: [DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-10 19:00:11
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

## Example
**Example 1:**
```
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```
**Example 2:**
```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```
**Example 3:**
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

## Solution

**Solution 1: Basic DP, $O(kn^2)$**
```
f[k, i] represents the max profit up until prices[i] (Note: NOT ending with prices[i]) using at most k transactions. 
f[k, i] = Math.max(f[k, i - 1], prices[i] - prices[j] + f[k - 1, j])
        = Math.max(f[k, i - 1], prices[i] + Math.max(f[k - 1, j] - prices[j]))
f[0, i] = 0;
f[k, 0] = 0;
```
```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length <= 1) return 0;
        // int k = 2;
        int[][] dp = new int[3][prices.length];
        int res = Integer.MIN_VALUE;
        for (int k = 1; k <= 2; k++){
            int temp = dp[k - 1][0] - prices[0];
            for (int i = 1; i < prices.length; i++){
                dp[k][i] = Math.max(dp[k][i - 1], prices[i] + temp);
                res = Math.max(res, dp[k][i]);
                temp = Math.max(temp, dp[k - 1][i] - prices[i]);
            }
        }
        
        return res;
    }
}
```

**Solution 2: Improved DP, $O(kn)$**
```java
class Solution {
//     O(kn)
        public int maxProfit(int[] prices)  
        {
            if (prices.length == 0) return 0;
            int[] dp = new int[3];
            int[] min = new int[3];
            for (int i = 0; i < min.length; i++)
                min[i] = prices[0];
            for (int i = 1; i < prices.length; i++)  {
                for (int k = 1; k <= 2; k++) {
                    min[k] = Math.min(min[k], prices[i] - dp[k-1]);
                    dp[k] = Math.max(dp[k], prices[i] - min[k]);
                }
            }

            return dp[2];
        }
}
```

Space complex: $O(1)$

```java
class Solution {
        public int maxProfit(int[] prices)  
        {
            int buy1 = Integer.MAX_VALUE, buy2 = Integer.MAX_VALUE;
            int sell1 = 0, sell2 = 0;

            for (int i = 0; i < prices.length; i++) {
                buy1 = Math.min(buy1, prices[i]);
                sell1 = Math.max(sell1, prices[i] - buy1);
                buy2 = Math.min(buy2, prices[i] - sell1);
                sell2 = Math.max(sell2, prices[i] - buy2);
            }

            return sell2;
        }
}
```
<hr />