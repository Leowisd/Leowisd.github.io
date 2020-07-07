---
title: Leetcode409-longestPalindrome
categories: leetcode
tags: [Hash Table, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-16 20:58:19
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

**Note:**
Assume the length of given string will not exceed 1,010.

## Example
```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

## Solution
```java
class Solution {
    public int longestPalindrome(String s) {
        if (s == null || s.length() == 0) return 0;
        HashSet<Character> set = new HashSet<>();
        int res = 0;
        for (char ch: s.toCharArray()){
            if (set.contains(ch)){
                set.remove(ch);
                res++;
            }
            else set.add(ch);
        }
        if (!set.isEmpty()) return 2*res + 1;
        return 2*res;
    }
}
```

<hr />