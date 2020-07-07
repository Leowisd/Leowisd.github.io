---
title: Leetcode242-validAnagram
categories: leetcode
tags: [Hash Table, String, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 16:44:31
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings s and t , write a function to determine if t is an anagram of s.

## Example
**Example 1:**
```
Input: s = "anagram", t = "nagaram"
Output: true
```
**Example 2:**
```
Input: s = "rat", t = "car"
Output: false
```

**Note:**

You may assume the string contains only lowercase alphabets.

**Follow up:**

What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solution
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null && t == null) return false;
        if (s.length() != t.length()) return false;
        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++){
            count[s.charAt(i) - 'a'] ++;
            count[t.charAt(i) - 'a'] --;
        }
        for (int num : count)
            if (num != 0) return false;
        return true;
    }
}
```

<hr />