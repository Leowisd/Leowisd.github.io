---
title: Leetcode097-interleavingString
categories: leetcode
tags: [DP, String, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 18:04:12
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

## Example
**Example 1:**
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
```
**Example 2:**
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
```
## Solution
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        
        boolean[][] dp = new boolean[s1.length() + 1][s2.length() + 1];
        dp[0][0] = true;
        for (int i = 1; i <= s2.length(); i++){
            dp[0][i] = dp[0][i-1] && (s2.charAt(i-1) == s3.charAt(i-1));
        }
        for (int i = 1; i <= s1.length(); i++){
            dp[i][0] = dp[i-1][0] && (s1.charAt(i-1) == s3.charAt(i-1));
        }
        for (int i = 1; i <= s1.length(); i++){
            for (int j = 1; j <= s2.length(); j++){
                dp[i][j] = (dp[i-1][j] && (s1.charAt(i-1) == s3.charAt(i + j -1)))
                    ||(dp[i][j-1] && (s2.charAt(j-1) == s3.charAt(i + j-1)));
            }
        }
        return dp[s1.length()][s2.length()];
    }
}
```

<hr />