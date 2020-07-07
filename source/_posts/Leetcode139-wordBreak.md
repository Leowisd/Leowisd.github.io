---
title: Leetcode139-wordBreak
categories: leetcode
tags: [DP, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 21:04:59
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

## Example
**Example 1:**
```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```
**Example 2:**
```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```
**Example 3:**
```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```
## Solution
```java
public class Solution {
    public boolean wordBreak(String s, List<String> dict) {
        HashSet<String> set = new HashSet<>();
        for (String st: dict){
            set.add(st);
        }
        boolean[] f = new boolean[s.length() + 1];
        
        f[0] = true;
        
        
        // First DP O(N*M)
        for(int i = 1; i <= s.length(); i++){
            for(String str: dict){
                if(str.length() <= i){
                    if(f[i - str.length()]){
                        if(s.substring(i-str.length(), i).equals(str)){
                            f[i] = true;
                            break;
                        }
                    }
                }
            }
        }
        
        //Second DP O(N^2)
        // for(int i=1; i <= s.length(); i++){
        //     for(int j=0; j < i; j++){
        //         if(f[j] && dict.contains(s.substring(j, i))){
        //             f[i] = true;
        //             break;
        //         }
        //     }
        // }
        
        return f[s.length()];
    }
}
```

memorizal DFS, O(n!)
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> set = new HashSet<>();
        HashSet<String> memory = new HashSet<>();
        for (String st: wordDict){
            set.add(st);
        }        
        return helper(s, set, memory);
    }
    
    private boolean helper(String s, HashSet<String> set, HashSet<String> memory){
        // System.out.println(s);
        if (set.contains(s)) return true;
        for (int i = 1; i < s.length(); i++){
            String tmp = s.substring(0, i);
            String rest = s.substring(i, s.length());
            if (set.contains(tmp) && !memory.contains(rest))
                if (helper(rest, set, memory)) return true;
                else memory.add(rest);
        }
        return false;
    }
}
```

<hr />