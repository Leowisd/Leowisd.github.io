---
title: Leetcode516-longestPalindromicSubsequence
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 20:51:37
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

## Example
**Example 1:**

Input:
```
"bbbab"
```

Output:
```
4
```
One possible longest palindromic subsequence is "bbbb".

**Example 2:**

Input:
```
"cbbd"
```
Output:
```
2
```

One possible longest palindromic subsequence is "bb".

## Solution
```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        if (s.length() == 0) return 0;
        
        int[][] dp = new int[s.length()][s.length()];
        for (int i = 0; i < s.length(); i++)
            dp[i][i] = 1;
        
        for (int i = s.length() - 1; i >= 0; i--){
            for (int j = i + 1; j < s.length(); j++){
                if (s.charAt(i) == s.charAt(j))
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                else dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
            }
        }
        
        return dp[0][s.length() - 1];
    }
}
```

<hr />