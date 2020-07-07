---
title: Leetcode1092-shortestCommonSupersequence
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 20:48:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings str1 and str2, return the shortest string that has both str1 and str2 as subsequences.  If multiple answers exist, you may return any of them.

(A string S is a subsequence of string T if deleting some number of characters from T (possibly 0, and the characters are chosen anywhere from T) results in the string S.)

## Example
**Example 1:**
```
Input: str1 = "abac", str2 = "cab"
Output: "cabac"
Explanation: 
str1 = "abac" is a subsequence of "cabac" because we can delete the first "c".
str2 = "cab" is a subsequence of "cabac" because we can delete the last "ac".
The answer provided is the shortest such string that satisfies these properties.
```

**Note:**

1. 1 <= str1.length, str2.length <= 1000
2. str1 and str2 consist of lowercase English letters.

## Solution
```java
class Solution {
    public String shortestCommonSupersequence(String str1, String str2) {
        int[][] dp = new int[str1.length() + 1][str2.length() + 1];
        for (int i = 0; i <= str1.length(); i++) dp[i][0] = i;
        for (int j = 0; j <= str2.length(); j++) dp[0][j] = j;
        
        for (int i = 1; i <= str1.length(); i++){
            for (int j = 1; j <= str2.length(); j++){
                if (str1.charAt(i - 1) == str2.charAt(j - 1))
                    dp[i][j] = dp[i-1][j-1] + 1;
                else dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + 1;
            }
        }
        
        int minimum = dp[str1.length()][str2.length()];
        int i = str1.length();
        int j = str2.length();
        String res = "";
        while(i > 0 && j > 0){
            if(str1.charAt(i - 1) == str2.charAt(j - 1)){
                res = str1.charAt(i - 1) + res;
                i--;
                j--;
            }
            else if (dp[i-1][j] < dp[i][j-1]){
                res = str1.charAt(i - 1) + res;
                i--;
            }
            else{
                res = str2.charAt(j - 1) + res;
                j--;
            } 
        }
        while (i > 0){
            res = str1.charAt(i - 1) + res;
            i--;
        }
        while (j > 0){
            res = str2.charAt(j - 1) + res;
            j--;
        }
        
        return res;
    }
}
```

<hr />