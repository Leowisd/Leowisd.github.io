---
title: Leetcode076-minimumWindowSubstring
categories: leetcode
tags: [Hash Table, Two Pointers, String, Sliding Window, Bloomberg, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:52:51
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

## Example
```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

* If there is no such window in S that covers all characters in T, return the empty string "".
* If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

## Solution
```java
// For most substring problem, we are given a string and need to find a substring of it which satisfy some restrictions. A general way is to use a hashmap assisted with two pointers. The template is given below.
// int findSubstring(string s){
//         int[] map = new int[128]; //used array instead hashmap could be more faster 
//         int counter; // check whether the substring is valid
//         int begin=0, end=0; //two pointers, one point to tail and one  head
//         int d; //the length of substring

//         for() { /* initialize the map here */ }

//         while(end<s.size()){

//             char ch1 = s.charAt(end);
//             if (map[ch1] > 0) {/* modify counter here */} 
//             map[ch1]--;
//             ch1++:

//             while(/* counter condition */){ 
                 
//                  /* update d here if finding minimum*/

//                 //increase begin to make it invalid/valid again
//                  char ch2 = s.charAt(begin);
//                  map[ch2]++;
//                  if (map[ch2] > 0) { /*modify counter here*/ }
//                 begin++
//             }  

//             /* update d here if finding maximum*/

//         }
//         return d;
//   }

class Solution {
    public String minWindow(String s, String t) {
        int[] map = new int[128];
        
        for (char ch: t.toCharArray()) map[ch]++;
        int maxLen = Integer.MAX_VALUE;
        int begin = 0;
        int end = 0;
        int count = t.length();
        int minStart = 0, minEnd = 0;
        
        while(end < s.length()){
            char cur = s.charAt(end);            
            if (map[cur] > 0) count--;
            map[cur]--;
            end++;
            
            while (count == 0){
                if (maxLen > end - begin){
                    maxLen = end- begin;
                    minStart = begin;
                    minEnd = end;
                }
                char ch =  s.charAt(begin);
                map[ch]++;
                if (map[ch] > 0) count++;
                begin++;
            }
        }
        if (maxLen == Integer.MAX_VALUE) return "";
        else return s.substring(minStart, minEnd);
    }
}
```

<hr />