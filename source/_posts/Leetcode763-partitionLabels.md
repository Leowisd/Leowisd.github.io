---
title: Leetcode763-partitionLabels
categories: leetcode
tags: [Two Pointers, Greedy, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 20:23:45
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

## Example
```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```
**Note:**

1. S will have length in range [1, 500].
2. S will consist of lowercase letters ('a' to 'z') only.
3. 
## Solution
```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        List<Integer> res = new ArrayList<>();
        if (S == null || S.length() == 0) return res;
        
        int[] index = new int[26];
        for (int i = 0; i < S.length(); i++){
            index[S.charAt(i) - 'a'] = i;
        }
        
        int start = 0;
        int end = 0;
        for (int i = 0; i < S.length(); i++){
            end = Math.max(end, index[S.charAt(i) - 'a']);
            if (end == i){
                res.add(end - start + 1);
                start = end + 1;
            }
        }
        
        return res;
    }
}
```

<hr />