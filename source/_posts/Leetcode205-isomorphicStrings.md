---
title: Leetcode205-isomorphicStrings
categories: leetcode
tags: [Hash Table, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-05 11:15:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

## Example
**Example 1:**
```
Input: s = "egg", t = "add"
Output: true
```
**Example 2:**
```
Input: s = "foo", t = "bar"
Output: false
```
**Example 3:**
```
Input: s = "paper", t = "title"
Output: true
```
**Note:**
You may assume both s and t have the same length.

## Solution
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s == null || s.length() == 0 || s.length() == 1) return true;
        char[] a1 = s.toCharArray();
        char[] a2 = t.toCharArray();
        
        HashMap<Character, Character> map = new HashMap<>();
        map.put(a1[0], a2[0]);
        HashSet<Character> set = new HashSet<>();
        set.add(a2[0]);
        for (int i = 1; i < a1.length; i++){
            if (a1[i] == a1[i-1] && a2[i] == a2[i-1]) continue;
            if (a1[i] != a1[i-1] && a2[i] != a2[i-1]){
                if (map.containsKey(a1[i])){
                    if (map.get(a1[i]) == a2[i]) continue;
                    else return false;
                }
                else{
                    if (set.contains(a2[i])) return false;
                    map.put(a1[i], a2[i]);
                    set.add(a2[i]);
                    continue;
                }
            }
            return false;
        }
        return true;
    }
}
```

<hr />