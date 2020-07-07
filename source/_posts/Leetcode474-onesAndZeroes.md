---
title: Leetcode474-onesAndZeroes
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 21:03:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Share
In the computer world, use restricted resource you have to generate maximum benefit is what we always want to pursue.

For now, suppose you are a dominator of m 0s and n 1s respectively. On the other hand, there is an array with strings consisting of only 0s and 1s.

Now your task is to find the maximum number of strings that you can form with given m 0s and n 1s. Each 0 and 1 can be used at most once.

Note:

1. The given numbers of 0s and 1s will both not exceed 100
2. The size of given string array won't exceed 600.

## Example
**Example 1:**
```
Input: Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3
Output: 4

Explanation: This are totally 4 strings can be formed by the using of 5 0s and 3 1s, which are “10,”0001”,”1”,”0”
```

**Example 2:**
```
Input: Array = {"10", "0", "1"}, m = 1, n = 1
Output: 2

Explanation: You could form "10", but then you'd have nothing left. Better form "0" and "1".
```

## Solution

0-1 Backpack, dp[k][i][j] -----> dp[i][j]

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][] dp = new int[m + 1][n + 1];
        for (String str: strs){
            int[] count = helper(str);
            for (int i = m; i >= count[0]; i--){
                for (int j = n; j >= count[1]; j--){
                    dp[i][j] = Math.max(dp[i][j], dp[i - count[0]][j - count[1]] + 1);
                }
            }
        }
        return dp[m][n];
    }
    private int[] helper(String str){
        int[] res = new int[2];
        for (char ch: str.toCharArray()){
            if (ch == '0') res[0]++;
            else res[1]++;
        }
        return res;
    }
}
```

<hr />