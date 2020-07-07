---
title: Leetcode316-removeDuplicateLetters
categories: leetcode
tags: [Stack, Greedy]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:37:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string which contains only lowercase letters, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

## Example
**Example 1:**
```
Input: "bcabc"
Output: "abc"
```
**Example 2:**
```
Input: "cbacdcbc"
Output: "acdb"
```
**Note:** This question is the same as 1081: https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/

## Solution
```java
class Solution {
//  stack, O(n), faster
    public String removeDuplicateLetters(String s) {
        if (s == null || s.length() <= 1) return s;
        Stack<Character> st = new Stack<>();    
        int[] set = new int[128];   //record if stack has the character
        int[] map = new int[128];   //record the number of characters remaining
        for (char ch: s.toCharArray()){
            map[ch]++;
        }
        
        for (char ch: s.toCharArray()){
            if (set[ch] > 0) {
                map[ch]--;
                continue;
            }
            while (!st.isEmpty() && ch < st.peek() && map[st.peek()] > 0){
                set[st.pop()] = 0;
            }
            st.push(ch);
            set[ch] = 1;
            map[ch]--;
        }
        
        StringBuilder res = new StringBuilder();
        while(!st.isEmpty())
            res.append(st.pop());
        
        return res.reverse().toString();
    }
}
```

<hr />