---
title: Leetcode392-isSubsequence
categories: leetcode
tags: [DP, Binary Search, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:17:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s and a string t, check if s is subsequence of t.

You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).

## Example
**Example 1:**
```
s = "abc", t = "ahbgdc"

Return true.
```

**Example 2:**
```
s = "axc", t = "ahbgdc"
Return false.
```
**Follow up:**
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

## Solution
**Solution 1**
```java
class Solution {
//     faster basic solution
    public boolean isSubsequence(String s, String t) {
        for(char c:s.toCharArray()){
            int index = t.indexOf(c);
            if(index < 0){
               return false; 
            }
            t = t.substring(index+1);
        }
        return true;
    }
}
```

**Solution 2**
```java
class Solution {
// two pointers, basic solution
    public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) return true;
        int indexS = 0, indexT = 0;
        while (indexT < t.length()) {
            if (t.charAt(indexT) == s.charAt(indexS)) {
                indexS++;
                if (indexS == s.length()) return true;
            }
            indexT++;
        }
        return false;
    }
}
```

**Solution 3**
```java
class Solution {
// binary search + index recording, for follow up
    public boolean isSubsequence(String s, String t) {
        List<Integer>[] index = new List[128];
        for (int i = 0; i < t.length(); i++){
            if (index[t.charAt(i)] == null)
                index[t.charAt(i)] = new ArrayList<>();
            index[t.charAt(i)].add(i);
        }
        
        int pre = -1;
        for (int i = 0; i < s.length(); i++){
            if (index[s.charAt(i)] == null) return false;
            int cur = helper(index[s.charAt(i)], pre);
            if (cur == -1) return false;
            pre = cur;
        }
        return true;
    }
    private int helper(List<Integer> list, int target){
        int left = 0;
        int right = list.size() - 1;
        
        while(left < right){
            int mid = (left + right)/2;
            if (list.get(mid) <= target)
                left = mid + 1;
            else right = mid;
        }
        if (list.get(left) > target) return list.get(left);
        else return -1;
    }
}
```
<hr />