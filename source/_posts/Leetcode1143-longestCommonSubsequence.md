---
title: Leetcode1143-longestCommonSubsequence
categories: leetcode
tags: [DP, Recursion]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 23:23:28
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

If there is no common subsequence, return 0.

## Example

**Example 1:**
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```
**Example 2:**
```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```
**Example 3:**
```
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```
**Constraints:**

* 1 <= text1.length <= 1000
* 1 <= text2.length <= 1000
* The input strings consist of lowercase English characters only.

## Solution
**Solution 1:** DP

$$ init: dp[i][0] = dp[0][j] = 0; (0 <= i < s1.length(), 0 <= j < s2.length()) $$
$$ dp[i][j] = dp[i-1][j-1] + 1; (s1[i] = s2[j]) $$
$$ dp[i][j] = max(dp[i-1][j], dp[i][j-1] ) $$
$$ res = dp[s1.length()][s2.length()] $$
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        if (text1.length() == 0 || text2.length() == 0) return 0;
        int[][] dp = new int[text1.length() + 1][text2.length() + 1];
        for (int i = 1; i <= text1.length(); i++){
            for (int j = 1; j <= text2.length(); j++){
                if (text1.charAt(i-1) == text2.charAt(j-1)) dp[i][j] = dp[i-1][j-1] + 1;
                else dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
            }
        }
        return dp[text1.length()][text2.length()];
    }
}
```

**Solution 2:** Recursion with memory
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        return helper(text1, 0, text2, 0, new int[text1.length()][text2.length()]);
    }
    private int helper(String s1, int index1, String s2, int index2, int[][] memory){
        if (index1 >= s1.length() || index2 >= s2.length()) return 0;
        if (memory[index1][index2] > 0) return memory[index1][index2] - 1;
        
        if (s1.charAt(index1) == s2.charAt(index2))
            return helper(s1, index1 + 1, s2, index2 + 1, memory) + 1;
        else {
            memory[index1][index2] = Math.max(helper(s1, index1 + 1, s2, index2, memory), helper(s1, index1, s2, index2 + 1, memory));
            memory[index1][index2]++;
            return memory[index1][index2]-1;
        }
    }
}
```

<hr />