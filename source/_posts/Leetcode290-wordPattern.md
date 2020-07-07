---
title: Leetcode290-wordPattern
categories: leetcode
tags: [Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 23:38:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

## Example
**Example 1:**
```
Input: pattern = "abba", str = "dog cat cat dog"
Output: true
```
**Example 2:**
```
Input:pattern = "abba", str = "dog cat cat fish"
Output: false
```
**Example 3:**
```
Input: pattern = "aaaa", str = "dog cat cat dog"
Output: false
```
**Example 4:**
```
Input: pattern = "abba", str = "dog dog dog dog"
Output: false
```

**Notes:**


You may assume pattern contains only lowercase letters, and str contains lowercase letters that may be separated by a single space.

## Solution
```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
        HashMap<Character, String> map1 = new HashMap<>();
        HashMap<String, Character> map2 = new HashMap<>();
        String[] dic = str.split(" ");
        if (pattern.length() != dic.length) return false;
        for (int i = 0; i < dic.length; i++){
            char ch = pattern.charAt(i);
            if (!map1.containsKey(ch)){
                map1.put(ch, dic[i]);
                if (!map2.containsKey(dic[i])){
                    map2.put(dic[i], ch);
                }
                else return false;
            }
            else {
                if (!dic[i].equals(map1.get(ch))) return false;
            }
        }
        return true;
    }
}
```

<hr />