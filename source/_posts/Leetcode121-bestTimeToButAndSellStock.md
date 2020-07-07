---
title: Leetcode121-bestTimeToButAndSellStock
categories: leetcode
tags: [Array, DP, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 09:56:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Say you have an array for which the $i^{th}$ element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

## Example
**Example 1:**
```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```
**Example 2:**
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```
## Solution
O(N) normal solution
```java
class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        if (prices == null || prices.length == 0) return res;
        
        int buy = prices[0];
        int sell = Integer.MIN_VALUE;
        
        for (int i = 1; i < prices.length; i++){
            if (prices[i] < buy){
                res = Math.max(res, sell - buy);
                buy  = prices[i];
                sell = Integer.MIN_VALUE;
            }
            else if (prices[i] > sell){
                sell = prices[i];
            }
        }
        res = Math.max(res, sell - buy);
        return res;
    }
}
```

O(N) DP solution
```java
class Solution{
    public int maxProfit(int[] prices) {
        int maxCur = 0, maxSoFar = 0;
        for(int i = 1; i < prices.length; i++) {
            maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
            maxSoFar = Math.max(maxCur, maxSoFar);
        }
        return maxSoFar;
    }
}
```
<hr />