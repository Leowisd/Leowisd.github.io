---
title: Leetcode386-Lexicographical Numbers
categories: leetcode
tags: [DFS, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-07 00:41:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer n, return 1 - n in lexicographical order.

For example, given 13, return: [1,10,11,12,13,2,3,4,5,6,7,8,9].

Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        List<Integer> res = new ArrayList<>();
        for (int i = 1; i <= 9; i++){
            helper(i, n, res);
        }
        return res;
    }
    
    private void helper(int cur, int n, List<Integer> res){
        if (cur > n){
            return;
        }
        
        res.add(cur);
        for (int i = 0; i <= 9; i++){
            int newInt = cur * 10 + i;
            if (newInt > n) return;
            helper(newInt, n, res);
        }
    }
}
```

<hr />