---
title: Leetcode567-Permutation In String
categories: leetcode
tags: [Two Pointers, Sliding Window, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-08 00:23:47
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

## Example

**Example 1:**
```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```
**Example 2:**
```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

**Constraints:**

* The input strings only contain lower case letters.
* The length of both given strings is in range [1, 10,000].

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(1)$$

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] map = new int[26];
        for (int i = 0; i < s1.length(); i++){
            map[s1.charAt(i) - 'a']++;
        }
        
        int match = 0;
        for (int i = 0, j = 0; j < s2.length(); j++){
            if (map[s2.charAt(j) - 'a'] > 0){
                if (++match == s1.length()){
                    return true;
                }
            }
            map[s2.charAt(j) - 'a']--;
            if (j >= s1.length() - 1){
                if (map[s2.charAt(i) - 'a'] >= 0){
                    match--;
                }
                map[s2.charAt(i) - 'a']++;
                i++;
                // if (map[s2.charAt(i++) - 'a']++ >= 0){
                //     match--;
                // }
            }
        }
        return false;
    }
}
```

<hr />