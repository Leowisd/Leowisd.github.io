---
title: Leetcode022-generateParenthneses
categories: leetcode
tags: [String, Backtracking, Microsoft, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 15:36:26
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

## Example
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) return res;
        
        helper(n, res, 0, 0, "");
        return res;
    }
    
    private void helper(int n, List<String> res, int left, int right, String cur){
        if (left == n && right == n) {
            res.add(cur);
            return;
        }
        int maxLeft = n - left;
        if (maxLeft > 0){
            cur += "(";
            helper(n, res, left + 1, right, cur);
            if (cur.length() > 1) cur = cur.substring(0, cur.length() - 1);
            else cur = "";
        }
        
        int maxRight = left - right;
        if (maxRight > 0){
            cur += ")";
            helper(n, res, left, right + 1, cur);
            if (cur.length() > 1) cur = cur.substring(0, cur.length() - 1);
            else cur = "";
        }
    }
}
```

<hr />