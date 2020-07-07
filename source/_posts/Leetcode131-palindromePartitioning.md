---
title: Leetcode131-palindromePartitioning
categories: leetcode
tags: [Backtracking]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-08 23:07:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

## Example
```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

## Solution
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        if (s.length() == 0){
            res.add(new ArrayList<>());
            return res;
        }
        helper(res, s, new ArrayList<String>(), 0);
        return res;
    }
    private void helper(List<List<String>> res, String s, List<String> temp, int index){
        if (index > s.length()-1){
            res.add(new ArrayList<>(temp));
        } 
        for (int i = index + 1; i <= s.length(); i++){
            String cur = s.substring(index, i);
            if (!isPalindrome(cur)) continue; 
            temp.add(cur);
            helper(res, s, temp, i);
            temp.remove(temp.size()-1);
        }
    }
    private boolean isPalindrome(String s){
        int left = 0;
        int right = s.length()-1;
        while(left < right){
            if (s.charAt(left) != s.charAt(right)) return false;
            left ++;
            right --;
        }
        return true;
    }
}
```

<hr />